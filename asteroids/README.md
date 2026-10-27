# Nothing Phone (3a) (asteroids)

## Source

Vendor UEFI drivers of the Nothing Phone (3a) (SM7635 "Volcano", Qualcomm package `MilosLAA`), firmware
`BOOT.MXF.2.1-01955-LANAI-1.88923.2`. Extracted with [UEFIReader](https://github.com/WOA-Project/UEFIReader) (fc2e9e3)
from `radio/uefi.img` of [NullDebris/proprietary_vendor_nothing_asteroids](https://gitlab.com/NullDebris/proprietary_vendor_nothing_asteroids)
at 7d498e06705f7de4ecbe6fb932ac19ce0995e148. Used by `Platforms/Nothing/asteroidsPkg` of
[rootstockos/uefi-asteroids](https://github.com/rootstockos/uefi-asteroids) (branch `asteroids`).

## Device Patches/Fixes

giulia's patches (same LANAI boot branch), carried over with rootstockos' `transplant-patches.py` (exact byte-context matching). Each range matched
uniquely with the full 48-byte context, no PC-relative masking.

### ClockDxe:

- **Reason:** To keep some important clocks on.
- **Patch:** Removed "DCDDisableDependencies" function call (giulia's patch at offset 0xa814 here).
- **Patch Creator:** [Robotix](https://github.com/Robotix22) (giulia)

### SPMIDxe:

> [!IMPORTANT]
> On giulia it must be paired with the PmicDxe Patch. asteroidsPkg does not load PmicDxe or its consumers (external abort on
> SPMI under Gunyah; see its PORTING.md), so there is no PmicDxe patch here.

- **Reason:** To make UEFI not Crash during UEFI Boot.
- **Patch:** Removed SPMI Handle Function (giulia's patch at offset 0x154c here).
- **Patch Creator:** [Kancy Joe](https://github.com/sunflower2333) (giulia)
