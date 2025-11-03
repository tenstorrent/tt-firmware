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
| [`fw_pack-19.1.0.fwbundle`](fw_pack-19.1.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

These release notes are also published in HTML at the URL below.

https://docs.tenstorrent.com/tt-zephyr-platforms/release/release-notes-19.1.html

Major enhancements with this release include new DMA drivers and enhanced SMBus communication stability.

## What's Changed

### Stability Improvements

  - Fixed a timing issue in Zephyr's `snps,designware-i2c` driver that caused intermittent loss of packet data
  - Improved error rate from 1 in 10k to 0 in 2M

### Drivers

- **New DMA Support**: Added comprehensive DMA driver infrastructure
  - New `dma_arc_hs` driver implementation
  - NOC-to-NOC DMA driver with proper device tree bindings
  - Full upstream DMA test configuration and support
  - Removed deprecated `noc_dma` files and includes

### Libraries

- **SMBus Enhancements**:
  - Improved DMC ping stability with better error handling
  - Added legacy ping command support for backwards compatibility

- **DMA Library Migration**:
  - Replaced custom NOC DMA implementation with standard Zephyr DMA subsystem

- **Removed APIs**:
  - Removed deprecated `tenstorrent fwupdate` library

### Documentation

- **Architecture Documentation**: Added comprehensive documentation about the boot process for both SMC and DMC components
- **Testing Documentation**: Updated pytest documentation with better usage examples and requirements

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v19.0.0 release can be found in [v19.1 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-19.1.md).

## Full ChangeLog

The full ChangeLog from the previous v19.0.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v19.0.0...v19.1.0


## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
