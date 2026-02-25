# tt-firmware

> **⚠️ ARCHIVED: This repository is now archived and no longer maintained.**
> 
> **All future firmware development and releases have moved to: [tenstorrent/tt-system-firmware](https://github.com/tenstorrent/tt-system-firmware)**
> 
> Please visit the new repository for the latest firmware releases, updates, and to contribute or report issues.

## Legacy Repository (Archived)

[https://github.com/tenstorrent/tt-firmware](https://github.com/tenstorrent/tt-firmware) (**ARCHIVED**)

This repository contains firmware binaries for Tenstorrent's Wormhole and Blackhole hardware. To see the open source files and how to get started with our development environment, visit [`tt-zephyr-platforms`](https://github.com/tenstorrent/tt-zephyr-platforms).

**For new firmware releases and development, please use [tenstorrent/tt-system-firmware](https://github.com/tenstorrent/tt-system-firmware).**

## What is this Firmware?

On Tenstorrent devices there are two embedded controllers,

* The Device Management Controller (DMC) manages board level functions such as power rails and fans.

* The System Management Controller (SMC) manages on-chip functions such as clocks, telemetry and ensuring external IO (PCIe, Ethernet, DRAM) can connect and remain connected.

If you are interested in the extent that applications interact with this firmware, see our [User Mode Driver](https://github.com/tenstorrent/tt-umd).

## Getting Started

**Note: For the latest firmware releases, please visit [tenstorrent/tt-system-firmware](https://github.com/tenstorrent/tt-system-firmware).**

Download firmware bundles from the [tt-system-firmware Releases page](https://github.com/tenstorrent/tt-system-firmware/releases), and use our [`tt-flash`](https://github.com/tenstorrent/tt-flash) utility to flash the bundle onto your Wormhole or Blackhole hardware. Refer to the release notes for any minimum `tt-flash` version required for a given firmware release.

Historical firmware releases from this archived repository can still be found on the [legacy Releases page](https://github.com/tenstorrent/tt-firmware/releases).

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
