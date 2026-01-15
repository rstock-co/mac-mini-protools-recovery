# Mac Mini Pro Tools Recovery

Tech support project - system recovery and software reinstall.

## System Specs

| Component | Details |
|-----------|---------|
| Machine | Mac Mini 2018 |
| CPU | 3.2 GHz 6-core Intel i7 |
| RAM | 32 GB DDR4 |
| Target OS | macOS Ventura 13.7.8 |
| Target Software | Pro Tools Ultimate 2024.10.3 |

## Problem

Computer is failing and needs complete reinstall from scratch.

## Tasks

### Phase 1: Create Bootable USB
- [ ] Obtain 16GB+ USB drive
- [ ] Download macOS Ventura 13.7.8 installer on a working Mac
- [ ] Create bootable installer using `createinstallmedia`

#### Terminal Commands (run on working Mac)

**Step 1: Download macOS Ventura 13.7.8**
```bash
softwareupdate --fetch-full-installer --full-installer-version 13.7.8
```

**Step 2: Create bootable USB** (replace "YourUSBDrive" with your USB drive name)
```bash
sudo /Applications/Install\ macOS\ Ventura.app/Contents/Resources/createinstallmedia --volume /Volumes/YourUSBDrive
```

**To find your USB drive name:**
```bash
ls /Volumes/
```

### Phase 2: Reinstall macOS
- [ ] Boot from USB (hold Option key at startup)
- [ ] Erase internal drive (APFS format) using Disk Utility
- [ ] Install macOS Ventura
- [ ] Complete initial setup

### Phase 3: Mount & Verify External Hard Drives
- [ ] Mount WD My Passport for Mac (PRIORITY)
- [ ] Mount Monster Digital Overdrive
- [ ] Mount G-Technology G-Drive Mini (requires FireWire adapter)
- [ ] Verify all data is accessible

### Phase 4: Install Pro Tools Ultimate (Separate - Requires Hardware)
- [ ] Download Pro Tools 2024.10.3 from Avid account (see download details below)
- [ ] Download HD Driver 2024.10.3 if using Avid hardware
- [ ] Install Pro Tools
- [ ] Authorize with iLok
- [ ] Verify audio interface compatibility
- [ ] Test basic session playback

## External Hard Drives

| Priority | Drive | Capacity | Serial/Model | Connection |
|----------|-------|----------|--------------|------------|
| **1st** | **WD My Passport for Mac** | — | WX21A63V5483 | USB |
| 2nd | Monster Digital Overdrive | 240 GB | ODT3246 | USB |
| 3rd | G-Technology G-Drive Mini | 1 TB | 0G0256 / GDRNU3PA1001BDB | FireWire 800 |

### G-Drive Mini Adapter Requirements

The G-Drive Mini uses FireWire 800 (square ports). The 2018 Mac Mini needs:
- Thunderbolt 3 (USB-C) to Thunderbolt 2 Adapter (~$29)
- Thunderbolt 2 to FireWire 800 Adapter (~$29)

Or check if the G-Drive has a USB port as well.

## Accounts

| Service | Email |
|---------|-------|
| Avid | bluestone.jfamily@gmail.com |

### iLok Authorization

**Using: Physical iLok USB dongle** (not iLok Cloud)

- Dongle holds the Pro Tools license
- Must be plugged in before launching Pro Tools
- No internet required for authorization

### Avid Download Process

**Direct Download Link:** https://my.avid.com/esd/Product/Download/2965

1. Go to the link above (or https://my.avid.com/esd)
2. Login with username/email and password
3. Download the Mac installer

### Pro Tools 2024.10.3 Download Details

| File | Size | MD5 Checksum |
|------|------|--------------|
| **Pro Tools 2024.10.3 (Mac)** | 6,276,483,035 bytes (~6.3 GB) | `d79b6e22726ff5b27ad691a43f011b95` |
| HD Driver 2024.10.3 (Mac) | 567,584,060 bytes (~568 MB) | `521c6913c78b97ec511e8a0e16255c30` |

**Release Date:** July 8th, 2025

**Why 2024.10.3?** This is the last Pro Tools version that supports Mac Mini 2018 (Macmini8,1). Pro Tools 2025.6+ dropped support for this hardware.

## Notes

- 2018 Mac Mini is Intel-based (not Apple Silicon) - straightforward macOS install
- Pro Tools Ultimate requires iLok authorization
- Using **Ventura 13.7.8** (not Sonoma) because Carbon has AVB issues on Sonoma (see compatibility.md)
- Using **Pro Tools 2024.10.3** (not 2025.6.1) because 2018 Mac Mini support was dropped in 2025.x
- WD My Passport is the priority drive for Phase 3

## Resources

- [Avid Pro Tools Downloads](https://www.avid.com/pro-tools/pro-tools-downloads)
- [Apple: Create bootable installer](https://support.apple.com/en-us/HT201372)
- [Pro Tools System Requirements](https://avid.secure.force.com/pkb/articles/compatibility/Pro-Tools-System-Requirements)
- [Pro Tools Carbon Requirements](https://kb.avid.com/pkb/articles/compatibility/Carbon-Requirements)
