# Mac Mini Pro Tools Recovery

Tech support project - system recovery and software reinstall.

## System Specs

| Component | Details |
|-----------|---------|
| Machine | Mac Mini 2018 |
| CPU | 3.2 GHz 6-core Intel i7 |
| RAM | 32 GB DDR4 |
| Target OS | macOS Ventura 13.x |
| Target Software | Pro Tools Ultimate 2024.10.3 |

## Problem

Computer is failing and needs complete reinstall from scratch.

## Tasks

### Phase 1: Create Bootable USB
- [x] Obtain 16GB+ USB drive
- [x] Download macOS Ventura installer on a working Mac
- [x] Create bootable installer using `createinstallmedia`

### Phase 2: Reinstall macOS
- [x] Boot from USB (hold Option key)
- [x] Erase internal drive (APFS format)
- [x] Install macOS Ventura
- [x] Complete initial setup

### Phase 3: Install Pro Tools Ultimate
- [ ] Download Pro Tools 2024.10.3 from Avid account
- [ ] Install Pro Tools
- [ ] Authorize with iLok
- [ ] Verify audio interface compatibility
- [ ] Test basic session playback

### Phase 4: Additional Setup (TBD)
- [ ] (User will provide more requirements)

## Notes

- 2018 Mac Mini is Intel-based (not Apple Silicon) - straightforward macOS install
- Pro Tools Ultimate requires iLok authorization
- Pro Tools 2024.10.3 compatible with macOS Ventura
- See `pro-tools-setup-guide.md` for detailed installation instructions

## Resources

- [Avid Pro Tools Downloads](https://www.avid.com/pro-tools/pro-tools-downloads)
- [Apple: Create bootable installer](https://support.apple.com/en-us/HT201372)
- [Pro Tools System Requirements](https://avid.secure.force.com/pkb/articles/compatibility/Pro-Tools-System-Requirements)
