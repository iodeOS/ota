![alt text](pictures/iode_20174.png)

# Introduction

iodéOS is a privacy-focused operating system powered by LineageOS and based on the Android 10 mobile platform. iodéOS aims at protecting the user's privacy with a built-in adblocker and by freeing the smartphone from snitches.

The objectives in the conception of this ROM are threefold:

<ol>
    <li>To keep the stability and security level of LineageOS, by minimizing the modifications made to the system. Apart the system modifications required by the adblocker, we mainly only added a few useful options commonly found in other custom ROMs, made some cosmetic changes, modified a few default settings to prevent data leaks to Google servers.</li>
    <li> To ease a quick adoption of this ROM by new users. We especially target users that are concerned by the protection of their privacy, but are not reluctant to still use inquisitive apps like Google ones. We thus included MicroG as well as a coherent set of default apps (all open source, with one exception), and simplified the initial setup of the system. Particularly, an initialization of MicroG has been made with GCM notifications allowed by default, a privacy-friendly network location provider (DéjàVu) pre-selected, as well as Nominatim Geocoder.</li>
    <li> To provide a new and powerful way of blocking ads, malwares, data leaks of all kinds to many intrusive servers. We are developing an analyzer, tightly integrated into the system, that captures all DNS requests and network traffic, as well as a user interface (the iodé app). Compared to some other well-known adblockers, this has the advantages of:
    <ul>
        <li>Avoiding to lock the VPN for that use. You can even use another adblocker that uses VPN technology alongside our blocker.</li>
        <li>Being independent of the kind of DNS server used by the system or set by an independent app: classical DNS on UDP port 53 or any other one, DNS over TLS (DoT), DNS over HTTPS (DoH), ..., as we capture the DNS requests before they are transmitted to the system function that emits the DNS request. What we do not support, is DoH when it is natively built into applications, i.e. when an app communicates directly with a DoH server, without asking name resolution to the system. It would require to decrypt HTTPS packets between such an app and the DoH server, which may create a big security hole.</li>
        <li>Precisely mapping DNS requests and network packets to the Android apps that emitted (or received) them.</li>
        <li>Deciding which apps have a filtered network usage (by default, all apps), and which ones can communicate with blacklisted servers.</li>
    </ul>
</ol>

# What's included

## Changes in LineageOS to prevent data leaks:
<ul>
    <li>Default DNS server: Google's DNS replaced by Quad9's 'unblocked' servers.</li>
    <li>A-GPS: supl.google.com replaced by supl.vodafone.com.</li>
    <li>Captive portal login: connectivitycheck.gstatic.com replaced by captiveportal.kuketz.de for connectivity check</li>
    <li>Dialer: Google default option replaced by OpenStreetMap for phone number lookup.</li>
</ul>

## Pre-installed apps:
<ul>
    <li>MicroG core apps: GmsCore, GsfProxy, FakeStore, maps API.</li>
    <li>NLP backends for MicroG : DejaVuNLPBackend (default), MozillaNLPBackend, AppleNLPBackend, RadioCellsNLPBackend, NominatimNLPBackend</li>
    <li>App stores : FDroid (with F-Droid Privileged Extension) and Aurora Store.</li>
    <li>Browser: Qwant instead of Lineage’s default browser Jelly.</li>
    <li>SMS: QKSMS instead of Lineage's default SMS app.</li>
    <li>Maps/navigation: Magic Earth GPS & Navigation (the only one free but not open source).</li>
    <li>Keyboard: OpenBoard instead of AOSP keyboard.</li>
    <li>PDF: Pdf Viewer Plus.</li>
    <li>Personal notes: Carnet.</li>
    <li>{Ad/Malware/Data leak}-blocker: iodé.</li>
</ul>

## Useful options from other custom ROMs:
<ul>
    <li>Smart charging (disables charging when a given level is reached, to protect battery health).</li>
    <li>Fingerprint vibration toggle.</li>
    <li>Swipe down to clear all in recent apps.</li>
</ul>



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

2 - fastboot flash recovery [twrp-3.4.0-0-cepheus-mauronofrio.img](https://github.com/iodeOS/ota/releases/download/v1.0-cepheus/twrp-3.4.0-0-cepheus-mauronofrio.img)

3 - press power+VOLUME UP until reboot in TWRP

4 - from TWRP => Wipe => Format Data: type 'yes'

5 - from TWRP => Advanced => ADB Sideload: swipe to start sideload, and issue adb sideload \<rom.zip\> (the rom image can be [found here](https://github.com/iodeOS/ota/releases/tag/v1.0-cepheus))
