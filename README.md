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
| [`fw_pack-19.3.1.fwbundle`](fw_pack-19.3.1.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

These release notes are also published in HTML at the URL below.

https://docs.tenstorrent.com/tt-zephyr-platforms/release/release-notes-19.3.html

We are pleased to announce the release of TT Zephyr Platforms firmware version 19.3.1 🥳🎉.

Major enhancements with this release include:

### New and Experimental Features

* Update Blackhole ERISC FW to v1.7.0
  * ETH msg DYNAMIC_NOC_INIT: Initialize dynamic NOC state for the ethernet core
* Doppler Power Management
  * Low-latency power management optimizing bursty workloads on p100a and p150* boards
  * 100 kHz tick rate, switched to a tick-less kernel
* Support BAR4 resizing
* New ARC message for blinking the board fault LED for board identification purposes
* New firmware bundle for Debian

### Drivers

* ``snps,designware-dma-arc-hs``: integrated ARC DMA driver into codebase
  * ARC DMA driver follows the upstream Zephyr DMA driver API

### Stability Improvements

* Update Blackhole ERISC FW to v1.7.1
  * Enable all TX/RXQ to be in packet mode after initial training for SYS-2294
  * Implement NOC counters in L1 for SYS-2489
  * Fixed left vs right chip logic in manual EQ override for P300
  * Changed default training mode back to ANLT for P150s and P300 on-PCB traces
  * Fixed bug that clears live status counters unnecessarily
  * Removed BIST check altogether from SerDes init sequence
  * Minimized SerDes access during retraining to reduce NOC traffic
  * Improve one sided reset and retrain logic for ANLT
  * Reduced ETH training timeouts
* Fixed a potential hang when Tensix is generating NOC traffic to idle GDDR
* Added more tests for ARC and I2C messaging
* Made tensix idle before clock gating in our reset flows
  * More graceful cleanup in cases of crashes, and more robust power down flows

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v19.2.0 release can be found in [v19.3 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-19.3.md).

## Full ChangeLog

The full ChangeLog from the previous v19.2.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v19.2.0...v19.3.1


## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
