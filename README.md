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
| [`fw_pack-18.9.0.fwbundle`](fw_pack-18.9.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### Performance Improvements

* Load spi flash images using temporary buffer rather than large statically allocated SRAM buffer
  * Represents a reduction of CSM memory usage by approximately 60 kiB since approximately v18.7.0

[comment]: <> (H3 New and Experimental Features, if applicable)
[comment]: <> (H3 External Project Collaboration Efforts, if applicable)

### Stability Improvements

* Update Blackhole ERISC FW to v1.5.0
  * Updated some eth training sequencing to help with Galaxy UBB products
  * Added CALL_ACK postcode in eth msg mailboxes to show message has been read and is being processed
  * Added fence instructions in eth msg mailboxes to invalidate L1 cache when polling
  * Changed default training mode to AUTO mode from ANLT, will result in manual eq on Galaxy QSFP ports
  * ETH msg FEATURE_ENABLE: allows for enable/disablement of eth fw features

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

[comment]: <> (H2 Other Notable Changes, if applicable)

[comment]: <> (UL PCIe)
[comment]: <> (UL DDR)
[comment]: <> (UL Ethernet)
[comment]: <> (UL Telemetry)
[comment]: <> (UL Debug / Developer Features)
[comment]: <> (UL Drivers)
[comment]: <> (UL Libraries)

[comment]: <> (H2 New Boards, if applicable)

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.8.0 release can be found in [v18.9 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.9.md).

## Full ChangeLog

The full ChangeLog from the previous v18.8.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.8.0...v18.9.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
