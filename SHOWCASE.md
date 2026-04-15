# Visual Showcase: Capitaine Cursors HiDPI

This page demonstrates the clarity improvement of multi-resolution cursors on Windows 11 displays with scaling.

## The Difference: Blurry vs. Sharp

### Display Scaling at 150% (48×48 pixels)

**Before (Standard Single-Resolution Cursor):**
- Windows stretches 32×32 px → 48×48 px
- Linear interpolation causes blurriness
- Jagged edges on diagonal elements
- Hard to see text cursor precisely

**After (This Project: Multi-Resolution):**
- Cursor rendered natively at 48×48 px
- Pixel-perfect edges
- Anti-aliasing applied at intended resolution
- Clear, precise appearance
- Visual weight matches design intent

---

## Display Scaling Scenarios

### Scenario 1: 4K Monitor with Standard Scaling

| Setting | Before | After |
|---------|--------|-------|
| **Display** | 3840×2160 (4K) | Same |
| **Scaling** | 100% (native resolution) | Same |
| **Cursor Size** | 32×32 px (tiny on 4K) | Uses 80×80 px layer |
| **Appearance** | Can be hard to see | Clearly visible, no blur |

---

### Scenario 2: Laptop with 150% UI Scaling

| Setting | Before | After |
|---------|--------|-------|
| **Display** | 1440p laptop | Same |
| **Scaling** | 150% (UI scaled) | Same |
| **Cursor Size** | Stretched to 48×48 | Native 48×48 px |
| **Appearance** | **Blurry** 😕 | **Sharp** ✅ |

---

### Scenario 3: Ultrawide at 125% Scaling

| Setting | Before | After |
|---------|--------|-------|
| **Display** | 3440×1440 ultrawide | Same |
| **Scaling** | 125% | Same |
| **Cursor Size** | Stretched to 40×40 | Native 40×40 px |
| **Appearance** | **Pixelated** 😕 | **Perfect** ✅ |

---

## Cursor Variants Comparison

### Light Variant (White/Light Strokes)

**Best for:**
- Dark wallpapers
- Dark Windows themes
- Night mode
- Dark IDEs (VS Code dark theme)

**Visual characteristics:**
- Thin, elegant strokes
- High contrast on dark backgrounds
- Professional appearance
- Similar to macOS aesthetic

---

### Dark Variant (Black/Dark Strokes)

**Best for:**
- Light wallpapers
- Light Windows themes
- Bright IDE themes
- Accessibility (easier to see)

**Visual characteristics:**
- Thicker, bolder strokes
- High contrast on light backgrounds
- Clear and visible
- Gaming-friendly

---

## Resolution Layers in Action

This table shows how the cursor appears at different display scales using embedded resolution layers:

| Scale | Cursor Size | Resolution Layer | Rendering | Result |
|-------|------------|------------------|-----------|--------|
| 100% | 32×32 px | x1 (native) | No scaling | ✅ Perfect |
| 125% | 40×40 px | x1.25 (native) | No scaling | ✅ Perfect |
| 150% | 48×48 px | x1.5 (native) | No scaling | ✅ Perfect |
| 175% | 56×56 px | x2 (closest) | Tiny scale up | ✅ Good |
| 200% | 64×64 px | x2 (native) | No scaling | ✅ Perfect |
| 250% | 80×80 px | x2.5 (native) | No scaling | ✅ Perfect |
| 300% | 96×96 px | x3 (native) | No scaling | ✅ Perfect |
| 400% | 128×128 px | x4 (native) | No scaling | ✅ Perfect |

**Legend:**
- **Native** = Exact resolution available, pixel-perfect
- **Closest** = Nearest available resolution, very minor upscaling
- **No scaling** = Uses exact matching layer, no interpolation

---

## Application Examples

### Web Browser at 150% Scaling

**Standard cursor:**
- Blurry text cursor when hovering text
- Blurry link pointer
- Blurry loading cursor (progress animation)

**This project:**
- Sharp text selection cursor
- Clear hyperlink indicator
- Crisp animated progress spinner

### Text Editor at 200% Scaling (High Zoom)

**Standard cursor:**
- Blurry blinking text cursor
- Blurry resize cursor on column dividers
- Blurry drag handle

**This project:**
- Clear, visible text insertion cursor
- Sharp resize indicators
- Precise drag handles

### Gaming at 4K with Scaling

**Standard cursor:**
- Tiny, hard-to-see cursor
- Blurry appearance
- May be difficult to find on screen

**This project:**
- Large, visible cursor (80-96px)
- Crystal clear edges
- Easy to locate and track

---

## Technical Details

For more information on how this works, see [TECHNICAL.md](./TECHNICAL.md#windows-11-cursor-selection-algorithm)

---

## Your Experience

Have you noticed the difference? Share your setup:
- Display resolution
- Scaling percentage
- Cursor variant chosen (Light/Dark)
- Any specific application where the improvement is most noticeable

[Open a GitHub Discussion](../../discussions) or [Create an Issue](../../issues) to share your experience!
