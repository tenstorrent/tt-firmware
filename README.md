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
| [`fw_pack-18.6.0.fwbundle`](fw_pack-18.6.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### 18.6.0

New since [18.5.0](https://github.com/tenstorrent/tt-firmware/tree/v18.5.0)

### Zephyr-4.2.0

This release of `tt-zephyr-platforms` begins migrating our application to run on the v4.2.0 release candidate of the Zephyr Real-time Operating System.

A preview of all of the new features in Zephyr v4.2.0 are available
[here](https://github.com/zephyrproject-rtos/zephyr/blob/main/doc/releases/release-notes-4.2.rst).

### New and Experimental Features

* Enabled PCIe event counters

### Performance Improvements

* Enabled Quad DDR SPI mode to speed up loading cmfw

### Stability Improvements

* Aligned ASIC location definition in the SPI table with that of the telemetry table
* Update Blackhole ERISC FW to v1.4.2
  * Updated ASIC location definition to align with SPI table changes
* Implemented SDIF timeout for PVT sensor read
* Update Blackhole MRISC FW to v2.8
  * Added Tuning setting for P300B cards
  * * dram_ocd_pulldown_offset = 3 (MR2[2:0]) (increase pull down driver strength)
  * * dram_data_termination_offset = 1 (MR3[2:0]) (decrease DRAM termination)

* Wormhole FW blob updated
  * CMFW 2.34.0.0
    * Update voltage regulator settings for n300
    * Additional verification of voltage regulator programming
  * ERISC FW 6.7.0.0
    * Add multi-mesh support for T3K
    * Fix intermittent static training synchronization failures

### Drivers

* add `tenstorrent,bh-gpio` driver
* add `tenstorrent,bh-fwtable` driver
* add `maxim,max6639` driver + tests
* add `tenstorrent,bh-fwtable` driver + tests
* add `tenstorrent,bh-clock-control` (PLL) driver + tests

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.5.0 release can be found in [v18.6.0 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.6.0.md).

## Full ChangeLog

View the full ChangeLog at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.5.0...v18.6.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
