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
| [`fw_pack-18.5.0.fwbundle`](fw_pack-18.5.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### 18.5.0

New since [18.4.0](https://github.com/tenstorrent/tt-firmware/tree/v18.4.0)


### Stability Improvements

* Update Blackhole ERISC FW to v1.4.1
  * Fixed bug in FW where training would stall when enabling training on P300 ports that do not connect
    outside of the Chip at all
* Prevent invalid overwrite of DMC init time
* Automatically recover firmware after hardware CI jobs
* fan_ctrl: disable initial fan spin-up to 100%
* pcie: drive perst of cem1 slot when operating in RC mode

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.4.0 release can be found in [v18.5.0 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.5.0.md).

## Full ChangeLog

View the full ChangeLog at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.4.0...v18.5.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
