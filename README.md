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
| [`fw_pack-18.12.0.fwbundle`](fw_pack-18.12.0.fwbundle) | is a package containing the  combined firmware image to flash Grayskull(gs),  Wormhole(wh) and  Blackhole(bh) boards.|

## Release Notes

These release notes are also published in HTML at the URL below.

https://docs.tenstorrent.com/tt-zephyr-platforms/release/release-notes-18.12.html

<!-- H3 Performance Improvements, if applicable -->

### Performance Improvements

* soc: tt_blackhole: enable hardware floating-point in SMC FW

<!-- H3 New and Experimental Features, if applicable -->
<!-- H3 External Project Collaboration Efforts, if applicable -->

<!-- H3 Stability Improvements, if applicable -->

### Stability Improvements

* boards: tt_blackhole: p150c: correct tdp_limit & tdc_limits
* scripts: recover-blackhole: add recovery bundle scripting in-tree
* patches: Fix smbus PEC correction patch
* ci: workflows: hardware-long: update metal container version and test p300a
* app: dmc: Move MFD, PWM and sensor configs to prj.conf
* scripts: tooling: vuart: report error if card reads as `0xffff_ffff`

<!-- H1 Security vulnerabilities fixed? -->

<!-- H2 API Changes, if applicable -->

<!-- H3 Removed APIs, H3 Deprecated APIs, H3 New APIs, if applicable -->

<!-- UL PCIe -->
<!-- UL DDR -->
<!-- UL Ethernet -->
<!-- UL Telemetry -->
<!-- UL Debug / Developer Features -->

### Debug / Developer Features

* `tt-zephyr-platforms` documentation is now available online at https://docs.tenstorrent.com/tt-zephyr-platforms 🙌🪁
  * doc: getting_started: move contents from README.md to getting started guide, and publish to HTML
  * doc: develop: add documentation for tracing
* ci: build-native: publish tt-console and tt-tracing artifacts
  * previously, users needed to build these binaries themselves with `make -C scripts/tooling`. Now they are built on every commit.
* ci: release: ensure build artifacts for all board revisions are in zip
* scripts: tt_boot_fs: ls: add hexdump functionality when verbose >= 2
  * this allows us to inspect all contents of TT Boot FS .bin files without breaking out a separate hex editor
* bh_arc: tt_shell: add shell support
  * a common location for custom Tenstorrent shell commands
  * print telemetry data with `telem` sub-command
  * read (and write) asic state with `asic_state` sub-command
* app: dmc: enable logging via DMC SMBUS path
  * first logs to a local ringbuffer, and then data is sent over smbus from DMC to SMC
  * users should now be able to view DMC logs with `tt-console -c 2`

<!-- UL Drivers -->

### Drivers

* drivers: sensor: pvt: integrate pvt driver, add tolerance in tests, read efused temperature calibration
* drivers: smbus: add platform-independent `zephyr,smbus-target` driver (should be upstreamed shortly)

<!-- UL Libraries -->

<!-- H2 New Samples, if applicable -->

<!-- UL PCIe -->
<!-- UL DDR -->
<!-- UL Ethernet -->
<!-- UL Telemetry -->
<!-- UL Debug / Developer Features -->
<!-- UL Drivers -->
<!-- UL Libraries -->

<!-- H2 Other Notable Changes, if applicable -->

<!-- UL PCIe -->
<!-- UL DDR -->
<!-- UL Ethernet -->
<!-- UL Telemetry -->
<!-- UL Debug / Developer Features -->
<!-- UL Drivers -->
<!-- UL Libraries -->

<!-- H2 New Boards, if applicable -->

## Migration guide

An overview of required and recommended changes to make when migrating from the previous v18.10.0 release can be found in [v18.12 Migration Guide](https://github.com/tenstorrent/tt-zephyr-platforms/tree/main/doc/release/migration-guide-18.12.md).

## Full ChangeLog

The full ChangeLog from the previous v18.10.0 release can be found at the link below.

https://github.com/tenstorrent/tt-zephyr-platforms/compare/v18.10.0...v18.12.0

## Experiments

Experiment firmware bundles are based off of the latest available firmware with minor modifications to address specific issues. These experiments can be found in [`experiments`](experiments/) .

For specific details on the changes refer to the experiments [`README`](experiments/README.md).

## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
