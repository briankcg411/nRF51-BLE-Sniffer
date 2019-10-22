# BLE-toolkit
Various tools for exploring BLE

## nRF51 Sniffer
### Flashing Instructions
- [Using nRF Connect Desktop](https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Connect-for-desktop
) - Programmer App
1. Open nRF Connect Desktop
2. Launch Programmer App (install if missing) 
3. Select dongle from device list
4. Add hex file `sniffer_pca10031_1c2a221.hex`
5. Write hex to device
- Using [JLink Commander](https://www.segger.com/downloads/jlink/) CLI
1. `cd` to directory containing sniffer hex
2. Run `jlinkexe`
3. Device -> `NRF51422`
4. Interface -> `SWD`
5. Speed -> `default(4MHz)`
6. `loadfile sniffer_pca10031_1c2a221.hex`
7. Enter `r` to reset target
8. Enter `g` to run sniffer firmware
  
### Wireshark
Wireshark is the prefered tool to sniff BLE traffic.
#### Set up Wireshark
1. Download latest version of [Wireshark](https://www.wireshark.org/#download)
2. Navigate to Wireshar's extcap directory. For MacOS: Wireshark->Contents->MacOS->extcap
3. Drop the python script `nrf_sniffer.py` and the `SnifferAPI` folder inside the `extcap` directory
4. Launch Wireshark and double click on `nRFSniffer` in the capture device list

### Some Useful Filters
#### Filter by advertising data: Find packets containig specific advertisement data
__Filter:__ `btcommon.eir_ad.entry.data contains <data>`\
`<data>` is the byte sequence to search for. Where each byte is separated by `:`\
_Example:_ Find device with advertising data containing `50414E45`\
`btcommon.eir_ad.entry.data contains 50:41:4E:45`

#### Filter by source MAC address
__Filter:__ `btle.advertising_address ==  <MAC address>`\
`<MAC address>` is the device's mac address separated by `:`\
_Example:_ Find device with MAC address `F5:55:F1:7E:21:06`\
`bbtle.advertising_address ==  F5:55:F1:7E:21:06`
