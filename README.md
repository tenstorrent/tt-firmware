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
| [`fw_pack-19.2.0.fwbundle`](fw_pack-19.2.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

These release notes are also published in HTML at the URL below.

https://docs.tenstorrent.com/tt-zephyr-platforms/release/release-notes-19.2.html

Major enhancements with this release include upgrading to Zephyr 4.3.0, delivering configurable PCIe BAR support via the new `CntlInitV2()` flow, and introducing a standalone `tt_fwbundle` tooling suite.

## What's Changed

### Drivers
- **Clock Control Emulation**: Added an emulated clock control driver and bindings used by native-sim tests.
- **DMA Reliability**: Switched the Blackhole DMA driver to RAM-to-Tensix transfers and enforced DT alignment so NOC DMA buffers meet 64-byte requirements.

### Libraries & Firmware
- **Power Management**: Refactored `bh_arc` power handling into `bh_power`, added L2 CPU enable/disable plumbing, and exposed the control through `tt_shell` with stricter error handling.
- **PCIe Enhancements**: Rolled out the `CntlInitV2()` path as a working demo of runtime BAR sizing, consolidating init parameters into a single struct, improving diagnostics, and aligning MSI buffers for predictable bring-up.
- **Firmware Tables**: Populated PCIe BAR size metadata across Blackhole board firmware tables to accompany the new BAR masks.

### Tooling & Tests
- **Firmware Bundle Utility**: Add `tt_fwbundle` script with create and combine commands, which replace
the fwbundle subcommand in `tt_boot_fs`. Remove this subcommand and update usage in tree to use `tt_fwbundle`.
- **Automated Coverage**: Added unit tests for the new firmware bundle flows and expanded native-sim PCIe MSI coverage.

### Applications & Stability
- **DMC I2C Timeout**: Tuned the STM32 I2C transfer timeout to track upstream changes and avoid spurious stalls.
- **Data Path Alignment**: Ensured Tensix RAM buffers are 64-byte aligned to match the NOC DMA engine’s requirements.

### Continuous Integration
- **Devicetree Linting**: Enabled the devicetree linter in compliance checks and regenerated DTS files accordingly.
- **Workflow Hardening**: Updated CI runners and tag fetching to improve build reliability on shared hardware.

### Upstream Contributions
- **DMA Test Alignment**: Carried Zephyr patches so the DMA loop, link, scatter-gather, and burst-length tests honor the `dma-buf-addr-alignment` devicetree property, matching the Blackhole NOC DMA engine’s 64-byte requirement.
- **MSPI NOR Enhancements**: Maintained an upstream-targeted patch that adds `read-frequency` binding support and enables the flash page layout API while we validate the new upstream MSPI drivers.
- **STM32 SMBus PEC Support**: Upstreamed platform-independent PEC helpers and STM32 SMBus PEC handling, allowing us to drop the large local patch while preserving CRC-backed transactions.
- **STM32 SMBus PCall Coverage**: Delivered block read/write PCall support into Zephyr’s STM32 SMBus stack to keep legacy control paths working without downstream shims.
- **I2C DesignWare Reliability**: Landed the fix that reinstates the target-mode stop callback, resolving elusive synchronization hangs observed with ARC-based controllers.
- **Patch Pruning**: Cleared out SMBus and runner patches that merged alongside the Zephyr 4.3.0 bump, shrinking our downstream maintenance surface.

### Documentation
- **Getting Started**: Documented Python 3.12 installation steps for development environments.

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v19.1.0 release can be found in [v19.2 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-19.2.md).

## Full ChangeLog

The full ChangeLog from the previous v19.1.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v19.1.0...v19.2.0


## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
