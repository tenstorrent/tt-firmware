# tt-firmware - experiments
Firmware bundles built off of the latest available firmware release with minor modifications to address specific issues.

## Available Firmware

| Firmware | Release Notes |
| --- | --- | 
| 80.15.2.0 | <ul><li>Built ontop of 80.15.0.0</li> <ul> <li>BH: Pick-up CMFW 0.9.2 </li> <ul> <li> Corrected telemetry table inadvertently reporting harvested ETH </li> <li> I2C Recovery mechanism if bus is hung. Will help mitigate [`vm stability issues`](https://github.com/tenstorrent/tt-metal/issues/18672)  </li> </ul> </ul> </ul> || 
| 80.15.3.0 | <ul><li>Built ontop of 80.15.0.0 - Wormhole Specifc Changes</li> <ul> <li>WH [n150, n300, 6U UBB Galaxy]: </li> <ul> <li> ARC FW 2.32.0 </li><ul> <li> Handshake with BM APP FW for SPI Copy Complete </li> <li> Increase Minimum Vcore to 800mV</li> <li> Increase MVDDQ to 1.38V and GDDRPHY to 0.88V for 6U UBB Galaxy</li> <li> VR Programming for 6U UBB Galaxy</li></ul> <li>ERISC 6.14</li> <ul><li>Tuning for 6U UBB Galaxy </li><li>Disable  port discovery and routing in base ERISC </li><li>MAC/PCS Conifg API for ERISC APP </li></ul><li> BM APP FW 5.12.0.0</li><ul><li>Handshake with ARC FW for SPI Copy Complete </li><li>Fix for remote chip detection on n300 </li></ul></ul> </ul> </ul> || 


## License
© 2024 Tenstorrent AI ULC<br/>
All rights reserved

Redistribution permitted, please see [LICENSE](LICENSE) for details.
