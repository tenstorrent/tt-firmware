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
| [`fw_pack-18.10.0.fwbundle`](fw_pack-18.10.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### Stability Improvements

* Update Blackhole ERISC FW to v1.6.0
  * Added eth_flush_icache to flush instruction cache for SYS-1944 - function is 2048 NOP instructions unrolled
  * New function pointer in eth_api_table: eth_flush_icache_ptr for aforementioned eth_flush_icache
  * Increased eth code size allocation by 8KB, code now starts at 0x70000
  * Enhanced training flow and retrain logic, links should now more reliably train up
  * Enabled interrupts in erisc fw: now snapshots and clears
  * Added live retraining when check_link_status() detects link down
  * ETH msg LINK_UP_CHECK: fast check to only update rx_link_up field of eth_live_status
* Setup FW table to lower ETH train speeds for Galaxy products to 200G, other products stay 400G

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

An overview of required and recommended changes to make when migrating from the previous v18.9.0 release can be found in [v18.10 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.10.md).

## Full ChangeLog

The full ChangeLog from the previous v18.9.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.9.0...v18.10.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
