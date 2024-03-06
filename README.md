# tt-firmware

## Official Repository
[https://github.com/tenstorrent/tt-firmware](https://github.com/tenstorrent/tt-firmware)

## What is this Firmware?

Why do you need to flash these binary blobs? On Tenstorrent devices we have a system management processor.
This processor is responsible for
    - Turning the hardware on
    - Making sure that external i/o (pcie, eth, dram, etc.) can connect and remain connected while the board is recieving power
    - Ensuring that we never exceed the power or temperature envolope that the card and chip were designed to operate in

## Why not open-source

In short it comes down to availablility of development resources. Tenstorrent products contain IP from third parties, we have agreements with these third parties which keeps us from distributing source code related to their property.
Therefore releasing the fw source code would require disentangling what we have ownership of vs. what is shared. Effectively requiring us to rewrite it to isolate anything proprietary, so we made the decision to spend the resources to
guarantee to make what we can of future fw open-source rather than going back to rewrite what we already have.

Also power management fw is really boring code. [UMD](https://github.com/tenstorrent-metal/umd) is where all of the interesting chip programming lives :)

## Available Firmware

| Firmware | Description |
| --- | --- |
| [`fw_pack-80.4.0.0_acec1267.tar.gz`](fw_pack-80.4.0.0_acec1267.tar.gz) | is a package containing the initial firmware images to flash Grayskull(gs) boards in order to use tt-smi |

## License
© 2023 Tenstorrent Inc.<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
