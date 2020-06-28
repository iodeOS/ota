![alt text](https://github.com/iodeOS/ota/blob/master/iode_20174.png)

# Introduction

Welcome to iodé's official code repository.      
iodé is a privacy-focused operating System based on lineageOS, with a built-in adblocker. 
Our supported devices: Sony Xperia XZ1, Xiaomi Mi 9.  
You can also directly buy a supported device with our operating system. Our smartphones are refurbished by our specialized partners, in France.  
More information on our website: https://iode.tech/en.

# How to flash XZ1

0 - Get your unlock code from [Sony website](https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader)

1 - unlock bootloader : connect to a wifi in order to
grey-out "Unlock OEM" in developer settings

2 - adb reboot bootloader (or press VOLUME UP and plug phone while it's shut down)

3 - fastboot oem unlock 0x\<unlock code\>

4 - fastboot flash recovery [twrp-3.3.1-0-20200210-poplar_10.img](https://github.com/iodeOS/ota/releases/download/v1.0/twrp-3.3.1-0-20200210-poplar_10.img)
  
5 - press power+VOLUME DOWN until reboot in TWRP

6 - from TWRP => Wipe => Format Data: type 'yes'

7 - from TWRP => Advanced => ADB Sideload: swipe to start sideload, and issue adb sideload \<rom.zip\> (the rom image can be [found here](https://github.com/iodeOS/ota/releases/tag/v1.0))

# How to flash Mi 9

0 - Unlock your phone by following the instructions from [Xiaomi website](https://en.miui.com/unlock/)

1 - adb reboot bootloader (or press power+VOLUME DOWN)

2 - fastboot flash recovery [twrp-3.4.0-0-cepheus-mauronofrio.img](https://github.com/iodeOS/ota/releases/download/v1.0/twrp-3.4.0-0-cepheus-mauronofrio.img)

3 - press power+VOLUME UP until reboot in TWRP

4 - from TWRP => Wipe => Format Data: type 'yes'

5 - from TWRP => Advanced => ADB Sideload: swipe to start sideload, and issue adb sideload \<rom.zip\> (the rom image can be [found here](https://github.com/iodeOS/ota/releases/tag/v1.0))
