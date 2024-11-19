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
| [`fw_pack-80.13.2.0.fwbundle`](fw_pack-80.13.2.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and for the first time Blackhole(bh) boards.|

## Release Notes

### 80.13.2.0
- BH: Resolve I2C race condition to improve TT-SMI Reset stability

### 80.13.1.0
- BH: Address noc hang caused by disabled blocks on the p100 board

### 80.13.0.0
- WH: Pick up fixes in 80.10.4.0 to help address tt-metal issue [#4968](https://github.com/tenstorrent-metal/tt-metal/issues/4968)
  - VR Regulator Tuning for N150 and N300 boards
  - Data sanitization on i2c received data
  - BM APP FW 5.10.0.0 - modified handling of thermal interrupts
- WH: ETH FW 6.10.0
- WH: Added support for 6U UBB Galaxy
- BH: First firmware bundle containing support for Blackhole boards.


## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2024 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
