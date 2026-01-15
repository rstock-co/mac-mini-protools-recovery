# Mac Mini Pro Tools Recovery

**YOU ARE RUNNING DIRECTLY ON THIS MAC MINI.** You can execute macOS commands via Terminal to help with recovery tasks.

## This Machine

| Component | Details |
|-----------|---------|
| Machine | Mac Mini 2018 (Macmini8,1) |
| CPU | 3.2 GHz 6-core Intel i7 (x64 architecture) |
| RAM | 32 GB DDR4 |
| OS | macOS Ventura 13.7.8 |
| Target Software | Pro Tools Ultimate 2024.10.3 |

## Current Status

**CURRENT PHASE: Phase 3 - External Hard Drive Restoration**

We are trying to recover data from external hard drives with corrupted/missing partition tables.

### Progress Summary
- Phase 1: Create Bootable USB ✅ COMPLETE
- Phase 2: Reinstall macOS ✅ COMPLETE
- **Phase 3: Drive Restoration** ⬅️ IN PROGRESS
- Phase 4: Install Pro Tools (pending)

---

## Phase 3: External Hard Drives

### Drives to Recover

| Priority | Drive | Capacity | Connection | Status |
|----------|-------|----------|------------|--------|
| **1st** | **WD My Passport for Mac** | 1 TB | USB | **Uninitialized - no partition table** |
| 2nd | Monster Digital Overdrive | 240 GB | USB | Not yet tested |
| 3rd | G-Technology G-Drive Mini | 1 TB | FireWire 800 | Needs adapters |

### WD My Passport - Current Issue

**See `wd-my-passport-restoration.md` for full troubleshooting log.**

**Summary:**
- Drive detected as `/dev/disk2` (1 TB, external, physical)
- Shows "Uninitialized" in Disk Utility
- Partition map: "Not Supported"
- `diskutil list` shows NO partitions - just raw disk
- First Aid ran successfully but didn't fix it
- **Likely cause:** Partition table corrupted/missing, but data may still exist on disk

**Next step:** Install TestDisk to scan for lost partitions and attempt recovery.

### Useful Commands

**List all disks:**
```bash
diskutil list
```

**Get detailed disk info:**
```bash
diskutil info /dev/disk2
```

**Check for data on raw disk (sample read):**
```bash
sudo dd if=/dev/disk2 bs=1M count=10 skip=1 2>/dev/null | strings | head -50
```

**Install Homebrew (if needed):**
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**Install TestDisk via Homebrew:**
```bash
brew install testdisk
```

**Run TestDisk:**
```bash
sudo testdisk
```

---

## Phase 4: Pro Tools Installation (Future)

See `pro-tools-setup-guide.md` and `pro-tools-setup-guide.pdf` for detailed instructions.

| File | Size | MD5 Checksum |
|------|------|--------------|
| Pro Tools 2024.10.3 (Mac) | ~6.3 GB | `d79b6e22726ff5b27ad691a43f011b95` |
| HD Driver 2024.10.3 (Mac) | ~568 MB | `521c6913c78b97ec511e8a0e16255c30` |

**Download:** https://my.avid.com/esd/Product/Download/2965

**Why 2024.10.3?** Last version supporting Mac Mini 2018. Pro Tools 2025.6+ dropped support.

### Accounts

| Service | Email |
|---------|-------|
| Avid | bluestone.jfamily@gmail.com |

### iLok Authorization

Using **physical iLok USB dongle** (not iLok Cloud):
- Dongle holds the Pro Tools license
- Must be plugged in before launching Pro Tools

---

## G-Drive Mini Adapter Requirements

The G-Drive Mini uses FireWire 800. This Mac needs:
- Thunderbolt 3 (USB-C) to Thunderbolt 2 Adapter (~$29)
- Thunderbolt 2 to FireWire 800 Adapter (~$29)

---

## Important Notes

- This is an Intel Mac (x64) - NOT Apple Silicon
- DNS was manually set to 8.8.8.8 / 1.1.1.1 (was broken initially)
- Node.js and Claude Code have been installed on this machine
- Always update `wd-my-passport-restoration.md` when troubleshooting the WD drive

## Resources

- [Avid Pro Tools Downloads](https://www.avid.com/pro-tools/pro-tools-downloads)
- [Pro Tools System Requirements](https://avid.secure.force.com/pkb/articles/compatibility/Pro-Tools-System-Requirements)
- [TestDisk Documentation](https://www.cgsecurity.org/wiki/TestDisk)
