# BLE-toolkit
Various tools for exploring BLE

## nRF51 BLE Sniffer
Uses assets from the [nrf51_dongle_sniffer](nrf51_dongle_sniffer) folder
### Hardware Requirements
- [nRF51 USB dongle](https://www.nordicsemi.com/Software-and-Tools/Development-Kits/nRF51-Dongle)
### Sniffer FW Flashing Instructions
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
  
### Sniff with Wireshark
Prepare Wireshark to sniff BLE traffic using the nRF51 dongle.
#### Setup
1. Download latest version of [Wireshark](https://www.wireshark.org/#download)
2. Navigate to Wireshar's extcap directory. For MacOS: Wireshark->Contents->MacOS->extcap
3. Copy and paste the content of [wireshark_extcap](nrf51_dongle_sniffer/wireshark_extcap) to the Wireshark `extcap` directory
4. Launch Wireshark and double click on `nRFSniffer` in the capture device list

*__If the `nRFSniffer` device is not in the list, reconnect dongle and restart Wireshark__*

#### Some Useful Filters
##### Filter by advertising data: Find packets containig specific advertisement data
__Filter:__ `btcommon.eir_ad.entry.data contains <data>`\
`<data>` is the byte sequence to search for. Where each byte is separated by `:`\
_Example:_ Find device with advertising data containing `50414E45`\
`btcommon.eir_ad.entry.data contains 50:41:4E:45`

##### Filter by source MAC address
__Filter:__ `btle.advertising_address ==  <MAC address>`\
`<MAC address>` is the device's mac address separated by `:`\
_Example:_ Find device with MAC address `F5:55:F1:7E:21:06`\
`bbtle.advertising_address ==  F5:55:F1:7E:21:06`
