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
| [`fw_pack-18.8.0.fwbundle`](fw_pack-18.8.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

New since [18.7.0](https://github.com/tenstorrent/tt-firmware/tree/v18.7.0)

### Stability Improvements

* Update Blackhole MRISC FW to v2.9
  * Modified Tuning setting for BH Galaxy cards
    * Pull in changes from P300 Learning: dram_ocd_pulldown_offset increased to “3”
    * Adjust CA delay from “8” to “0” (Using the default values that are already used in other projects like P100, P150 and P300).
    * Removed bottom DRAM to train CA bus (Using the default values that are already used in other projects like P100, P150 and P300).
* The `tenstorrent,bh-clock-control` driver has seen some improvements
  * Driver is used by default and initialized via Zephyr's init system, like all other devices in the driver model
  * Fixed a bug where the AICLK frequency was set to 1/4 of the expected value by correctly accounting for postdiv
  * Read AICLK limits from fwtable instead of devicetree
* The `tenstorrent,bh-fwtable` driver now deterministically loads tables on initialization
* Telemetry now displays `AICLK_MAX`, `VDD_LIMIT`, `THM_LIMIT` and `TDC_LIMIT` via `tt-smi`.
* Added regulator config values for p300 and galaxy
* `tt-console`
  * Support rescan via `ioctl()`
  * Fixed a bug to account for rescanning from within a container returning `-ENXIO` instead of the expected `-ENOENT`
  * Do not return with an error if interrupted by a signal (`SIGINT` / `Ctrl+C`)
* Added SMBus command to update ARC state, along with `native_sim`-based testsuite
* P300
  * Normalize `p300a`, `p300b`, and `p300c` to be like regular board variants
  * Add a GPIO spec to Devicetree to for the P300 JTAG mux
  * Fix fan control for p300

[comment]: <> (H1 Security vulnerabilities fixed?)

[comment]: <> (H2 API Changes, if applicable)

### New APIs

[comment]: <> (UL PCIe)
[comment]: <> (UL DDR)
[comment]: <> (UL Ethernet)
[comment]: <> (UL Telemetry)
[comment]: <> (UL Debug / Developer Features)
[comment]: <> (UL Drivers)

### Removed APIs

#### Drivers

* Removed the forked stm32 i2c driver
* Removed the forked stm32 smbus driver

#### Libraries

* TT Boot FS
  * Two new API calls; `ls` to list files in the filesystem, and a second to read an individual file descriptor by tag
  * list files on a filesystem on `dev`: `int tt_boot_fs_ls(const struct device *dev, tt_boot_fs_fd *fds, size_t nfds, size_t offset);`
  * look up a single file on `dev`: `int tt_boot_fs_ls(const struct device *dev, tt_boot_fs_fd *fds, size_t nfds, size_t offset);`
  * The filesystem is now fully specified via devicetree, removing the need for several redundant YAML files

[comment]: <> (H2 New Samples, if applicable)

[comment]: <> (UL PCIe)
[comment]: <> (UL DDR)
[comment]: <> (UL Ethernet)
[comment]: <> (UL Telemetry)
[comment]: <> (UL Debug / Developer Features)
[comment]: <> (UL Drivers)
[comment]: <> (UL Libraries)

[comment]: <> (H2 Other Notable Changes, if applicable)

[comment]: <> (UL PCIe)
[comment]: <> (UL DDR)
[comment]: <> (UL Ethernet)
[comment]: <> (UL Telemetry)
[comment]: <> (UL Debug / Developer Features)
[comment]: <> (UL Drivers)
[comment]: <> (UL Libraries)

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.7.0 release can be found in [v18.8 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.8.md).

## Full ChangeLog

The full ChangeLog from the previous v18.7.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.7.0...v18.8.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
