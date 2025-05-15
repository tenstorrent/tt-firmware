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
| [`fw_pack-18.3.0.fwbundle`](fw_pack-18.3.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### 18.3.0

New since [18.2.0](https://github.com/tenstorrent/tt-firmware/tree/v18.2.0)

* DMC now reads and sends power (instead of current) from INA228 device to SMC
  * SMC now uses power reading as input to Total Board Power (TBP) throttler instead of 12 * current
* DMC support for accessing tca9554a GPIO expanders added


### Stability Improvements

* Add I2C handshake between SMC and DMC FW to ensure that initialization messages are received
* Total Board Power (TBP) throttler parameters have been tuned, and TBP limit is now set in the fwtable to guarantee product definition is followed

## API Changes

### Removed APIs

* Telemetry no longer reports `TAG_INPUT_CURRENT`

### New APIs

* Telemetry now reports `TAG_INPUT_POWER` to replace `TAG_INPUT_CURRENT`

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.2.0 release can be found in [v18.3.0 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.3.0.md).

## Full ChangeLog

View the full ChangeLog at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.2.0...v18.3.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
