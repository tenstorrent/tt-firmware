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

Also power management fw is really boring code. [UMD](https://github.com/tenstorrent/tt-umd) is where all of the interesting chip programming lives :)

## Available Firmware

| Firmware | Description |
| --- | --- |
| [`fw_pack-80.9.0.0.fwbundle`](fw_pack-80.9.0.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs) and Wormhole(wh) boards|

## Release Notes

### 80.9.0.0
- GS: Correct Max Frequency to 1200MHz 
- WH: Fix SMBUS issue on N300s

## Patches

Patch firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These patches can be found in [`patches`](patches/) .

For specific details on the changes refer to the patches [`README`](patches/README.md).

## License
© 2024 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
