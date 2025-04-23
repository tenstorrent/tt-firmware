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
| [`fw_pack-80.18.0.0.fwbundle`](fw_pack-80.18.0.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### 80.18.0.0

New since [80.17.0.0](https://github.com/tenstorrent/tt-firmware/tree/1fff46a95e210770aa33b37af09fda9fed27062a)
- BH [p100 p100a p150a p150b p150c p300a p300b p300c]: 
  - CMFW 0.10.0
    - NOC Translation and Harvesting support (SYS-750)
      - Note: this is a potentially breaking change for software and depends on the presence of tt-metal support
    - Support for Blackhole Cloud VM Triaging (SYS-1286)
    - EMC Readiness (SYS-1212)
    - p100a / p150a Fan Control (SYS-527)
    - Report ai_clk as set rather than actual for p150c and p300c (SYS-1410)
  - ERISC 1.2.0
    - Updated ETH FW training sequence to be more stable
    - Increased default ETH training speed to 400 Gbps
    - Updated training sequence APIs to address issue where noc_copy() from ETH to DRAM could cause hangs.
  - MRISC 2.6.0
    - Expanded GDDR Telemetry Table to include:
      - speed
      - training status
      - error status
      - firmware version
      - DRAM vendor
      - number of corrected and uncorrected EDC errors
    - Fixed a bug for Micron E die revision parameter setting

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
