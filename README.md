![alt text](pictures/iode_20174.png)

# Introduction

iodéOS is a privacy-focused operating system powered by LineageOS and based on the Android mobile platform. iodéOS aims at protecting the user's privacy with a built-in adblocker and by freeing the smartphone from snitches.

The objectives in the conception of this ROM are threefold:

1. To keep the stability and security level of LineageOS, by minimizing the modifications made to the system. Apart the system modifications required by the adblocker, we mainly only added a few useful options commonly found in other custom ROMs, made some cosmetic changes, modified a few default settings to prevent data leaks to Google servers.
1. To ease a quick adoption of this ROM by new users. We especially target users that are concerned by the protection of their privacy, but are not reluctant to still use inquisitive apps like Google ones. We thus included MicroG as well as a coherent set of default apps (all open source, with one exception), and simplified the initial setup of the system. Particularly, an initialization of MicroG has been made with GCM notifications allowed by default, a privacy-friendly network location provider (DéjàVu) pre-selected, as well as Nominatim Geocoder.
1. To provide a new and powerful way of blocking ads, malwares, data leaks of all kinds to many intrusive servers. We are developing an analyzer, tightly integrated into the system, that captures all DNS requests and network traffic, as well as a user interface (the iodé app). Compared to some other well-known adblockers, this has the advantages of:
   * Avoiding to lock the VPN for that use. You can even use another adblocker that uses VPN technology alongside our blocker.
   * Being independent of the kind of DNS server used by the system or set by an independent app: classical DNS on UDP port 53 or any other one, DNS over TLS (DoT), DNS over HTTPS (DoH), ..., as we capture the DNS requests before they are transmitted to the system function that emits the DNS request. What we do not support, is DoH when it is natively built into applications, i.e. when an app communicates directly with a DoH server, without asking name resolution to the system. It would require to decrypt HTTPS packets between such an app and the DoH server, which may create a big security hole.
   * Precisely mapping DNS requests and network packets to the Android apps that emitted (or received) them.
   * Deciding which apps have a filtered network usage (by default, all apps), and which ones can communicate with blacklisted servers.

# What's included

## Changes in LineageOS to prevent data leaks:
* Default DNS server: Google's DNS replaced by Quad9's 'unblocked' servers.
* A-GPS: supl.google.com replaced by supl.vodafone.com.
* Captive portal login: connectivitycheck.gstatic.com replaced by captiveportal.kuketz.de for connectivity check
* Dialer: Google default option replaced by OpenStreetMap for phone number lookup.

## Pre-installed apps:
* MicroG core apps: GmsCore, GsfProxy, FakeStore, maps API.
* NLP backends for MicroG : DejaVuNLPBackend (default), MozillaNLPBackend, AppleNLPBackend, RadioCellsNLPBackend, NominatimNLPBackend
* App stores : FDroid (with F-Droid Privileged Extension) and Aurora Store.
* Browser: iodé Browser (based on Firefox) instead of Lineage’s default browser Jelly.
* SMS: QKSMS instead of Lineage's default SMS app.
* Maps/navigation: Magic Earth GPS & Navigation (the only one free but not open source).
* Keyboard: OpenBoard instead of AOSP keyboard.
* PDF: Pdf Viewer Plus.
* Personal notes: Carnet.
* {Ad/Malware/Data leak}-blocker: iodé.
* News: to keep users informed about our developments, as well as a FAQ.

## Useful options from other custom ROMs:
* Smart charging (disables charging when a given level is reached, to protect battery health).
* Fingerprint vibration toggle.
* Swipe down to clear all in recent apps.

# How to flash Fairphone (FP3, FP3+)

1. Update the stock firmware to the latest
1. Unlock your phone by following the instructions from [Fairphone website](https://www.fairphone.com/en/bootloader-unlocking-code-for-fairphone-3/)
1. adb reboot bootloader (or press VOLUME DOWN and plug phone while it's shut down)
1. fastboot oem unlock
1. fastboot flash boot [recovery for FP3(+)](https://github.com/iodeOS/ota/releases/tag/v2-FP3)
1. press POWER+VOLUME UP until reboot in recovery
1. Sideload flash [iodéOS for FP3(+)](https://github.com/iodeOS/ota/releases/tag/v2-FP3)
1. Format data
1. fastboot oem lock


# How to flash Teracube (2E)

1. Update the stock firmware to the latest
2. Unlock your phone & install TWRP [from Teracube’s forum](https://community.myteracube.com/t/advanced-users-only-twrp-recovery-root-for-teracube-2e/1729)
3. Sideload flash [iodéOS for E2](https://github.com/iodeOS/ota/releases/tag/v1-2e)
4. Format data



# How to flash Xiaomi (Mi 9)

1. Update the stock firmware to the latest
1. Unlock your phone by following the instructions from [Xiaomi website](https://en.miui.com/unlock/)
1. adb reboot bootloader (or press power+VOLUME DOWN)
1. fastboot flash recovery [twrp-3.4.0-0-cepheus-mauronofrio.img](https://github.com/iodeOS/ota/releases/download/v1-cepheus/twrp-3.4.0-0-cepheus-mauronofrio.img)
1. Press POWER+VOLUME UP until reboot in TWRP
1. From TWRP => Wipe => Format Data: type 'yes'
1. From TWRP => Advanced => ADB Sideload: swipe to start sideload, and issue adb sideload &lt;rom.zip&gt; (the rom image can be [found here](https://github.com/iodeOS/ota/releases/tag/v1-cepheus))

# How to flash Samsung

## A5 (2017), A7 (2017)

1. Update the stock firmware to the latest
1. Unlock OEM in developer settings
1. Reboot and press power/vol-/home buttons altogether.
1. Flash [recovery for A5](https://github.com/iodeOS/ota/releases/tag/v2-a5y17lte) | [recovery for A7](https://github.com/iodeOS/ota/releases/tag/v2-a7y17lte) with command: heimdall flash --RECOVERY <recovery_filename>.img
1. As soon as the flash ends, quickly press power/vol+/home buttons altogether to directly reboot to recovery
1. From TWRP => Wipe => Format Data: type 'yes'
1. From TWRP => Advanced => ADB Sideload: swipe to start sideload, and issue adb sideload &lt;rom.zip&gt; [iodé for A5](https://github.com/iodeOS/ota/releases/tag/v2-a5y17lte) | [iodé for A7](https://github.com/iodeOS/ota/releases/tag/v2-a7y17lte)

## S9, S9+, Note9

1. Update the stock firmware to the latest
1. Unlock OEM in developer settings
1. At reboot, follow the setup wizard, make sure to be connected to the internet, then activate developer options
1. Activate adb and type: 'adb reboot bootloader', or press  power/vol-/bixby buttons altogether.
1. Flash lineageOS [recovery for S9](https://github.com/iodeOS/ota/releases/download/v2-starlte/recovery-starlte.img) or  [recovery for S9+](https://github.com/iodeOS/ota/releases/download/v2-star2lte/recovery-star2lte.img) or [recovery for Note9](https://github.com/iodeOS/ota/releases/download/v2-crownlte/recovery-crownlte.img) with command: heimdall flash --RECOVERY <recovery_filename>.img
1. As soon as the flash ends, quickly press power/vol+/bixby buttons altogether to directly reboot to recovery
1. Sideload flash [iodéOS for s9](https://github.com/iodeOS/ota/releases/tag/v2-starlte) or [iodéOS for s9+](https://github.com/iodeOS/ota/releases/tag/v2-star2lte) or or [iodéOS for Note9](https://github.com/iodeOS/ota/releases/tag/v2-crownlte)
1. Format data

## S10, S10e, S10+

1. Update the stock firmware to the latest
2. Unlock OEM in developer settings
3. Activate adb and type: 'adb reboot bootloader', or shut down phone &  press vol-/bixby buttons altogether while plugging to computer
4. In Download Mode (DL), long press Vol+ and unlock bootloader
5. Reboot to DL mode & flash [recovery for S10](https://github.com/iodeOS/ota/releases/tag/v2-beyond1lte) | [recovery for S10e](https://github.com/iodeOS/ota/releases/tag/v2-beyond0lte) | [recovery for S10+](https://github.com/iodeOS/ota/releases/tag/v2-beyond2lte) with command: heimdall flash --RECOVERY <recovery_filename>.img
6. As soon as the flash ends, quickly press power/vol+/bixby buttons altogether to directly reboot to recovery
7. Sideload flash [iodéOS for S10](https://github.com/iodeOS/ota/releases/tag/v2-beyond1lte) | [iodéOS for S10e](https://github.com/iodeOS/ota/releases/tag/v2-beyond0lte) | [iodéOS for S10+](https://github.com/iodeOS/ota/releases/tag/v2-beyond2lte)
8. Format data

## Note 10, Note 10+

1. Update the stock firmware to the latest
2. Unlock OEM in developer settings
3. Activate adb and type: 'adb reboot bootloader', or shut down phone &  press vol+/vol- buttons altogether while plugging to computer
4. In Download Mode (DL), long press Vol+ and unlock bootloader
5. Reboot to DL mode & flash [recovery for Note 10](https://github.com/iodeOS/ota/releases/tag/v2-d1) | [recovery for Note 10+](https://github.com/iodeOS/ota/releases/tag/v2-d2s) with command: heimdall flash --RECOVERY <recovery_filename>.img
6. As soon as the flash ends, quickly press power/vol+/bixby buttons altogether to directly reboot to recovery
7. Sideload flash iodéOS for [iodéOS for Note 10](https://github.com/iodeOS/ota/releases/tag/v2-d1) | [iodéOS for Note 10+](https://github.com/iodeOS/ota/releases/tag/v2-d2s)
8. Format data

# How to flash Sony Xperia (XA2, XZ1, XZ2, XZ3)

1. Get your unlock code from [Sony website](https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader)
1. Unlock bootloader: connect to a wifi in order to grey-out "Unlock OEM" in developer settings
1. adb reboot bootloader (or press VOLUME UP and plug phone while it's shut down)
1. fastboot oem unlock 0x&lt;unlock code&gt;
1. Following your device:
   * XA2:  
 fastboot flash boot_a [boot-pioneer.img](https://github.com/iodeOS/ota/releases/download/v2-pioneer/boot-pioneer.img)  
 fastboot flash boot_b [boot-pioneer.img](https://github.com/iodeOS/ota/releases/download/v2-pioneer/boot-pioneer.img)
   * XZ1:  
fastboot flash recovery [recovery-poplar.img](https://github.com/iodeOS/ota/releases/download/v2-poplar/recovery-poplar.img)
   * XZ2:  
fastboot flash boot_a [boot-akari.img](https://github.com/iodeOS/ota/releases/download/v2-akari/boot-akari.img)  
fastboot flash boot_b [boot-akari.img](https://github.com/iodeOS/ota/releases/download/v2-akari/boot-akari.img)
   * XZ3:  
fastboot flash boot_a [boot-akatsuki.img](https://github.com/iodeOS/ota/releases/download/v2-akatsuki/boot-akatsuki.img)  
fastboot flash boot_b [boot-akatsuki.img](https://github.com/iodeOS/ota/releases/download/v2-akatsuki/boot-akatsuki.img)


## XA2, XZ1, XZ2

1. Unplug the phone
1. press POWER+VOLUME DOWN until reboot in TWRP
1. From TWRP => Wipe => Format Data: type 'yes'
1. From TWRP => Advanced => ADB Sideload: swipe to start sideload, and issue adb sideload &lt;rom.zip&gt; (the rom image can be found here: [XA2](https://github.com/iodeOS/ota/releases/tag/v2-pioneer), [XZ1](https://github.com/iodeOS/ota/releases/tag/v2-poplar), [XZ2](https://github.com/iodeOS/ota/releases/tag/v2-akari))

## XZ3 

1. Unplug the phone
1. press POWER+VOLUME DOWN until reboot in recovery
2. From recovery => Factory reset  => Format Data
3. From recovery => Apply update => Apply from ADB => ADB Sideload [iodé for XZ3](https://github.com/iodeOS/ota/releases/tag/v2-akatsuki)
