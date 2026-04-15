# Capitaine Cursors for Windows 11 (HiDPI Optimized)

[![License: LGPL v3](https://img.shields.io/badge/License-LGPL%20v3-blue.svg)](./LICENSE)
[![Windows 11](https://img.shields.io/badge/Windows-11-0078D4.svg)](https://www.microsoft.com/windows/windows-11)
[![HiDPI Support](https://img.shields.io/badge/HiDPI-7%20Scales-green.svg)](./TECHNICAL.md)
[![Cursor Variants](https://img.shields.io/badge/Variants-Light%20%7C%20Dark-orange.svg)]()

**Stop blurry cursors on Windows 11.** Sharp, pixel-perfect cursors optimized for high-resolution displays, ultrawide monitors, and scaled laptops.

This is a professional adaptation of [**Capitaine Cursors**](https://github.com/keeferrourke/capitaine-cursors) by Keefer Rourke, optimized for Windows 11 HiDPI displays using multi-resolution cursor layering.

---

## ⚡ Quick Start (30 Seconds)

1. [**Download latest release**](../../releases/latest) → Extract ZIP
2. Open `capitaine-light/` or `capitaine-dark/`
3. **Right-click** `install.inf` → **Select "Install"**
4. **Settings** → **Personalization** → **Mouse pointer** → Select **"Capitaine HiDPI"**

Done! Your cursors are now sharp at any zoom level.

**Quick links:** [📖 Full Guide](INSTALL.md) • [🔧 Technical Details](TECHNICAL.md)

---

## 👁️ Preview

### Light Variant
![Capitaine Cursors Light](https://raw.githubusercontent.com/keeferrourke/capitaine-cursors/master/preview-light.png)

### Dark Variant
![Capitaine Cursors Dark](https://raw.githubusercontent.com/keeferrourke/capitaine-cursors/master/preview-dark.png)

*Preview images from the original [Capitaine Cursors](https://github.com/keeferrourke/capitaine-cursors) project.*

---

## ❌ The Problem: Blurry Cursors on Windows 11

Standard cursor files contain only a single **32×32 pixel** image. On Windows 11 with:
- **4K monitors** or high-resolution displays (2K, ultrawide)
- **Display scaling** (125%, 150%, 200%, 250%)
- **High DPI laptops** (4K MacBook-equivalent displays)

Windows must stretch and interpolate this small image, causing **blurriness and pixelation**.

**This affects:**
- ❌ 4K monitor users
- ❌ Gaming laptop owners with high-refresh displays
- ❌ Users with display scaling enabled
- ❌ Ultrawide monitor enthusiasts
- ❌ Anyone seeking accessibility (blurry icons are hard to see)

---

## ✅ The Solution: Multi-Resolution HiDPI Cursors

These cursors contain **7 embedded resolution layers** (32px to 128px) inside each file. Windows 11 automatically selects the exact resolution matching your display scaling—**no stretching, no blurriness**.

```
Standard cursor:      cursor.cur (32×32) → Windows stretches → BLURRY ❌

This project:         cursor.cur contains 7 layers:
                      ├─ 32×32 px  (100% scaling)
                      ├─ 40×40 px  (125% scaling)
                      ├─ 48×48 px  (150% scaling)  ← Windows picks this at 150%
                      ├─ 64×64 px  (200% scaling)
                      ├─ 80×80 px  (250% scaling)
                      ├─ 96×96 px  (300% scaling)
                      └─ 128×128 px (400% scaling)
                      
Result:               No scaling needed → PIXEL-PERFECT ✅
```

**See [TECHNICAL.md](TECHNICAL.md) for complete technical explanation.**

---

## 🎯 Why This Project?

| Feature | Standard Cursors | This Project |
|---------|---|---|
| **Sharpness at 150% scale** | ❌ Blurry/pixelated | ✅ Crystal clear |
| **4K display support** | ❌ Blurry appearance | ✅ Perfect rendering |
| **Ultrawide support** | ❌ Blurry stretching | ✅ Sharp at any ratio |
| **Installation** | Manual registry hacking | ✅ One right-click (install.inf) |
| **Variants** | Limited options | ✅ Light + Dark |
| **Open source** | Varies | ✅ LGPL v3 licensed |
| **Based on** | Unknown origin | ✅ Beautiful Capitaine design |

---

## 📦 What's Included

✅ **2 Cursor Themes**
- Light variant (white strokes for dark backgrounds)
- Dark variant (black strokes for light backgrounds)

✅ **7 Resolution Scales** (32px to 128px)
- Supports display scaling: 100%, 125%, 150%, 200%, 250%, 300%, 400%

✅ **17+ Cursor Types**
- Standard pointer, text, help, link, move, resize (8 directions)
- Animated cursors (progress, working/busy)
- Complete Windows cursor coverage

✅ **Complete Documentation**
- Installation guide with troubleshooting
- Technical deep-dive on HiDPI architecture
- Visual showcase and comparisons

✅ **Easy Installation**
- `install.inf` for automatic Windows Registry integration
- No scripts to run, no administrator hassle
- One right-click: "Install"

**Repository size:** 38 files • **Package size:** ~2 MB

---

## 💻 System Requirements & Compatibility

| OS | Status | Notes |
|---|---|---|
| **Windows 11** | ✅ **FULLY SUPPORTED** | Optimized; all HiDPI layers utilized |
| **Windows 10** | ⚠️ Works | Partial support; may not use all layers |
| **Windows 8/8.1** | ❓ Untested | Compatibility unknown |
| **Windows 7** | ❌ Not compatible | Cursor format incompatible |

**Display scaling supported:** 100%, 125%, 150%, 200%, 250%, 300%, 400%

---

## 📥 Installation

### Method 1: Automatic Install (Recommended)

1. [Download latest release](../../releases/latest)
2. Extract the ZIP archive
3. Open `capitaine-light/` or `capitaine-dark/`
4. **Right-click** `install.inf` → **Select "Install"**
5. **Settings** → **Personalization** → **Mouse pointer** → Select **"Capitaine HiDPI"**

### Method 2: Manual Installation

1. Extract ZIP
2. Press `Win + R` → Type `%AppData%\CursorSchemes` → Enter
3. Copy `capitaine-light` or `capitaine-dark` folder into CursorSchemes
4. **Settings** → **Personalization** → **Mouse pointer** → Select **"Capitaine HiDPI"**

**[See INSTALL.md](INSTALL.md) for troubleshooting, uninstalling, and advanced options.**

---

## 🎨 Themes & Variants

### Light Variant (Recommended for Dark Backgrounds)
- Thin, elegant white/light strokes
- High contrast on dark wallpapers
- Professional, macOS-like appearance
- Great for dark Windows themes and IDEs

### Dark Variant (Recommended for Light Backgrounds)
- Thicker, bolder black/dark strokes
🎨 Visual Showcase

See **[SHOWCASE.md](SHOWCASE.md)** for:
- Before/after comparisons at different scales
- Display scenario walkthroughs (4K, 150% scaling, ultrawide)
- Variant comparisons
- How resolution layers work visually

---

## 📚 Learn More

- **[Installation Guide](INSTALL.md)** — Complete installation instructions + troubleshooting
- **[Technical Deep Dive](TECHNICAL.md)** — How the HiDPI fix works under the hood

---

## 🏆 Credits

An adaptation of [**Capitaine Cursors**](https://github.com/keeferrourke/capitaine-cursors) by [Keefer Rourke](https://krourke.org), originally based on [KDE Breeze](https://github.com/KDE/breeze).

**What this project adds:**
- ✅ Multi-resolution HiDPI cursor layers
- ✅ Windows 11 optimization and testing
- ✅ Automatic installation via `install.inf`
- ✅ Comprehensive Windows documentation

---

## 📜 License

Licensed under **GNU Lesser General Public License (LGPL) v3 or later**

**You can:**
- Use freely for personal or commercial use
- Modify and improve
- Redistribute your changes

**You must:**
- Include the LGPL v3 license
- Attribute original Capitaine Cursors authors
- License modifications under the same license

See [LICENSE](LICENSE) and [COPYING](COPYING) for full text.

---

## 💬 Support & Feedback

- **Report issues:** [GitHub Issues](../../issues)
- **Suggest improvements:** [GitHub Discussions](../../discussions) (enable in repo)
- **Original project:** [keeferrourke/capitaine-cursors](https://github.com/keeferrourke/capitaine-cursors)

---

## 🔗 Related Projects

- [**Capitaine Cursors**](https://github.com/keeferrourke/capitaine-cursors) — Original X11/Linux cursor theme
- [**KDE Breeze**](https://github.com/KDE/breeze) — Icon design foundation
- [**La Capitaine Icons**](https://github.com/keeferrourke/la-capitaine-icon-theme) — Companion icon theme

---

## ☕ Buy Me a Coffee

If you find this cursor theme useful and want to support its development:

**[Donate via PayPal](https://www.paypal.com/donate/?hosted_button_id=2QYLT6G8RJMNY)**

*Your support helps maintain and improve this project. Thank you!*

---

## ✨ Get Started Today

No more blurry cursors. No more pixelation. Just sharp, professional-looking cursors at any display scale.

[**📥 Download Latest Release**](../../releases/latest)
- **[Buy Me a Coffee](https://buymeacoffee.com)** — One-time or recurring
- **[PayPal](https://www.paypal.com)** — Direct payment option
- **[GitHub Sponsors](https://github.com/sponsors)** — Support directly on GitHub
- **[Patreon](https://www.patreon.com)** — Monthly recurring support

