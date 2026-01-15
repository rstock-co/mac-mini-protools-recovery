# WD My Passport Restoration Log

Troubleshooting log for recovering data from WD My Passport for Mac.

## Drive Info

| Property | Value |
|----------|-------|
| Drive | WD My Passport for Mac |
| Serial | WX21A63V5483 |
| Connection | USB |
| Target Mac | Mac Mini 2018 |
| Target OS | macOS Ventura 13.7.8 |

---

## Symptom

"The disk you attached was not readable by this computer" warning popup on connection.

---

## Phase 1: Initial Diagnostics (2026-01-15)

**Goal:** Determine drive format and current state in Disk Utility.

### Step 1: Dismiss the popup
- [x] Click **"Ignore"** on the popup

### Step 2: Open Disk Utility
- [x] Click Spotlight icon (magnifying glass, top right of screen)
- [x] Type "Disk Utility" and press Enter

### Step 3: Locate the drive
- [x] Look in the left sidebar for "WD My Passport" or a disk size (e.g., "500 GB")
- [x] Click on the drive to select it

### Step 4: Record findings
- [x] Note what shows for "Format" or "Type"
- [x] Check if "Mount" button is available at the top
- [x] Report findings

**Findings:**
- Drive visible in sidebar: **Yes** - "WD MyPassport 0748 Media" under External
- Capacity: **1 TB**
- Type: **disk**
- Device: **disk2**
- Partition map: **Not Supported** ← Problem identified
- SMART status: **Not Supported**
- Sub-header shows: **"Uninitialized"** ← Partition table missing/corrupted
- Mount button available: N/A (no partition to mount)

**Outcome:** Drive detected but partition map unreadable. Proceed to Phase 2.

---

## Phase 2: First Aid & Terminal Diagnostics (2026-01-15)

**Goal:** Attempt repair and gather detailed disk information.

### Step 1: Check for partitions in Disk Utility
- [x] Look for a disclosure triangle (▶) next to "WD MyPassport 0748 Media"
- [x] No triangle present - no partitions visible
- [x] Sub-header shows "Uninitialized"

### Step 2: Try First Aid
- [x] With the WD drive selected, click **"First Aid"** button (top of Disk Utility)
- [x] Click **"Run"** when prompted
- [x] Wait for it to complete
- [x] Result: **"Operation successful"** - but drive still shows Uninitialized

### Step 3: Get Terminal diagnostics
- [x] Open **Terminal** (Spotlight → type "Terminal" → Enter)
- [x] Run: `diskutil list` and report output

**Terminal Output for disk2:**
```
/dev/disk2 (external, physical):
   #:  TYPE        NAME        SIZE       IDENTIFIER
   0:                          1 TB       disk2
```

**Findings:**
- No partitions visible - only raw disk (entry 0)
- No TYPE, no NAME - partition table is missing/corrupted
- Drive is detected as 1TB physical disk but has no readable filesystem

**Outcome:** Partition table is gone. Need data recovery software to scan raw disk.

---

## Phase 3: Data Recovery Software (TBD)

**Goal:** Use recovery software to scan raw disk for lost partitions or files.

**Recommended Tools:**

| Tool | Cost | Notes |
|------|------|-------|
| **TestDisk** | Free | Can recover lost partitions, restore partition table |
| **PhotoRec** | Free | Recovers files directly (ignores filesystem) |
| Disk Drill | Free tier / Paid | Mac-native, user-friendly |
| R-Studio | Paid | Professional-grade recovery |

**Recommended approach:** Try TestDisk first - it may be able to find and restore the original partition.

### Step 1: Install TestDisk
- [ ] (Instructions TBD)

### Step 2: Scan for lost partitions
- [ ] (Instructions TBD)

**Outcome:** (pending)

---

## Possible Causes Reference

| Cause | Likelihood | Solution |
|-------|------------|----------|
| Corrupted partition table | Medium | Try First Aid, or use `diskutil` in Terminal |
| Encrypted drive | Low | Need original password/recovery key |
| NTFS formatted | Low | Install NTFS driver (Paragon, Mounty, etc.) |
| Physical drive failure | Unknown | Try different USB port/cable |
| Needs repair | Medium | Run First Aid or use data recovery software |

---

## Terminal Commands Reference

**List all disks:**
```bash
diskutil list
```

**Get disk info:**
```bash
diskutil info /dev/diskX
```

**Attempt to mount:**
```bash
diskutil mount /dev/diskXsY
```

**Run repair (First Aid equivalent):**
```bash
diskutil verifyVolume /dev/diskXsY
diskutil repairVolume /dev/diskXsY
```

---

## Resolution

**Status:** Unresolved

**Final Outcome:** (to be updated)

**Data Recovered:** (to be updated)
