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
| [`fw_pack-19.4.0.fwbundle`](fw_pack-19.4.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

These release notes are also published in HTML at the URL below.

https://docs.tenstorrent.com/tt-zephyr-platforms/release/release-notes-19.4.html

We are pleased to announce the release of TT Zephyr Platforms firmware version 19.4.0 🥳🎉.

Major enhancements with this release include:

## What's Changed

### Stability Improvements

* Update Wormhole FW blob
  * ERISC FW 6.7.3.0
    * Fix retrain hangs with Active Cables
    * Adjust DFE value to improve BER on WH UBB QSFP ports
    * Link quality improvements to non-retimer long trace on WH UBB
    * Updated retraining logic to set train_status to LINK_TRAIN_TRAINING when entering into retraining
    * Remove link_training_fw_phony debug feature from eth_init to free up more space
  * Switch WH FW over to Zephyr ARC toolchain 0.17.4
  * Fix BSS to be 0-initialized
    * Causes telemetry `TAG_TIMER_HEARTBEAT` to start at 0 upon reset
  * GDDR improvement for WH Galaxy
    * Increase read latency from 23 to 25 for 14G
    * Explicitly disable EDC tracking
  * Add vendor-specific GDDR settings and report GDDR vendor
* Re-release MRISC FW 2.11
  * Reduce Galaxy datarate to 14G to address regression in FW bundle v19.3.0
  * Reapply memory bandwidth utilization improvements to all board types

### Drivers

* Fix SMBus cancel/uncancel interface
  * Driver-specific implementations are now properly called
  * Cancel state is now properly taken into account when starting a transaction, which fixes some PCIe enumeration issues

### Libraries

* BH ARC library improvements
  * AICLK power management enhancements
    * Apply AICLK busy state from GO_BUSY and POWER messages for legacy application compatibility
    * Track last BUSY/IDLE message received and apply AICLK state based on both that and power settings
    * Extended native simulation support for aiclk_ppm initialization
  * Message queue improvements
    * Add doxygen documentation and structured access for ASIC state messages (TT_SMC_MSG_ASIC_STATE0 and TT_SMC_MSG_ASIC_STATE3)
    * Add doxygen documentation and structured access for TT_SMC_MSG_TEST
    * Code formatting improvements (clang-format)
  * Power management logging improvements
    * Condense noisy prints in bh_power into a single print statement

### Debug / Developer Features

* Scripts and tooling improvements
  * `tt_bootstrap`: Add support for erasing flash with `west flash -r tt_bootstrap --erase`
  * `vuart`: Open file descriptor with O_APPEND flag to prevent power-on when opening console
  * Add `update_versions.sh` script to upgrade versions of SMC, DMC, and FW during the release process

### Other Notable Changes

* Documentation
  * Update release process documentation to use version update script
  * Add firmware signing key conflicts guide explaining how to move from a production-signed firmware to a development-signed firmware (v19.0.0+)


## Migration guide

An overview of required and recommended changes to make when migrating from the previous v19.3.0 release can be found in [v19.4 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-19.4.md).

## Full ChangeLog

The full ChangeLog from the previous v19.3.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v19.3.0...v19.4.0


## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
