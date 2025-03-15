# tt-firmware - experiments
Firmware bundles built off of the latest available firmware release with minor modifications to address specific issues.

## Available Firmware

| Firmware | Release Notes |
| --- | --- | 
| 80.15.2.0 | <ul><li>Built ontop of 80.15.0.0</li> <ul> <li>BH: Pick-up CMFW 0.9.2 </li> <ul> <li> Corrected telemetry table inadvertently reporting harvested ETH </li> <li> I2C Recovery mechanism if bus is hung. Will help mitigate [`vm stability issues`](https://github.com/tenstorrent/tt-metal/issues/18672)  </li> </ul> </ul> </ul> || 


## License
© 2024 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
