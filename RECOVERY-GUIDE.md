# Mac Mini 2018 Recovery Guide

Step-by-step instructions for complete system recovery.

---

## What You'll Need

- 16GB+ USB flash drive (will be erased)
- A working Mac to create the installer
- Internet connection
- Avid account credentials (for Phase 4)
- iLok account and hardware (for Phase 4)
- FireWire 800 adapters for G-Drive Mini (Phase 3)

---

## Phase 1: Create Bootable USB Installer

**On a working Mac:**

1. Open the App Store and search for "macOS Sequoia"
2. Click **Get** to download (do not install when prompted)
3. Insert your 16GB+ USB drive
4. Open **Terminal** (Applications → Utilities → Terminal)
5. Run this command:
   ```bash
   sudo /Applications/Install\ macOS\ Sequoia.app/Contents/Resources/createinstallmedia --volume /Volumes/YOUR_USB_NAME
   ```
   *(Replace YOUR_USB_NAME with your USB drive's actual name)*
6. Enter your admin password when prompted
7. Type `Y` and press Enter to confirm erasing the drive
8. Wait 20-30 minutes for completion
9. Terminal will say "Install media now available" when done

---

## Phase 2: Reinstall macOS on the Mac Mini

1. **Shut down** the Mac Mini completely
2. Insert the bootable USB drive
3. **Power on while holding the Option (⌥) key**
4. Release when you see the boot menu
5. Select the orange USB installer drive (usually called "Install macOS Sequoia")
6. Wait for Recovery to load

### Erase the Internal Drive

7. From the macOS Utilities window, open **Disk Utility**
8. Click **View → Show All Devices**
9. Select the top-level internal drive (not a sub-volume)
10. Click **Erase** with these settings:
    - **Name:** `Macintosh HD`
    - **Format:** `APFS`
    - **Scheme:** `GUID Partition Map`
11. Click **Erase** and wait for completion
12. Close Disk Utility

### Install macOS

13. Select **Install macOS Sequoia**
14. Click **Continue** and agree to terms
15. Select "Macintosh HD" as the destination
16. Wait 30-60 minutes for installation (Mac will restart several times)
17. Complete the initial setup wizard:
    - Language & region
    - Apple ID sign-in (or skip)
    - Create user account
    - Privacy settings

---

## Phase 3: Mount & Verify External Hard Drives

**Priority Order:**
1. WD My Passport for Mac (PRIORITY)
2. Monster Digital Overdrive
3. G-Technology G-Drive Mini

---

### Drive 1: WD My Passport for Mac (PRIORITY)

| Detail | Value |
|--------|-------|
| Serial | WX21A63V5483 |
| Connection | USB |

**Steps:**

1. Connect the drive via USB directly to the Mac Mini (not through a hub)
2. Wait 10-15 seconds for it to appear on Desktop or Finder sidebar
3. If it appears, double-click to verify contents are accessible
4. **If NOT visible:**
   - Open **Disk Utility** (Applications → Utilities)
   - Click **View → Show All Devices**
   - Look for the drive in the left sidebar
   - If visible but grayed out, select it and click **Mount**
   - If mount fails, click **First Aid** to attempt repair

**Record results:** ☐ Mounted successfully ☐ Needed repair ☐ Failed

---

### Drive 2: Monster Digital Overdrive

| Detail | Value |
|--------|-------|
| Capacity | 240 GB |
| Serial | ODT3246 |
| Connection | USB |

**Steps:** Same as Drive 1

**Record results:** ☐ Mounted successfully ☐ Needed repair ☐ Failed

---

### Drive 3: G-Technology G-Drive Mini

| Detail | Value |
|--------|-------|
| Capacity | 1 TB |
| Model | 0G0256 / GDRNU3PA1001BDB |
| Connection | FireWire 800 |
| Age | ~15 years |

**⚠️ This drive requires adapters:**

The square ports on the back are FireWire 800. The 2018 Mac Mini doesn't have FireWire, so you need:

1. **Apple Thunderbolt 3 (USB-C) to Thunderbolt 2 Adapter** (~$29)
   https://www.apple.com/shop/product/MMEL2AM/A/

2. **Apple Thunderbolt to FireWire Adapter** (~$29)
   https://www.apple.com/shop/product/MD464LL/A/

Chain: Mac Mini USB-C → TB3-to-TB2 Adapter → TB2-to-FW800 Adapter → G-Drive

**Alternative:** Check if the G-Drive has a USB port on it (some models had both).

**Steps:** Once adapters are connected, same mounting process as Drive 1

**Special notes for 15-year-old drive:**
- Listen for clicking or grinding sounds (signs of mechanical failure)
- If drive spins but won't mount, may need data recovery software
- Consider backing up contents immediately once mounted

**Record results:** ☐ Mounted successfully ☐ Needed repair ☐ Failed ☐ Needs adapters

---

## Phase 3 Troubleshooting

| Problem | Solution |
|---------|----------|
| Drive not showing at all | Try different USB port, try different cable |
| "Disk not readable" popup | Click "Ignore", then try First Aid in Disk Utility |
| Drive visible but won't mount | Run First Aid, may need data recovery tools |
| Very slow to mount | Normal for older drives, wait several minutes |
| Clicking sounds | Stop immediately - sign of mechanical failure |

---

## Phase 4: Install Pro Tools Ultimate 2025.6.1

*(To be completed separately - requires iLok hardware)*

1. Download iLok License Manager from https://www.ilok.com
2. Install and sign in to your iLok account
3. Connect iLok USB key or activate cloud session
4. Go to https://www.avid.com/pro-tools/pro-tools-downloads
5. Sign in to Avid account
6. Download Pro Tools Ultimate 2025.6.1
7. Run the installer
8. Restart when prompted
9. Launch Pro Tools and authorize via iLok
10. Configure audio interface in Setup → Playback Engine
11. Test with a session

---

## Progress Checklist

- [ ] Phase 1: Bootable USB created
- [ ] Phase 2: macOS Sequoia installed
- [ ] Phase 3: WD My Passport mounted
- [ ] Phase 3: Monster Digital mounted
- [ ] Phase 3: G-Drive Mini mounted (or adapters ordered)
- [ ] Phase 4: Pro Tools installed (separate task)
