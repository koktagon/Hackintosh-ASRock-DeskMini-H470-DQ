# Hackintosh ASRock DeskMini H470
## macOS Monterey 12.4 - OpenCore 0.8.0 - Intel Core i3-10100 - Deutsche Qualität

![obligatory screenshot](/images/skrienshod.png)

Things that are working and their corresponding kexts: - Intel UHD 630 Graphics - [WhateverGreen](https://github.com/acidanthera/WhateverGreen) (PLEASE SEE NOTES BELOW)
- Realtek ALC233 Audio - [AppleALC](https://github.com/acidanthera/AppleALC), layout ID 18 
- Intel AC 3168 WiFi+BT - [AirportItlwm](https://github.com/OpenIntelWireless/itlwm) + [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) 
- Intel I219-V Ethernet - [IntelMausi](https://github.com/acidanthera/IntelMausi)

Things partially or not working:
- HDMI audio
- AirDrop + Handoff (use a real BCM94360CS2 card)

SMBIOS is blanked on purpose, you need to provide your own, use 
[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) for that

## Graphics shenanigans

By default, all display outputs on macOS are forced to DisplayPort, which 
doesn't work for using HDMI output. This is what I added under 
DeviceProperties for the iGPU for the HDMI output to work:

```
AAPL,ig-platform-id      | Data | 07009B3E
framebuffer-patch-enable | Data | 01000000
framebuffer-con1-enable  | Data | 01000000
framebuffer-con1-alldata | Data | 02020A00 00080000 C7030000
```
