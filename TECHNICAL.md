# Technical Documentation: Windows 11 HiDPI Cursor Fix

## Overview

This document explains the technical approach used to solve cursor blurriness on Windows 11, including the build process, multi-resolution layering, and how Windows 11 uses these cursors.

## The Problem: Display Scaling and Cursor Blurriness

### Traditional Single-Resolution Cursors

Standard cursor files (`.cur` format) used in Windows typically contain:
- **Single resolution:** 32×32 pixels
- **Color data:** Standard RGBA or indexed
- **No scaling logic:** Just the raw bitmap

When a user on Windows 11 sets their display scaling to 150% or higher:

```
Original cursor (32×32 px)
↓ (Windows scales up)
Display at 48×48 px (on 150% scaling)
↓ (Interpolation/nearest neighbor)
BLURRY or PIXELATED appearance
```

### Why This Happens

Windows 11 uses linear interpolation or nearest-neighbor sampling to scale the 32px cursor to larger sizes. Both methods produce poor visual results:
- **Linear interpolation:** Creates soft, blurry edges
- **Nearest neighbor:** Creates jagged, pixelated edges

### The Scale Problem in Numbers

On modern displays, this affects many users:

| Display | Resolution | Typical Scaling | Cursor at | Issue |
|---------|-----------|-----------------|-----------|-------|
| Laptop | 1440p | 150% | 48×48 px | Blurry |
| 4K Monitor | 3840×2160 | 200% | 64×64 px | Blurry |
| Ultrawide 1440p | 3440×1440 | 125% | 40×40 px | Blurry |

## The Solution: Multi-Resolution Cursor Layering

### How It Works

Instead of a single 32×32 cursor, these cursors contain **7 resolution layers** inside each `.cur` or `.ani` file:

```
cursor.cur (single file, multiple resolutions inside)
├─ Layer 1: 32×32 px   (for 100% scaling / 96 DPI)
├─ Layer 2: 40×40 px   (for 125% scaling / 120 DPI)
├─ Layer 3: 48×48 px   (for 150% scaling / 144 DPI)
├─ Layer 4: 64×64 px   (for 200% scaling / 192 DPI)
├─ Layer 5: 80×80 px   (for 250% scaling / 240 DPI)
├─ Layer 6: 96×96 px   (for 300% scaling / 288 DPI)
└─ Layer 7: 128×128 px (for 400% scaling / 384+ DPI)
```

When Windows 11 loads the cursor, it:

1. **Detects current display scaling:** e.g., 150%
2. **Looks up the matching layer:** 48×48 px layer
3. **Uses exact resolution:** No scaling needed
4. **Result:** **Perfect, sharp cursor**

### Technical Advantage

- **No interpolation needed:** Cursor displays at native resolution
- **Perfect anti-aliasing:** Pre-rendered at the target size
- **No aliasing artifacts:** No pixelation or blur
- **Minimal file size impact:** Compressed storage inside `.cur` file

## The Build Process

### Step 1: Source Rendering

**Input:** Original Capitaine Cursors SVG designs

**Tool:** Inkscape + custom build script

**Process:**
- SVG vector graphics rendered at 7 different scales
- Each scale produces individual PNG files
- Anti-aliasing and filtering applied at render time

**Output:**
```
_build/
├── x1/
│   ├── arrow.png (32×32)
│   ├── crosshair.png (32×32)
│   └── ...
├── x1.25/
│   ├── arrow.png (40×40)
│   └── ...
├── x1.5/
│   ├── arrow.png (48×48)
│   └── ...
├── x2/
│   ├── arrow.png (64×64)
│   └── ...
├── x2.5/
│   ├── arrow.png (80×80)
│   └── ...
├── x3/
│   ├── arrow.png (96×96)
│   └── ...
└── x4/
    ├── arrow.png (128×128)
    └── ...
```

### Step 2: Cursor Assembly

**Tool:** `xcursorgen` (X11 cursor generation utility)

**Process:**
- Reads cursor specifications (hotspot, animation timing)
- Combines PNG layers from all scales into index files
- Creates X cursor format with embedded resolution information

**Cursor specification example:**
```
# This allows automatic loading of the best resolution
32 0 0 x1/arrow.png
40 0 0 x1.25/arrow.png
48 0 0 x1.5/arrow.png
64 0 0 x2/arrow.png
80 0 0 x2.5/arrow.png
96 0 0 x3/arrow.png
128 0 0 x4/arrow.png
```

**Output:** Linux cursor files with embedded multi-resolution support

### Step 3: Windows Format Conversion

**Tool:** Custom converter (Windows cursor format generator)

**Process:**
- X cursor files converted to Windows `.cur` format
- Maintains all resolution layers embedded in the file
- Preserves resolution metadata for Windows 11 selection

**Format differences:**
- **X cursor:** Uses cursor name → resolution mapping
- **Windows cursor:** Embeds resolution info inside file using hotspot variations

**Output:**
```
Windows cursor files (.cur):
├── arrow.cur (multiple resolutions embedded)
├── help.cur
├── text.cur
└── ...
```

## Windows 11 Cursor Selection Algorithm

### How Windows 11 Chooses Which Resolution

When Windows 11 applies these cursors to your system, it uses this logic:

```
1. Read current display scaling: GetSystemMetrics(SM_CXCURSOR)
   → Returns logical cursor size (e.g., 48 for 150% scaling)

2. Compare against embedded resolutions in cursor file
   → 32, 40, 48, 64, 80, 96, 128

3. Select best match:
   - If exact match exists → Use it
   - If no exact match → Use closest larger resolution
   - If smaller only available → Use largest available

4. Load and display selected resolution
   → No runtime scaling needed
```

### Scaling Support Matrix

| Windows Setting | Display Scaling | System DPI | Cursor Size | Layer Used |
|---|---|---|---|---|
| Display settings → 100% | 100% | 96 DPI | 32×32 | x1 |
| Display settings → 125% | 125% | 120 DPI | 40×40 | x1.25 |
| Display settings → 150% | 150% | 144 DPI | 48×48 | x1.5 |
| Display settings → 175% | 175% | 168 DPI | 56×56 | x2 (closest) |
| Display settings → 200% | 200% | 192 DPI | 64×64 | x2 |
| Display settings → 225% | 225% | 216 DPI | 72×72 | x2.5 (closest) |
| Display settings → 250% | 250% | 240 DPI | 80×80 | x2.5 |
| Display settings → 300% | 300% | 288 DPI | 96×96 | x3 |
| Display settings → 400% | 400% | 384 DPI | 128×128 | x4 |

## File Format Details

### Windows Cursor File Structure (.cur)

```
File Structure:
├─ Header (6 bytes)
│  ├─ Reserved (2 bytes) = 0x0000
│  ├─ Type (2 bytes) = 0x0002 (cursor)
│  └─ Count (2 bytes) = number of images
├─ Directory entries (per image)
│  ├─ Width (1 byte)
│  ├─ Height (1 byte)
│  ├─ Color count (1 byte)
│  ├─ Reserved (1 byte)
│  ├─ Hotspot X (2 bytes)
│  ├─ Hotspot Y (2 bytes)
│  ├─ Size (4 bytes)
│  └─ Offset (4 bytes)
└─ Image data blocks
   ├─ BMP image 1 (32×32)
   ├─ BMP image 2 (40×40)
   ├─ BMP image 3 (48×48)
   ├─ BMP image 4 (64×64)
   ├─ BMP image 5 (80×80)
   ├─ BMP image 6 (96×96)
   └─ BMP image 7 (128×128)
```

### Animation Files (.ani)

Animated cursors use a container format:

```
.ani (RIFF format)
├─ RIFF header
├─ ANIH chunk (animation info)
│  ├─ Frame count
│  ├─ Step count (frame duration)
│  └─ Width/Height
├─ RATE chunk (per-frame delays)
└─ fram chunks (compiled .cur files)
   ├─ Multiple resolution cursor 1
   ├─ Multiple resolution cursor 2 (next frame)
   └─ ...
```

## Performance Implications

### File Size

| Type | Single-res 32×32 | Multi-res (x1 to x4) | Increase |
|---|---|---|---|
| Static cursor (.cur) | ~5-15 KB | ~20-40 KB | 2-3× |
| Animated (10 frames) | ~50-100 KB | ~150-250 KB | 2-3× |

**Impact:** Negligible. Typical full cursor set: ~2-3 MB vs ~1 MB for single-res.

### Runtime Performance

- **Loading time:** No impact (cursors cached after first load)
- **Memory:** Same; only active cursor in memory
- **Rendering:** Identical (no scaling needed)

## Compatibility

### Windows 11
- ✅ **Full support** — Selects correct resolution automatically
- ✅ **Future compatible** — Additional DPI scales can be added

### Windows 10
- ⚠️ **Partial support** — Works but may not correctly select resolution layer
- ⚠️ **May use wrong layer** — Depends on Windows 10 cursor selection algorithm
- ⚠️ **Fallback behavior** — Uses first/best available layer

### Windows 8 and Earlier
- ❌ **Not supported** — Older cursor format incompatible

## Installation Method: .inf Files

### How install.inf Works

The `install.inf` file is a Windows Registry installer:

```ini
; install.inf
[Version]
Signature = "$CHICAGO$"

[DefaultInstall]
CopyFiles = Scheme.Cur
AddReg    = Scheme.Reg

[Scheme.Reg]
; Add registry entries pointing to cursor files
HKLM,"SOFTWARE\Microsoft\Windows\CurrentVersion\Control Panel\Cursors\Schemes","Capitaine HiDPI",,
    "%10%\Cursors\Capitaine HiDPI\arrow.cur,..."
```

When right-clicked and installed:

1. **Extracts cursor files** to `%SystemRoot%\Cursors\Capitaine HiDPI\`
2. **Adds registry keys** to `HKEY_LOCAL_MACHINE\SOFTWARE\...\Cursors\Schemes\`
3. **Registers cursor scheme** name as selectable option in Settings
4. **Windows recognizes immediately** — Theme appears in Personalization settings

## Future Improvements

### Potential Enhancements

- **Higher DPI support:** Add x5, x6, x10 layers for 500%+ scaling
- **Color variants:** Additional shades or accent colors
- **Hardware cursor optimization:** GPU-accelerated rendering on supported displays
- **Dynamic loading:** Load only necessary layers based on system DPI

## References

- [Windows Cursor Format Documentation](https://en.wikipedia.org/wiki/Cursor_(user_interface)#File_format)
- [X11 Cursor Format](https://man.archlinux.org/man/xcursor.core.5)
- [High DPI Support in Windows](https://learn.microsoft.com/en-us/windows/win32/hidpi/high-dpi-desktop-application-development-on-windows)
- [Original Capitaine Cursors](https://github.com/keeferrourke/capitaine-cursors)
