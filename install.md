# Mac Mini Pro Tools Installation Guide

Complete step-by-step instructions for reinstalling macOS and Pro Tools.

---

## ✅ Confirmed Configuration

| Component | Version |
|-----------|---------|
| macOS | **Ventura 13.7.8** |
| Pro Tools | **2024.10.3** |
| Hardware | **Mac Mini 2018** |
| Audio Interface | **Avid Carbon** |

---

## What You Need

- [ ] Working Mac (to create the installer)
- [ ] 16GB+ USB drive (will be erased)
- [ ] Internet connection
- [ ] Avid account login (bluestone.jfamily@gmail.com)
- [ ] **Physical iLok USB dongle** (has Pro Tools license on it)

---

## Phase 1: Download Everything (On Working Mac)

### Step 1: Download macOS Ventura 13.7.8

Open Terminal and run:
```bash
softwareupdate --fetch-full-installer --full-installer-version 13.7.8
```
⏱️ ~12GB download, may take 30-60 minutes

### Step 2: Download Pro Tools 2024.10.3

1. Go to: https://my.avid.com/esd/Product/Download/2965
2. Log in with Avid account
3. Download **Pro Tools 2024.10.3 (Mac)** (~6.3 GB)
4. Download **HD Driver 2024.10.3 (Mac)** (~568 MB) — needed for Carbon

### Step 3: Save Pro Tools Installers

Copy the downloaded Pro Tools files to an external drive (WD My Passport) so you can access them after macOS is installed.

---

## Phase 2: Create Bootable USB (On Working Mac)

### Step 4: Plug in USB Drive

Insert your 16GB+ USB drive.

### Step 5: Find USB Drive Name

```bash
ls /Volumes/
```
Note the name of your USB drive (e.g., "Untitled" or "USB Drive").

### Step 6: Create Bootable Installer

Replace `YourUSBDrive` with your actual USB drive name:
```bash
sudo /Applications/Install\ macOS\ Ventura.app/Contents/Resources/createinstallmedia --volume /Volumes/YourUSBDrive
```

- Enter your Mac password when prompted
- Type `Y` and press Enter to confirm erasing the USB
- ⏱️ Wait ~20-30 minutes

When complete, you'll see: "Install media now available"

---

## Phase 3: Install macOS (On Mac Mini)

### Step 7: Boot from USB

1. Plug the bootable USB into the Mac Mini
2. Power on the Mac Mini
3. **Immediately hold the Option (⌥) key**
4. Keep holding until you see the boot menu
5. Select **"Install macOS Ventura"** and press Enter

### Step 8: Erase Internal Drive

1. From macOS Utilities, select **Disk Utility**
2. Click **View** → **Show All Devices**
3. Select the internal drive (top-level, e.g., "APPLE SSD")
4. Click **Erase**
   - Name: `Macintosh HD`
   - Format: `APFS`
   - Scheme: `GUID Partition Map`
5. Click **Erase**, then **Done**
6. Quit Disk Utility (Cmd+Q)

### Step 9: Install macOS

1. Select **Install macOS Ventura**
2. Click **Continue**
3. Agree to terms
4. Select `Macintosh HD` as destination
5. Click **Install**
6. ⏱️ Wait ~30-45 minutes (Mac will restart several times)

### Step 10: Complete Initial Setup

1. Select country/region
2. Set up keyboard, Wi-Fi
3. Skip migration assistant (set up as new Mac)
4. Create user account
5. Complete remaining setup steps

---

## Phase 4: Mount External Drives

### Step 11: Connect External Drives

1. Connect **WD My Passport for Mac** (USB) — has your Pro Tools installer
2. Connect **Monster Digital Overdrive** (USB) if needed
3. Connect **G-Technology G-Drive Mini** (requires FireWire adapter) if needed

### Step 12: Verify Drives Mount

All drives should appear on Desktop or in Finder sidebar. If not:
1. Open **Disk Utility**
2. Select the drive
3. Click **Mount**

---

## Phase 5: Install Pro Tools

### Step 13: Install Pro Tools 2024.10.3

1. Open the Pro Tools installer from your external drive
2. Double-click **Install Pro Tools 2024.10.3.dmg**
3. Run the installer
4. Follow installation prompts
5. Restart when prompted

### Step 14: Install HD Driver

1. Open **HD Driver 2024.10.3.dmg**
2. Run the installer
3. Restart when prompted

### Step 15: Authorize Pro Tools

1. **Plug in the physical iLok USB dongle** before launching Pro Tools
2. Launch Pro Tools
3. Pro Tools will detect the license on the dongle automatically
4. If prompted, sign in to iLok License Manager to verify

**Note:** The iLok dongle holds the license. No internet required for authorization once the dongle is connected. Just plug it in before launching Pro Tools.

---

## Phase 6: Set Up Carbon

### Step 16: Download Carbon Central

1. Go to: https://www.avid.com/products/pro-tools-carbon/learn-and-support
2. Download **Carbon Central 25.1** (or latest)
3. Install and restart if prompted

### Step 17: Connect Carbon

1. Connect Carbon to Mac via Ethernet/AVB
2. Open Carbon Central
3. Follow setup prompts to configure audio interface

### Step 18: Configure Pro Tools

1. Open Pro Tools
2. Go to **Setup** → **Playback Engine**
3. Select **Pro Tools Carbon** as playback engine
4. Set buffer size as needed

---

## Phase 7: Test

### Step 19: Verify Everything Works

- [ ] Pro Tools launches without errors
- [ ] Carbon appears in Playback Engine options
- [ ] Audio plays back correctly
- [ ] Can record audio through Carbon inputs
- [ ] External drives accessible for session files

---

## Quick Reference

### Downloads

| Item | Link |
|------|------|
| Pro Tools 2024.10.3 | https://my.avid.com/esd/Product/Download/2965 |
| Carbon Central | https://www.avid.com/products/pro-tools-carbon/learn-and-support |

### Pro Tools 2024.10.3 Checksums

| File | MD5 |
|------|-----|
| Pro Tools 2024.10.3 (Mac) | `d79b6e22726ff5b27ad691a43f011b95` |
| HD Driver 2024.10.3 (Mac) | `521c6913c78b97ec511e8a0e16255c30` |

### Terminal Commands

```bash
# Download macOS
softwareupdate --fetch-full-installer --full-installer-version 13.7.8

# List volumes (to find USB name)
ls /Volumes/

# Create bootable USB (replace YourUSBDrive)
sudo /Applications/Install\ macOS\ Ventura.app/Contents/Resources/createinstallmedia --volume /Volumes/YourUSBDrive
```

---

## Troubleshooting

**USB not booting?**
- Make sure you're holding Option key immediately at power-on
- Try a different USB port

**Drive not mounting?**
- Open Disk Utility → Select drive → Click Mount
- If greyed out, drive may need repair: First Aid

**Pro Tools authorization issues?**
- Make sure **iLok USB dongle is plugged in** before launching Pro Tools
- Try a different USB port
- Download iLok License Manager: https://www.ilok.com/#!license-manager
- Open iLok License Manager to verify the license is on the dongle
- If license isn't showing, sign in at https://www.ilok.com to check account

**Carbon not showing up?**
- Ensure Carbon Central is installed
- Check Ethernet/AVB connection
- Restart Carbon and Mac

---

*Last updated: January 2026*
