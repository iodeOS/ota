![alt text](https://github.com/iodeOS/ota/blob/master/iode_20174.png)

# Introduction

iodéOS is a privacy-focused operating system powered by LineageOS and based on the Android 10 mobile platform. iodéOS aims at protecting the user's privacy with a built-in adblocker and by freeing the smartphone from snitches.

The objectives in the conception of this ROM are threefold:

    1. To keep the stability and security level of LineageOS, by minimizing the modifications made to the system. We mainly only added a few useful options commonly found in other custom ROMs, made some cosmetic changes, modified a few default settings to prevent data leaks to Google servers.
    2. To ease a quick adoption of this ROM by new users. We especially target users that are concerned by the protection of their privacy, but are not reluctant to still use inquisitive apps like Google ones. We thus included MicroG as well as a coherent set of default apps (all open source, with one exception), and simplified the initial setup of the system. Particularly, an initialization of MicroG has been made with GCM notifications allowed by default, a privacy-friendly network location provider (DéjàVu) pre-selected, as well as Nominatim Geocoder.
    3. To provide a new and powerful way of blocking ads, malwares, data leaks of all kinds to many intrusive servers. We are developing an analyzer, tightly integrated into the system, that captures all DNS requests and network traffic, as well an user interface (the iodé app). Compared to some other well-known adblockers, this has the advantages of:
        ◦ avoiding to lock the VPN for that use,
        ◦ being independent of the kind of DNS server (encrypted or not, ...), as we capture the request before it is injected into the network,
        ◦ precisely mapping DNS requests and network packets to the Android apps that emitted (or received) them,
        ◦ deciding which apps have a filtered network usage (by default, all apps), and which ones can communicate with not recommended servers.

# What's included

## Changes in LineageOS to prevent data leaks:
    • Default DNS server: Google's DNS replaced by Quad9's 'unblocked' servers.
    • A-GPS: supl.google.com replaced by supl.vodafone.com.
    • Captive portal login: connectivitycheck.gstatic.com replaced by captiveportal.kuketz.de for connectivity check
    • Dialer: Google default option replaced by OpenStreetMap for phone number lookup.

## Pre-installed apps:
    • MicroG core apps: GmsCore, GsfProxy, FakeStore, maps API.
    • NLP backends for MicroG : DejaVuNLPBackend (default), MozillaNLPBackend, AppleNLPBackend, RadioCellsNLPBackend, NominatimNLPBackend
    • App stores : FDroid (with F-Droid Privileged Extension) and Aurora Store.
    • Browser: Qwant
    • SMS: QKSMS instead of Lineage's default SMS app.
    • Maps/navigation: Magic Earth GPS & Navigation (the only one free but not open source)
    • PDF: Pdf Viewer Plus
    • Personal notes: Carnet
    • {Ad/Malware/Data leak}-blocker: iodé
    
## Useful options from other custom ROMs:
    • Smart charging (disables charging when a given level is reached, to protect battery health)
    • Fingerprint vibration toggle
    • Swipe down to clear all in recent apps



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
