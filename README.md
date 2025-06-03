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
| [`fw_pack-18.4.0.fwbundle`](fw_pack-18.4.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### 18.4.0

New since [18.3.0](https://github.com/tenstorrent/tt-firmware/tree/v18.3.0)

* DMC now increments a counter for thermal trips and reports the count to SMC
  * SMC now reports this value in the telemetry table
  * This counter is reset on PERST
* Add an SMC message to toggle Tensix resets for testing purposes

### Performance Improvements

* Wormhole FW blob updated
  * SPI bootrom 3.13.0.0
    * Remove PCIe MPS limit (**Note: tt-kmd >= 1.33 is required**)
  * CMFW 2.33.0.0
    * Fix to decrease variation across TMONs at idle
    * Make therm trip limit a SPI parameter
    * Backport BH-style telemetry tables
  * ERISC FW 6.6.15.0
    * Training improvements for 6U UBB Galaxy

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.3.0 release can be found in [v18.4.0 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.4.0.md).

## Full ChangeLog

View the full ChangeLog at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.3.0...v18.4.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
