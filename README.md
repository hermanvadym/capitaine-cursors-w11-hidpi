# Capitaine Cursors for Windows 11 (HiDPI Optimized)

This is an adaptation of the beautiful [Capitaine Cursors](https://github.com/keeferrourke/capitaine-cursors) theme by Keefer Rourke, optimized for sharp, crisp rendering on Windows 11 with high-DPI displays.

## The Problem: Blurry Cursors on Windows 11

Standard cursor files contain only a single resolution (typically 32×32 pixels). When used on Windows 11 with:
- High-resolution displays (2K, 4K)
- Display scaling enabled (125%, 150%, 200%, 250%)
- System DPI set above 96 DPI

Windows must artificially scale and interpolate the small cursor image, resulting in a **blurry, pixelated appearance**. This is particularly noticeable on:
- High-refresh-rate gaming displays
- Ultrawide monitors
- Scaled laptops (e.g., 1440p or 4K at 150% UI scale)

## The Solution: Multi-Resolution Cursor Layering

This project uses **Windows cursor layering**: multiple cursor resolutions embedded inside single `.cur` (static) and `.ani` (animated) files. Windows 11 examines your display scaling setting and loads the exact resolution layer that matches—no scaling needed, no blurriness.

### How It Works (Technical Details)

**Traditional single-resolution cursor:**
```
cursor.cur → 32×32 px → Windows scales to 64×64 → BLURRY
```

**Layered multi-resolution cursor (this project):**
```
cursor.cur contains:
├─ Resolution 1: 32×32 px   (for 100% scaling)
├─ Resolution 2: 40×40 px   (for 125% scaling)
├─ Resolution 3: 48×48 px   (for 150% scaling)
├─ Resolution 4: 64×64 px   (for 200% scaling)
├─ Resolution 5: 80×80 px   (for 250% scaling)
├─ Resolution 6: 96×96 px   (for 300% scaling)
└─ Resolution 7: 128×128 px (for 400% scaling)

Windows 11 loads the perfect match → NO scaling → SHARP
```

### Build Process

Each cursor was built using the original Capitaine Cursors SVG sources:
Quick Start (30 seconds)

1. **Download** the latest release from the [Releases page](../../releases)
2. **Extract** the ZIP
3. **Right-click** `capitaine-light/install.inf` (or `capitaine-dark/install.inf`)
4. Select **Install**
5. Go to **Settings** → **Personalization** → **Mouse pointer** → Select **"Capitaine HiDPI"**

That's it. Your cursors are now sharp at any zoom level.

### Detailed Instructions

See [INSTALL.md](INSTALL.md) for step-by-step instructions, troubleshooting, and manual installation options.

### Supported Windows Versions

| OS | Status | Notes |
|---|---|---|
| Windows 11 | ✅ **Full support** | Optimized; multi-layer cursors fully utilized |
| Windows 10 | ⚠️ Works | Basic support; HiDPI features may be limited |
| Windows 8/8.1 | ❌ Not tested | Format compatibility unknown |
| Windows 7 | ❌ Not compatible | Older cursor format |
4. **Restart your computer** (some apps may require restart to apply)
5. **Apply the theme**:
   - Open **Settings** → **Personalization** → **Mouse pointer**
   - Select **"Capitaine Cursors Light"** or **"Capitaine Cursors Dark"**

### Windows 11 (Manual Method)

If you prefer not to run scripts:

1. Extract the archive
2. Open the theme folder (e.g., `capitaine-light/`)
3. Press `Win + R` and type: `%AppData%\CursorSchemes`
4. Paste the theme folder into the CursorSchemes directory
5. Open **Settings** → **Personalization** → **Mouse pointer** and select the theme

### Windows 10 and Earlier

These cursors are optimized for Windows 11. They may work on Windows 10 but are not officially tested on earlier versions.

## Variants

- **Light** (`capitaine-light/`) — White cursors on dark backgrounds
- **Dark** (`capitaine-dark/`) — Black cursors on light backgrounds

Choose the variant that provides best contrast with your wallpaper/theme:

- **Light** (`capitaine-light/`) — Thin white/light strokes; ideal for dark backgrounds
- **Dark** (`capitaine-dark/`) — Thick black/dark strokes; ideal for light backgrounds

Both variants include all cursor states (busy, resize, text select, move, etc.) and animated cursors (progress, wait).

## Troubleshooting

See [INSTALL.md](INSTALL.md#troubleshooting) for detailed troubleshooting, uninstallation, and advanced configuration.
All standard X cursor names are supported:

**Static cursors:** default, pointer, context-menu, help, progress, wait, crosshair, text, vertical-text, alias, copy, move, no-drop, not-allowed, all-scroll, col-resize, row-resize, cell, size_bdiag, size_fdiag, size_hor, size_ver, top_left_corner, top_right_corner, bottom_left_corner, bottom_right_corner, left_side, right_side, top_side, bottom_side, and more.

**Animated cursors:** progress, wait, and other animations for visual feedback.

## Attribution

This is an adaptation of [Capitaine Cursors](https://github.com/keeferrourke/capitaine-cursors) by **Keefer Rourke**, originally based on [KDE Breeze](https://github.com/KDE/breeze).

**What was adapted:**
- Original cursor designs: ✓ Used unchanged
- Multi-resolution layering: ✓ Added for HiDPI support
- Windows installer: ✓ Added for easy installation
- Windows 11 documentation: ✓ Added

## License

Licensed under **GNU Lesser General Public License (LGPL) v3 or later**. See [COPYING](COPYING).

You may freely use, modify, and redistribute these cursors provided you:
- Include the LGPL v3 license
- Attribute the original Capitaine Cursors authors
- License modifications under the same license

## Contributing

Found an issue? Have a suggestion?

- Report issues on the [Issues page](../../issues)
- Original project: [keeferrourke/capitaine-cursors](https://github.com/keeferrourke/capitaine-cursors)

## Related Projects

- [Capitaine Cursors](https://github.com/keeferrourke/capitaine-cursors) — Original X11/Linux cursor theme
- [KDE Breeze](https://github.com/KDE/breeze) — Icon theme inspiration
- [La Capitaine Icons](https://github.com/keeferrourke/la-capitaine-icon-theme) — Companion icon theme

---

**Enjoy sharp, beautiful cursors on Windows 11!** 🎯
