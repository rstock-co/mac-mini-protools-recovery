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

## Phase 3: Data Recovery Attempt (2026-01-15)

**Goal:** Use recovery software to scan raw disk for lost partitions or files.

### Step 1: Install Homebrew
- [x] Ran Homebrew installer in Terminal
- [x] Installation successful

### Step 2: Install TestDisk
- [x] Ran: `/usr/local/bin/brew install testdisk`
- [x] TestDisk 7.2 installed successfully

### Step 3: Run TestDisk
- [x] Ran: `sudo /usr/local/bin/testdisk`
- [x] Selected /dev/disk2 (1 TB WD My Passport)
- [x] Selected EFI GPT partition table type
- [x] Selected Analyse → Quick Search
- [ ] **PROBLEM:** TestDisk froze during scan - 0% CPU usage

### Step 4: Direct disk read test
- [x] Ran: `sudo dd if=/dev/disk2 bs=512 count=1`
- [x] **RESULT:** `dd: /dev/disk2: Input/output error`
- [x] Multiple attempts - all failed with I/O error

### Step 5: Hardware diagnostics
- [x] Checked USB power: 896mA required vs 900mA available (marginal)
- [x] Checked SMART: Reports "Verified" (healthy)
- [x] Tried different USB port: Same I/O error
- [x] Tried unplugging/replugging: Same I/O error

**Findings:**

| Test | Result |
|------|--------|
| USB Detection | Works - drive enumerated correctly |
| SMART Status | Verified (reports healthy) |
| Partition Map | Unknown/Missing |
| Read Any Data | **FAILS - I/O Error** |
| Power Draw | 896mA (near 900mA limit) |

**Diagnosis:** Hardware failure - likely the USB-SATA bridge inside the WD enclosure is failing. The drive platters may be intact, but the enclosure electronics cannot read them.

**Outcome:** Cannot proceed with software recovery due to hardware I/O errors.

---

## Phase 4: Hardware Recovery Options (TBD)

The drive has a hardware-level failure preventing any data reads. Software tools cannot help until the hardware issue is resolved.

**Options:**

| Option | Cost | Difficulty | Notes |
|--------|------|------------|-------|
| Try powered USB hub | $20-40 | Easy | Rules out power issues |
| Try different USB cable | $10-15 | Easy | Requires WD proprietary Micro-B 3.0 connector |
| Extract drive from enclosure | $15-25 | Medium | Requires SATA-to-USB adapter; may not work on newer WD models (USB soldered to drive) |
| Professional data recovery | $300-1500+ | N/A | Last resort; they can read platters directly |

**Next step:** Determine drive age/model to assess if internal drive extraction is possible.

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
