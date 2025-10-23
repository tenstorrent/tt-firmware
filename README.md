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
| [`fw_pack-19.0.0.fwbundle`](fw_pack-19.0.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

These release notes are also published in HTML at the URL below.

https://docs.tenstorrent.com/tt-zephyr-platforms/release/release-notes-19.0.html

Major enhancements with this release include:

- New bootloader scheme for CMFW and DMFW. This will improve update reliability
  for both firmware binaries
- If firmware flash fails, CMFW will now revert to recovery mode. From this mode
  tt-flash can be used to restore a working firmware.

## What's Changed

<!-- Subsections can break down improvements by (area or board) -->
<!-- UL PCIe -->
<!-- UL DDR -->
<!-- UL Ethernet -->
<!-- UL Telemetry -->
<!-- UL Debug / Developer Features -->
<!-- UL Drivers -->
<!-- UL Libraries -->

<!-- Performance Improvements, if applicable -->
### New and Experimental Features

* Update Blackhole ERISC FW to v1.7.0
  * ETH msg PORT_RETRAIN: force a link to retrain
  * ETH msg PORT_REINIT: asks a failed port to redo initialization
  * ETH msg PORT_LOOPBACK: allows putting the port in internal or external loopback
  * ETH msg INTERRUPT: enables or disables interrupts to the ERISC
  * ETH msg PORT_ACTION: force the link to be up or down via the MAC
  * ETH msg CABLE_CHECK: checks whether a cables exists or not
  * ETH msg TELEMETRY_EVENT: handles specific telemetry exchange events over the link
  * ETH msg REMOTE_ALIVE: send packet to check if remote side is alive
  * ETH msg PORT_SPEED: re-initializes the port to a different speed

<!-- External Project Collaboration Efforts, if applicable -->

### Developer & Debug Tools
- **scripts**: New `dump_smc_stack.py` utility for on-demand SMC state analysis
- **scripts: tooling**: Enhanced `tt-console` with PCIe rescan skip option for smooth TT-KMD transitions (2.3.0 to 2.4.1)
- **scripts**: Updated `blackhole_recovery` with improved status messaging and increased delays

* Update Blackhole ERISC FW to v1.7.0
  * Fix snapshot reading bug in eth_runtime where the upper 32 bits of a preceding metric read is picked up by the following metric read
  * Remove interrupt enablement as current implementation can cause infinite loops
  * Changed logical_eth_id calculation using new enabled_eth param to address SYS-2064
  * Added ASIC ID in chip_info and param table to address SYS-2065
  * Changed manual EQ TX-FIRs for ASIC 8 Retimer ports to address SYS-2096
  * Only trigger retraining if check_link_up polls link down for 5ms
  * Removed BIST check in training sequence, improves stability a bit
  * Send chip_info packet on retrain completion, which along with BIST disabled allows for a single chip with an active link to be reset and allow the link come back up
  * Set manual TX FIR parameters for warp cable connections on P300 to 1/3/4/45/2 for PCB-1997
  * increase stack size to 2048 for SYS-2266
  * inline icache flush function for SYS-2267
  * Fix for reset skew where one tt-smi reset should make other side up
  * Added interrupt enablement again, controlled via INTERRUPT_CHECK feature enable flag
  * Moved auto retraining outside of link_status_check into its own link check state machine, controlled via DYNAMIC_LINK_STATE_CHECK feature enable flag
  * Added link flap check based on resend and un-cor words
  * Added eth_reinit state machine to handle fail case when port is up
* PVT Sensor
  * correct PVT RTIO buffer size and frame count for decode
* Update Wormhole FW blob
  * ERISC 6.7.2.0
  * Add support to trigger retraining on failed training ethernet ports

<!-- Security vulnerabilities fixed? -->
<!-- API Changes, if applicable -->
<!-- Removed APIs, H3 Deprecated APIs, H3 New APIs, if applicable -->
<!-- New Samples, if applicable -->
<!-- Other Notable Changes, if applicable -->
<!-- New Boards, if applicable -->

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.12.0 release can be found in [v19.0 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-19.0.md).

## Full ChangeLog

The full ChangeLog from the previous v18.12.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.12.0...v19.0.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
