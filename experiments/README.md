# tt-firmware - experiments
Firmware bundles built off of the latest available firmware release with minor modifications to address specific issues.

## Available Firmware

| Firmware | Release Notes |
| --- | --- | 
| [`fw_pack-80.10.1.0.fwbundle`](fw_pack-80.10.1.0.fwbundle) | Decrease max AICLK to 900MHz|
| [`fw_pack-80.10.2.0.fwbundle`](fw_pack-80.10.2.0.fwbundle) |<ul><li>VR Regulator programming to ensure current is balanced on phases</li><li>ARC workaround to prevent I2C hangs</li></ul>|
| [`fw_pack-80.10.3.0.fwbundle`](fw_pack-80.10.3.0.fwbundle) |<ul><li>Built ontop of 80.10.2.0</li><li>Use last good value if invalid i2c data received</li></ul>|

## License
© 2024 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
