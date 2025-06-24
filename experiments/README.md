# tt-firmware - experiments
Firmware bundles built off of the latest available firmware release with minor modifications to address specific issues.

## Available Firmware
### 18.5.1
This is a patch release with additional changes on top of the previous
[18.5.0 release](https://github.com/tenstorrent/tt-firmware/releases/v18.5.0).

Changes include:

* Wormhole FW blob updated
  * CMFW 2.34.0.0
    * Update voltage regulator settings for n300
    * Additional verification of voltage regulator programming
  * ERISC FW 6.7.0.0
    * Add multi-mesh support for T3K
    * Fix intermittent static training synchronization failures on WH 6U Galaxy




## License
© 2025 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
