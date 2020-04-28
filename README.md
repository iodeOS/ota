# ota


# How to flash XZ1

tuto : https://clickitornot.com/install-twrp-recovery-root-sony-xperia-xz1/


1 - unlock bootloader : ! connect to a wifi in order to
grey-out "Unlock OEM'

(2 - enable USB DEBUGGING)

3 - adb reboot bootloader ( or VOL+ and plug phone while it's shut down)


4 - fastboot oem unlock 0x<unlock code>

5 - fastboot flash recovery recovery.img
  
6 - power+VolDown until reboot in TWRP

7- from TWRP => format data 

8 - from TWRP => adb sideload rom.zip
