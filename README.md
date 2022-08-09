![alt text](pictures/iode_20174.png)

# Introduction

iodéOS is a privacy-focused operating system powered by LineageOS and based on the Android mobile platform. iodéOS aims at protecting the user's privacy with a built-in adblocker and by freeing the smartphone from snitches.

The objectives in the conception of this ROM are threefold:

1. To keep the stability and security level of LineageOS, by minimizing the modifications made to the system. Apart the system modifications required by the adblocker, we mainly only added a few useful options commonly found in other custom ROMs, made some cosmetic changes, modified a few default settings to prevent data leaks to Google servers.
1. To ease a quick adoption of this ROM by new users. We especially target users that are concerned by the protection of their privacy, but are not reluctant to still use inquisitive apps like Google ones. We thus included MicroG as well as a coherent set of default apps, and simplified the initial setup of the system. Particularly, an initialization of MicroG has been made with GCM notifications allowed by default, a privacy-friendly network location provider (DéjàVu) pre-selected, as well as Nominatim Geocoder.
1. To provide a new and powerful way of blocking ads, malwares, data leaks of all kinds to many intrusive servers. We are developing an analyzer, tightly integrated into the system, that captures all DNS requests and network traffic, as well as a user interface (the iodé app). Compared to some other well-known adblockers, this has the advantages of:
    * Avoiding to lock the VPN for that use. You can even use another adblocker that uses VPN technology alongside our blocker.
    * Being independent of the kind of DNS server used by the system or set by an independent app: classical DNS on UDP port 53 or any other one, DNS over TLS (DoT), DNS over HTTPS (DoH), ..., as we capture the DNS requests before they are transmitted to the system function that emits the DNS request. What we do not support, is DoH when it is natively built into applications, i.e. when an app communicates directly with a DoH server, without asking name resolution to the system. It would require to decrypt HTTPS packets between such an app and the DoH server, which may create a big security hole.
    * Precisely mapping DNS requests and network packets to the Android apps that emitted (or received) them.
    * Deciding which apps have a filtered network usage (by default, all apps), and which ones can communicate with blacklisted servers.

Since its first versions, we added many features to the iodé blocker: several levels of protection, fine-grained control over the hosts that should be blocked or authorized, displaying statistics on a map to see the quantity of data exchanged to which countries, clearing statistics... We are actively developing the blocker, and new functionalities will be regularly added.

<img src="https://user-images.githubusercontent.com/52780214/156890648-ff6f162f-0582-455e-8fac-57314d1650a9.png" alt="Home" width="250"/><img src="https://user-images.githubusercontent.com/52780214/156890758-cd456584-ab77-430f-9c08-cd7d29e7290f.png" alt="Report" width="250"/><img src="https://user-images.githubusercontent.com/52780214/156890861-9d699ce9-68b3-43bf-b078-96e00cd1d4f3.png" alt="Report Netflix" width="250"/><img src="https://user-images.githubusercontent.com/52780214/156890884-4cb962d4-08e7-4ee3-a49e-2f8197e55e1f.png" alt="Report Facebook" width="250"/><img src="https://user-images.githubusercontent.com/52780214/156890772-e2be7fcb-5e79-4c16-a8bf-b88fd2af4166.png" alt="Map" width="250"/><img src="https://user-images.githubusercontent.com/52780214/156890791-0e812e3a-c2f8-4551-8704-e010dc0f9ad2.png" alt="Stream" width="250"/><img src="https://user-images.githubusercontent.com/52780214/156890797-1590d85c-4d06-4ff4-b01a-463b55cdd292.png" alt="Settings" width="250"/><img src="https://user-images.githubusercontent.com/52780214/156890957-7fd08951-9667-42c6-a085-e64d1eba24b5.png" alt="Customized protection" width="250"/>

# What's included

## Changes in LineageOS to prevent data leaks:

* Default DNS server: Google's DNS replaced by Quad9's 'unblocked' servers in all parts of the system.
* A-GPS: patches to avoid leaking personnal information like IMSI to supl server.
* Captive portal login: connectivitycheck.gstatic.com replaced by captiveportal.kuketz.de for connectivity check.
* Dialer: Google default option replaced by OpenStreetMap for phone number lookup.


## Pre-installed apps:

We included many useful default apps, but our choice cannot suit everyone; so we added the possibility to remove them. It can be done at the end of the phone setup, or at any time by going to Parameters -> Apps & Notifications -> Preinstalled apps.

* MicroG core apps: GmsCore, GsfProxy, FakeStore.
* NLP backends for MicroG : DejaVuNLPBackend (default), MozillaNLPBackend, AppleNLPBackend, RadioCellsNLPBackend, NominatimNLPBackend
* App stores : FDroid (with F-Droid Privileged Extension) and Aurora Store.
* Browser: our own fork of Firefox (with Qwant as default search engine, many other ones added, telemetry disabled, parts of telemetry code removed) instead of * * Lineage’s default browser Jelly.
* SMS: QKSMS instead of Lineage's default SMS app.
* Email: p≡p (Pretty Easy Privacy).
* Camera: our own fork of Open Camera, with a few tweaks.
* Maps/navigation: Magic Earth GPS & Navigation (the only one free but not open source).
* Keyboard: OpenBoard instead of AOSP keyboard.
* PDF: Pdf Viewer Plus.
* Personnal notes: Carnet.
* {Ad/Malware/Data leak}-blocker: iodé.
* News: to keep users informed about our developments, as well as a FAQ.
* Meteo: Geometric Weather.

## Useful options from other custom ROMs:
* Smart charging (disables charging when a given level is reached, to protect battery health).
* Fingerprint vibration toggle.

# How to flash Fairphone (FP3, FP3+, FP4)

## FP3, FP3+

1. Update the stock firmware to the latest
1. Unlock your phone by following the instructions from [Fairphone website](https://www.fairphone.com/en/bootloader-unlocking-code-for-fairphone-3/)
1. adb reboot bootloader (or press VOLUME DOWN and plug phone while it's shut down)
1. fastboot oem unlock
1. fastboot flash boot &lt;[recovery for FP3(+)](https://github.com/iodeOS/ota/releases/tag/v3-FP3)&gt;
1. press POWER+VOLUME UP until reboot in recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;[iodéOS for FP3(+)](https://github.com/iodeOS/ota/releases/tag/v3-FP3)&gt;
1. fastboot oem lock
1. Boot, and in developer settings uncheck "OEM unlocking"

# FP4

1. Update the stock firmware to the latest
1. Unlock your phone by following the instructions from [Fairphone website](https://www.fairphone.com/en/bootloader-unlocking-code-for-fairphone-3/), but **do not unlock critical partitions** (do not execute 'fastboot flashing unlock_critical').
1. adb reboot bootloader (or press VOLUME DOWN and plug phone while it's shut down)
1. fastboot flashing unlock
1. fastboot flash recovery_a &lt;[recovery for FP4](https://github.com/iodeOS/ota/releases/tag/v3-FP4)&gt;  
   fastboot flash recovery_b &lt;[recovery for FP4](https://github.com/iodeOS/ota/releases/tag/v3-FP4)&gt;
1. In order to relock bootloader: fastboot flash avb_custom_key &lt;[avb_custom_key-FP4.bin](https://github.com/iodeOS/ota/releases/download/v3-FP4/avb_custom_key-FP4.bin)&gt;
1. press POWER+VOLUME UP until reboot in recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;[iodéOS for FP4](https://github.com/iodeOS/ota/releases/tag/v3-FP4)&gt;
1. Reboot to booloader
1  Execute 'fastboot flashing get_unlock_ability'. It it returns 'get_unlock_ability: 0': **do not try to relock the bootloader (steps below)**
1. If previous step returned 'get_unlock_ability: 1': fastboot flashing lock
1. Boot, and in developer settings uncheck "OEM unlocking"

# How to flash Teracube

## 2E 2022 batch (emerald)

1. Update the stock firmware to the latest
1. Unlock OEM in developer settings
1. Reboot to bootloader
1. fastboot flashing unlock
1. fastboot flash boot &lt;[recovery for 2E](https://github.com/iodeOS/ota/releases/tag/v2-emerald)&gt;
1. Reboot to recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;[iodéOS for 2E](https://github.com/iodeOS/ota/releases/tag/v2-emerald)&gt;

## 2E 2021 batch

1. Update the stock firmware to the latest
1. Unlock OEM in developer settings
1. Reboot to bootloader
1. fastboot flashing unlock
1. fastboot flash recovery &lt;[recovery for 2E](https://github.com/iodeOS/ota/releases/tag/v2-2e)&gt;
1. Reboot to recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;[iodéOS for 2E](https://github.com/iodeOS/ota/releases/tag/v2-2e)&gt;



# How to flash Xiaomi (Mi9, Mi 10 LITE, Mi 10T (Pro), Redmi K30S Ultra)

1. Update the stock firmware to the latest
1. Unlock your phone by following the instructions from [Xiaomi website](https://en.miui.com/unlock/download_en.html)
1. adb reboot bootloader (or press power+VOLUME DOWN)
1. fastboot flash recovery [iodé mi9 recovery image](https://github.com/iodeOS/ota/releases/tag/v3-cepheus) | [iodé Mi 10 LITE recovery image](https://github.com/iodeOS/ota/releases/tag/v3-monet) | [iodé Mi10T (pro) recovery image](https://github.com/iodeOS/ota/releases/tag/v3-apollon)
1. Press POWER+VOLUME UP until reboot in recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;rom.zip&gt; ([iodéOS for Mi 9](https://github.com/iodeOS/ota/releases/tag/v3-cepheus) | [iodéOS for Mi 10 lite](https://github.com/iodeOS/ota/releases/tag/v3-monet) | [iodéOS for Mi 10T (pro) zip ROM ](https://github.com/iodeOS/ota/releases/tag/v3-apollon))

# How to flash Samsung

## A5 (2017), A7 (2017)

1. Update the stock firmware to the latest
1. Unlock OEM in developer settings
1. Reboot and press power/vol-/home buttons altogether.
1. Flash [recovery for A5](https://github.com/iodeOS/ota/releases/tag/v2-a5y17lte) | [recovery for A7](https://github.com/iodeOS/ota/releases/tag/v2-a7y17lte) with command: heimdall flash --RECOVERY <recovery_filename>.img
1. As soon as the flash ends, quickly press power/vol+/home buttons altogether to directly reboot to recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Advanced => ADB Sideload: swipe to start sideload, and issue adb sideload &lt;rom.zip&gt; ([iodéOS for A5](https://github.com/iodeOS/ota/releases/tag/v2-a5y17lte) | [iodéOS for A7](https://github.com/iodeOS/ota/releases/tag/v2-a7y17lte))

## S9, S9+, Note9

1. Update the stock firmware to the latest
1. Unlock OEM in developer settings
1. At reboot, follow the setup wizard, make sure to be connected to the internet, then activate developer options
1. Activate adb and type: 'adb reboot bootloader', or press  power/vol-/bixby buttons altogether.
1. Flash lineageOS [recovery for S9](https://github.com/iodeOS/ota/releases/download/v3-starlte/recovery-starlte.img) or  [recovery for S9+](https://github.com/iodeOS/ota/releases/download/v3-star2lte/recovery-star2lte.img) or [recovery for Note9](https://github.com/iodeOS/ota/releases/download/v3-crownlte/recovery-crownlte.img) with command: heimdall flash --RECOVERY <recovery_filename>.img
1. As soon as the flash ends, quickly press power/vol+/bixby buttons altogether to directly reboot to recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;rom.zip&gt; ([iodéOS for S9](https://github.com/iodeOS/ota/releases/tag/v3-starlte) | [iodéOS for S9+](https://github.com/iodeOS/ota/releases/tag/v3-star2lte) | [iodéOS for Note9](https://github.com/iodeOS/ota/releases/tag/v3-crownlte))

## S10, S10e, S10+

1. Update the stock firmware to the latest
1. Unlock OEM in developer settings
1. Activate adb and type: 'adb reboot bootloader', or shut down phone &  press vol-/bixby buttons altogether while plugging to computer
1. In Download Mode (DL), long press Vol+ and unlock bootloader
1. Reboot to DL mode & flash [recovery for S10](https://github.com/iodeOS/ota/releases/tag/v3-beyond1lte) | [recovery for S10e](https://github.com/iodeOS/ota/releases/tag/v3-beyond0lte) | [recovery for S10+](https://github.com/iodeOS/ota/releases/tag/v3-beyond2lte) with command: heimdall flash --RECOVERY <recovery_filename>.img
1. As soon as the flash ends, quickly press power/vol+/bixby buttons altogether to directly reboot to recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;rom.zip&gt; ([iodéOS for S10](https://github.com/iodeOS/ota/releases/tag/v3-beyond1lte) | [iodéOS for S10e](https://github.com/iodeOS/ota/releases/tag/v3-beyond0lte) | [iodéOS for S10+](https://github.com/iodeOS/ota/releases/tag/v3-beyond2lte))

## Note 10, Note 10+

1. Update the stock firmware to the latest
1. Unlock OEM in developer settings
1. Activate adb and type: 'adb reboot bootloader', or shut down phone &  press vol+/vol- buttons altogether while plugging to computer
1. In Download Mode (DL), long press Vol+ and unlock bootloader
1. Reboot to DL mode & flash [recovery for Note 10](https://github.com/iodeOS/ota/releases/tag/v3-d1) | [recovery for Note 10+](https://github.com/iodeOS/ota/releases/tag/v3-d2s) with command: heimdall flash --RECOVERY <recovery_filename>.img
1. As soon as the flash ends, quickly press power/vol+/bixby buttons altogether to directly reboot to recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;rom.zip&gt; ([iodéOS for Note 10](https://github.com/iodeOS/ota/releases/tag/v3-d1) | [iodéOS for Note 10+](https://github.com/iodeOS/ota/releases/tag/v3-d2s))

# How to flash Sony Xperia (XA2, XZ1, XZ2, XZ3)

1. Get your unlock code from [Sony website](https://developer.sony.com/develop/open-devices/get-started/unlock-bootloader)
1. Unlock bootloader: connect to a wifi in order to grey-out "Unlock OEM" in developer settings
1. adb reboot bootloader (or press VOLUME UP and plug phone while it's shut down)
1. fastboot oem unlock 0x&lt;unlock code&gt;
1. Following your device:
   * XA2:  
fastboot flash boot_a [recovery-pioneer.img](https://github.com/iodeOS/ota/releases/tag/v3-pioneer)  
fastboot flash boot_b [recovery-pioneer.img](https://github.com/iodeOS/ota/releases/tag/v3-pioneer)
   * XZ1:  
fastboot flash recovery [recovery-poplar.img](https://github.com/iodeOS/ota/releases/tag/v3-poplar)
   * XZ2:  
fastboot flash boot_a [recovery-akari.img](https://github.com/iodeOS/ota/releases/tag/v3-akari)  
fastboot flash boot_b [recovery-akari.img](https://github.com/iodeOS/ota/releases/tag/v3-akari)
   * XZ3:  
fastboot flash boot_a [recovery-akatsuki.img](https://github.com/iodeOS/ota/releases/tag/v3-akatsuki)  
fastboot flash boot_b [recovery-akatsuki.img](https://github.com/iodeOS/ota/releases/tag/v3-akatsuki)


## XA2, XZ1, XZ2

1. Unplug the phone
1. press POWER+VOLUME DOWN until reboot in recovery
1. From recovery => Factory reset => Format Data/factory reset
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;rom.zip&gt; ([iodéOS for XA2](https://github.com/iodeOS/ota/releases/tag/v3-pioneer) | [iodéOS for XZ1](https://github.com/iodeOS/ota/releases/tag/v3-poplar) | [iodéOS for XZ2](https://github.com/iodeOS/ota/releases/tag/v3-akari))

## XZ3 

1. Unplug the phone
1. press POWER+VOLUME DOWN until reboot in recovery
1. From recovery => Factory reset  => Format Data
1. From recovery => Apply update => Apply from ADB => adb sideload &lt;[iodéOS for XZ3](https://github.com/iodeOS/ota/releases/tag/v3-akatsuki)&gt;
