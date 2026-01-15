# WD My Passport Recovery Attempt - Email Draft

---

**Subject:** WD My Passport Drive - Recovery Attempt Update

---

Hi Jason,

I wanted to update you on the WD My Passport drive recovery attempt. When we connected the drive to the Mac Mini, it was detected by the system but showed as "Uninitialized" with no readable partition table. This typically means the drive's file system structure was corrupted or lost, but the actual data often remains intact on the disk and can be recovered with the right tools.

We installed TestDisk, a professional-grade data recovery utility, and attempted to scan the drive for lost partitions. Unfortunately, when the scan started, we encountered persistent "Input/Output errors" — the drive simply wouldn't respond to read requests. We tried multiple USB ports, unplugged and reconnected the drive several times, and verified that the Mac was detecting the hardware correctly. The drive shows up and even reports a healthy status, but every attempt to actually read data from it fails at the hardware level.

Based on our diagnostics, the issue appears to be with the drive's internal USB controller (the electronics that translate between USB and the actual disk), rather than the disk platters themselves. The drive is drawing nearly the maximum power allowed over USB (896mA out of 900mA available), which could be contributing to the problem. The good news is that your actual data is likely still intact on the physical disk — we just can't access it through the drive's built-in electronics.

Here are the options going forward:

- **Try a powered USB hub** ($20-40) — This would provide more stable power and might allow the drive to function properly.
- **Extract the internal drive** ($15-25 for a SATA adapter) — If this is an older WD model, we may be able to remove the drive from its enclosure and connect it directly using a standard SATA-to-USB adapter, bypassing the failing USB controller entirely.
- **Professional data recovery service** ($300-1500+) — If the above options don't work, a professional service can open the drive in a clean room and read the platters directly. This is the most reliable option for critical data.

Let me know how you'd like to proceed, and whether the data on this drive is worth pursuing one of these options.
