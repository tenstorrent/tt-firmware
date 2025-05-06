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
| [`fw_pack-18.2.0.0.fwbundle`](fw_pack-18.2.0.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### 18.2.0

New since [80.18.1.0](https://github.com/tenstorrent/tt-firmware/tree/v80.18.1.0)

* Update Blackhole ERISC FW to v1.4.0
  * Added ETH mailbox with 2 messages
  * ETH msg LINK_STATUS_CHECK: checks for link status
  * ETH msg RELEASE_CORE: Releases control of RISC0 to run function at specified L1 addr
* Virtual UART now enabled by default for Blackhole firmware bundles
  * Creates an in-memory virtual uart for firmware observability and debugging
  * Use `tt-console` to view `printk()` and `LOG_*()` messages from the host

### Stability Improvements

* Update Blackhole ERISC FW to v1.4.0
  * Improve link training sequence for greater success rate on loopback cases
* Fix synchronization issue in BMFW that could result in potential deadlock / failure to enumerate
* Improve SMC I2C recovery function, resulting in reset and re-enumeration success rate of 99.6%
* PCIe Maximum Payload Size (MPS) now set by TT-KMD, improving VM stability

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v80.18.1 release can be found in [v18.2.0 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.2.0.md).

## Full ChangeLog

View the full ChangeLog at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v80.18.1...v18.2.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
