# Installation Guide for Capitaine Cursors (Windows 11 HiDPI)

## Quick Start

1. **Extract** the release ZIP
2. **Right-click** `capitaine-light/install.inf` (or `capitaine-dark/install.inf`)
3. **Select "Install"**
4. Open **Settings** → **Personalization** → **Mouse pointer** → Select **"Capitaine HiDPI"**

Done in under 30 seconds.

---

## Why HiDPI Cursors Matter on Windows 11

### The Problem

Standard cursor files are 32×32 pixels. On Windows 11 with:
- High-resolution displays (4K, ultrawide)
- Display scaling enabled (125%, 150%, 200%, 250%)
- System DPI above default

Windows must artificially scale the cursor image, causing **blurriness and pixelation**.

### The Solution

These cursors contain **7 resolution layers** (32px to 128px) inside each file. Windows 11 automatically uses the exact resolution matching your current display scaling. No scaling needed = sharp, crisp cursors.

**Supported scales:** 100%, 125%, 150%, 200%, 250%, 300%, 400%

---

## Installation Methods

### Method 1: Using install.inf (Recommended)

**Fastest and easiest method.**

1. **Extract** the ZIP archive to any location
2. **Navigate** to `capitaine-light/` or `capitaine-dark/` (depending on preference)
3. **Right-click** `install.inf`
4. **Select "Install"** from the context menu
5. **Open Settings:**
   - Press `Win + I`
   - Go to **Personalization** → **Mouse pointer**
   - Scroll down and select **"Capitaine HiDPI"** from the dropdown
   - Cursor changes immediately
6. ✓ Done. Restart applications if needed.

**What `install.inf` does:**
- Registers the cursor scheme in Windows Registry
- No scripts to run, no administrator prompts
- Windows recognizes the theme automatically

### Method 2: Manual Installation (If install.inf doesn't work)

1. **Extract** the ZIP archive
2. **Open Cursor Schemes folder:**
   - Press `Win + R`
   - Type: `%AppData%\CursorSchemes`
   - Press Enter
3. **Copy the theme folder:**
   - From your extracted archive, copy `capitaine-light` or `capitaine-dark`
   - Paste into the CursorSchemes folder
4. **Apply theme:**
   - Settings → Personalization → Mouse pointer
   - Select **"Capitaine HiDPI"**

---

## Troubleshooting

### Issue: install.inf doesn't appear in right-click menu

**Try this:**
1. Right-click `install.inf`
2. Select **"Open with"**
3. Choose **"IExpress Wizard"** or **"Registry Editor"**
4. If successful, Windows will associate .inf files for future installations

**If that doesn't work:**
- Use Method 2 (Manual Installation) instead

### Issue: Cursors still look blurry after installation

**Check 1: Verify theme is applied**
- Settings → Personalization → Mouse pointer
- Confirm **"Capitaine HiDPI"** is selected
- If not, select it and wait 3 seconds

**Check 2: Refresh cursor cache**
1. Open Settings → Personalization → Mouse pointer
2. Switch to a different cursor theme (e.g., "Default")
3. Wait 5 seconds
4. Switch back to **"Capitaine HiDPI"**
5. This forces Windows to reload the cursor files

**Check 3: Try the other variant**
- Uninstall and try the opposite variant (Light vs Dark)
- Different rendering may appear sharper on your display

**Check 4: Verify display scaling**
- Right-click desktop → **Display settings**
- Note your **Scale** setting
- These cursors support: 100%, 125%, 150%, 200%, 250%, 300%, 400%
- If using unusual scaling (e.g., 175%), the closest resolution layer will be used

### Issue: Theme doesn't appear in Settings list

**Step 1: Verify installation folder**
- Press `Win + R` → `%AppData%\CursorSchemes`
- Check if **"Capitaine HiDPI"** folder exists
- If yes, skip to Step 3
- If no, try installing again

**Step 2: Reinstall**
- Go back to the extracted ZIP
- Right-click `install.inf` again and select **"Install"**

**Step 3: Restart Settings app**
- Close all Settings windows
- Open Settings again
- Go back to Personalization → Mouse pointer
- The theme should now appear

### Issue: Some applications not using the new cursor

**Expected behavior:** Some applications (web browsers, development tools, older software) override the system cursor. This is normal.

**Workaround:**
- Use the application's own cursor settings if available
- Most modern apps respect the Windows cursor theme

---

## Uninstalling

### Method 1: Revert to Default (Recommended)

1. **Settings** → **Personalization** → **Mouse pointer**
2. **Select** a different theme (e.g., "Windows Default")
3. The Capitaine theme is now deactivated

### Method 2: Remove from System

To completely remove the cursor scheme:

1. **Deactivate first** (see Method 1)
2. **Press** `Win + R` → `%AppData%\CursorSchemes`
3. **Delete** the **"Capitaine HiDPI"** folder
4. **Empty** Recycle Bin

---

## Technical Details

### File Structure

Each theme folder contains:

```
capitaine-light/
├── install.inf          # Windows Registry installer
├── arrow.cur            # Static cursor (standard pointer)
├── crosshair.cur        # Crosshair cursor
├── help.cur             # Help cursor
├── link.cur             # Link/hyperlink cursor
├── move.cur             # Move/drag cursor
├── pen.cur              # Drawing/pen cursor
├── size_*.cur           # Resize arrows (8 directions)
├── text.cur             # Text selection cursor
├── unavailable.cur      # Disabled/unavailable cursor
├── up_arrow.cur         # Up arrow cursor
├── wait.ani             # Animated wait/loading cursor
└── working.ani          # Animated working cursor
```

### Layered Cursor Format

Each `.cur` file internally contains 7 resolution layers:

| Scale | Size | Use Case |
|-------|------|----------|
| x1 | 32×32 px | 100% display scaling |
| x1.25 | 40×40 px | 125% display scaling |
| x1.5 | 48×48 px | 150% display scaling |
| x2 | 64×64 px | 200% display scaling |
| x2.5 | 80×80 px | 250% display scaling |
| x3 | 96×96 px | 300% display scaling |
| x4 | 128×128 px | 400% display scaling |

Windows 11 loads the layer matching your current display scaling for perfect clarity.

---

## Compatibility

| OS | Status | Notes |
|---|---|---|
| Windows 11 | ✅ Full support | Optimized; multi-layer cursors fully used |
| Windows 10 | ⚠️ Works | Limited HiDPI support |
| Windows 8.1 | ❌ Untested | May not work |
| Windows 7 | ❌ Incompatible | Older cursor format |

---

## Questions?

- **For issues:** Check Troubleshooting section above
- **Original Capitaine Cursors:** https://github.com/keeferrourke/capitaine-cursors
- **This adaptation:** Report issues on GitHub
