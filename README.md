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
| [`fw_pack-80.17.0.0.fwbundle`](fw_pack-80.17.0.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

### 80.17.0.0
- BH [p100 p150 p150a p150c]: 
  - CMFW 0.9.3
    - Corrected telemetry table inadvertently reporting harvested ETH
    - Fixes for [`vm stability issues`](https://github.com/tenstorrent/tt-metal/issues/18672)
      - I2C Recovery mechanism if bus is hung.
      - Reduce PCIe Config Max Payload Size(MPS) to avoid mismatch between USP and DSP after reset in VM
  - ERISC 1.0.0
  - MRISC 2.5.0
- WH [n150, n300, 6U Galaxy]
  - ARC FW 2.32.0
    - Handshake with BM APP FW for SPI Copy Complete
    - Increase Minimum Vcore to 800mV.
      - Improves stability running intensive workloads. [E.g. LoudBox model instability](https://github.com/tenstorrent/cloud/issues/3217)
    - Increase MVDDQ to 1.38V and GDDRPHY to 0.88V for 6U UBB Galaxy
    - VR Programming for 6U UBB Galaxy
  - ERISC 6.14
    - Tuning for 6U UBB Galaxy
    - Disable port discovery and routing in base ERISC
    - MAC/PCS Conifg API for ERISC APP
  - BM APP FW 5.12.0.0
    - Handshake with ARC FW for SPI Copy Complete
    - Fix for remote chip detection on n300


## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
