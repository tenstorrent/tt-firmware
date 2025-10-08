# tt-firmware

## Official Repository
[https://github.com/tenstorrent/tt-firmware](https://github.com/tenstorrent/tt-firmware)

## What is this Firmware?

On Tenstorrent devices we have a system management processor.
This processor is responsible for
    - Turning the hardware on
    - Making sure that external i/o (pcie, eth, dram, etc.) can connect and remain connected while the board is recieving power
    - Ensuring that we never exceed the power or temperature envolope that the card and chip were designed to operate in
And the firmware code encapsulates this functionality

## Why is this a binary release

Tenstorrent products contain IP from third parties, we have agreements with these third parties which keeps us from distributing source code related to their property.
Therefore releasing the fw source code, in its current form, would require disentangling what we have ownership of vs. what is shared. Effectively requiring us to rewrite it to isolate anything proprietary, so we made the decision to spend the resources to
guarantee to make what we can of future fw open-source rather than going back to rewrite what we already have.

If you are interested in the extent that applications interact with this firmware, see [UMD](https://github.com/tenstorrent/tt-umd).

## Available Firmware

| Firmware | Description |
| --- | --- |
| [`fw_pack-18.12.0.fwbundle`](fw_pack-18.12.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

These release notes are also published in HTML at the URL below.

https://docs.tenstorrent.com/tt-zephyr-platforms/release/release-notes-18.12.html

## Major Highlights

- **Enhanced Power Management**: New MRISC PHY powerdown/wakeup support and power command capabilities
- **Improved SMBus Reliability**: Enhanced error detection, logging, and robustness for CM2DM operations
- **Advanced Developer Tooling**: New stack dump utilities and improved console tooling
- **Zephyr v4.3.0 Alignment**: Updated to latest Zephyr pre-release for better upstream compatibility
- **Streamlined Board Support**: Focused support on production devices

## New Features

### Power Management
- **lib: bh_arc**: Added support for MRISC PHY powerdown/wakeup operations
- **lib: bh_arc**: Implemented new Power command functionality
- **boards: tt_blackhole**: Enabled AICLK PPM in firmware table for Galaxy boards
- **boards: tenstorrent**: Applied more conservative TDP limits for P300 boards

### Communication & Protocols
- **app: dmc**: Added support for SMBus block process call (pcall) operations
- **drivers: smbus: stm32**: Enhanced with block read capabilities
- **app: smc**: Added overlay configuration to build DMFW with I2C shell enabled

### Developer & Debug Tools
- **scripts**: New `dump_smc_stack.py` utility for on-demand SMC state analysis
- **scripts: tooling**: Enhanced `tt-console` with PCIe rescan skip option for smooth TT-KMD transitions (2.3.0 to 2.4.1)
- **scripts**: Updated `blackhole_recovery` with improved status messaging and increased delays

## Stability & Robustness Improvements

### Communication Reliability
- **CM2DM Protocol**: Enhanced robustness with detection of duplicate SMBus messages and improved error handling
- **lib: tenstorrent: bh_arc**: Improved error logging in SPI EEPROM operations

### System Reliability
- **app: dmc**: Implemented fine-grained DMC events, replacing the previous single "wakeup" flag approach
- **regulators**: Fixed Galaxy SerDes programming regression
- **boards: tenstorrent**: Reduced P300 I2C clock speeds to minimize packet errors
- **lib: bh_chip**: Optimized I2C gate handling during BH ARC reset operations

### Infrastructure
- **CI/CD**: Migrated to centralized Docker containers hosted at `ghcr.io/tenstorrent`
- **scripts: tooling**: Reworked logging macros with new rate-limited variants

### Wormhole Updates
- **blobs**: Updated Wormhole firmware blob
  - CMFW 2.36.0.0
    - Attempt to enter A3 state on both chips of n300 before triggering
      reset
    - Fix VR addresses for Nebula CB P0V8_GDDR_VDD and P1V35_MVDDQ
    - Update Nebula CB SPI parameters
      - Disable DRAM training at boot
      - Voltage margin = 0
      - P0V8_GDDR_VDD override to 850 mV
      - P1V35_MVDDQ override to 1.35 V
      - Enable additional DRAM training parameters
  - ERISC 6.7.1.0
    - Enable partial response phase detector mode to compensate jitter lanes
    - Initial support for per asic resetting in WH Galaxy

## API Changes

### Breaking Changes
- **lib: bh_arc**: Renamed `msg_type` to `tt_smc_msg`
  - Header file changed from `tenstorrent/msg_type.h` to `tenstorrent/smc_msg.h`
  - **Migration Required**: Update include statements in existing code

### Platform Updates
- **zephyr: patches**: Added patch for SPI-NOR erase-block-size property support

## Zephyr Integration

### Version Update
- **manifest**: Updated to Zephyr v4.3.0-pre
  - Snapshot from Zephyr mainline prior to v4.3.0 feature freeze (October 24th)
  - Minimized in-tree patches through active upstream contribution

### Upstream Contributions
- Enhanced PWM API test suite with cleaner platform-specific conditionals
- Fixed I2C DesignWare target implementation
- Improved SMBus STM32 driver with proper block write byte count handling
- Added IRQ lock protection for CTF tracing timestamp generation
- Extended interrupt controller support for multiple DesignWare instances
- Implemented "safe" API variants for `k_event_wait()` in kernel events

## Documentation Improvements

### Enhanced Documentation
- **lib: bh_arc**: Comprehensive Doxygen documentation for host-to-SMC message types
- **doxygen**: Added supported boards reference links
- **doc**: New contribution and coding guidelines
- **docs**: Added CI job status visualization on project landing page

### Developer Guidance
- **doc**: Added code update workflow snippet: `west patch clean; west update; west patch apply`
- **lib: bh_arc**: Documented unused commands for better API clarity
- **doc**: Improved version handling using project settings from `conf.py`

## Board Support Changes

### Removed Support
- **Removed P100 (Scrappy) Support**:
  - P100 was an internal engineering unit used during initial bringup and testing
  - Support removed to focus resources on consumer-facing devices
  - **Migration Impact**: P100 users must transition to supported production boards

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.11.0 release can be found in [v18.12 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.12.md).

## Full ChangeLog

The full ChangeLog from the previous v18.11.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.11.0...v18.12.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
