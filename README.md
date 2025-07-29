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
| [`fw_pack-18.7.0.fwbundle`](fw_pack-18.7.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

New since [18.6.0](https://github.com/tenstorrent/tt-firmware/tree/v18.6.0)

### Zephyr-4.2.0

This release of `tt-zephyr-platforms` runs on the latest v4.2.0 release of the Zephyr Real-time Operating System.

Zephyr v4.2.0 Release Notes are available [here](https://docs.zephyrproject.org/4.2.0/releases/release-notes-4.2.html)

### New and Experimental Features

* Enabled PCIe event counters

Major enhancements with this release include:

[comment]: <> (H3 Performance Improvements, if applicable)

### New and Experimental Features

* Implement aiclk_ppm sweep handler

[comment]: <> (H3 External Project Collaboration Efforts, if applicable)

### Stability Improvements

* Reduce Blackhole Galaxy GDDR speed from 16G to 14G
* Update Wormhole FW blob
  * CMFW 2.35.0.0
    * Fix telemetry entry ENABLED_TENSIX_ROW
    * Add telemetry entries for ASIC_ID_{HIGH,LOW}

[comment]: <> (H1 Security vulnerabilities fixed?)

[comment]: <> (H2 API Changes, if applicable)

[comment]: <> (H3 Removed APIs, H3 Deprecated APIs, H3 New APIs, if applicable)

[comment]: <> (UL PCIe)
[comment]: <> (UL DDR)
[comment]: <> (UL Ethernet)
[comment]: <> (UL Telemetry)
[comment]: <> (UL Debug / Developer Features)
[comment]: <> (UL Drivers)
[comment]: <> (UL Libraries)

[comment]: <> (H2 New Samples, if applicable)

[comment]: <> (UL PCIe)
[comment]: <> (UL DDR)
[comment]: <> (UL Ethernet)
[comment]: <> (UL Telemetry)
[comment]: <> (UL Debug / Developer Features)
[comment]: <> (UL Drivers)
[comment]: <> (UL Libraries)

### Other Notable Changes

[comment]: <> (UL PCIe)
[comment]: <> (UL DDR)
[comment]: <> (UL Ethernet)
[comment]: <> (UL Telemetry)

#### Debug / Developer Features

* The `tenstorrent,vuart` virtual PCIe serial device is now the default for console I/O. The virtual uart supports multiple instances, so one instance may be used for console I/O while another instance may be used for e.g. RPC, tracing, coredump, profiling, or other functionality. [Demo](https://github.com/tenstorrent/tt-zephyr-platforms/blob/f138f5b24c766a0088cbb88bc04ba3d31acf43f2/doc/img/shell.gif).
* Zephyr's tracing subsystem may now be used over the virtual uart. For now it is limited to a an app [overlay](https://github.com/tenstorrent/tt-zephyr-platforms/blob/v18.7.0/app/smc/tracing.conf) but plans are in place to integrate this feature into production firmware with support for dynamically configurable tracing. [Demo](https://github.com/tenstorrent/tt-zephyr-platforms/blob/f138f5b24c766a0088cbb88bc04ba3d31acf43f2/doc/img/tracing.gif)

[comment]: <> (UL Drivers)
[comment]: <> (UL Libraries)

[comment]: <> (H2 New Boards, if applicable)

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.6.0 release can be found in [v18.7 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/blob/v18.7.0/doc/release/migration-guide-18.7.md).

## Full ChangeLog

The full ChangeLog from the previous v18.6.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.6.0...v18.7.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
