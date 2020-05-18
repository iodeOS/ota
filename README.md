![alt text](https://github.com/iodeOS/ota/blob/master/iode_20174.png)

# Introduction

Welcome to iodé's official code repository. 
iodé is a Lineage operating System with built-in adblocker. Due to strategic and logistic reasons, our source code is yet to be open source. We will progressively open our source code in the forthcoming months. 
In the meantime, feel free to test out our operating system on the supported devices: Sony Xperia XZ1, Xiaomi Mi 9.
You can also directly buy a supported device with our operating system. Our smartphones are refurbished by specialized partners, in France.
More information on our website: https://iode.tech/en.

# How to flash XZ1

https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader


1 - unlock bootloader : ! connect to a wifi in order to
grey-out "Unlock OEM'

2 - adb reboot bootloader ( or VOLUME UP and plug phone while it's shut down)

3 - fastboot oem unlock 0x<unlock code>

4 - fastboot flash recovery twrp.img (the image can be found in this repository)
  
5 - power+VOLUME DOWN until reboot in TWRP

6- from TWRP => format data 

7 - from TWRP => adb sideload rom.zip (the rom image can be found in this repository)
