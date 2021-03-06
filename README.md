# H81M-DS2-Hackintosh

Just a EFI folder for mainboard Gigabyte H81M-DS2 (rev3.0)

# My PC specification:
+ Mainboard Gigabyte H81M-DS2 (rev3.0)
+ CPU: Intel Pentium G3250 (Haswell Refresh, 3,20GHz, 2 core) (FakeCPUID set to 0x0306A9)
+ RAM: 4GB
+ GPU: NVIDIA Geforce GT 730 (GK208B, 128bit, 2GB GDDR5), natively support in Mojave, Catalina.
+ Disk: Netac SSD 128GB (Windows installed), WD Blue 256GB (macOS 10.13.6 installed), dualboot with Bootcamp.
+ Network: Realtek RTL8111 (best layout-id in my build is 3)
+ Sound: Realtek ALC887
+ Current macOS installed on this build: macOS High Sierra (17G14019)
+ SMBIOS: iMac14,1 or iMac14,2 (iMac15,1 for Big Sur)

# This specification was run:
+ Lastest Windows 10 build
+ macOS Big Sur
+ macOS Big Sur Beta 5
+ macOS Catalina
+ macOS Mojave
+ macOS High Sierra
+ Mac OS X El Captain

# What is working:
+ Microphone (pink jack input)
+ Speaker (green jack input) 
+ Ethernet (en0)
+ App Store
+ iBooks
+ iCloud Drive
+ Graphics (GT730 is natively support in Catalina, other NVIDIA card please check when install Catalina.)
+ Intel QuickSync/Hardware Acceleration (use SMBIOS iMac14,1 won't work, use iMac14,2 instead)
+ USB 2.0
+ USB 3.0
+ Airdrop (not test yet cuz i don't have external internet/bluetooth card)
+ AirPlay (same as Airdrop)
+ Handoff (same as Airdrop)
+ iMessages (not fix yet)
+ FaceTime (not fix yet)

# Guide for Pentium
+ Because macOS don't support Pentium, Celeron CPUs, so we need a use the Fake CPUID patches for that CPU to boot in MacOS:

Clover tutorial:

+ In Clover bootloader, press O, go to Binary patching, set the FakeCPUID to: 0x0306A0 or 0x0306A9 (both have been tested by me)
+ Or you can set FakeCPUID in Clover Configurator by going to Kernel and Kext Patches section, set the FakeCPUID to 0x0306A0 or 0x0306A9 (this will save your time when boot installed macOS in your hard drive)

OpenCore tutorial:
+ In your config.plist, goto Kernel > Emulate add these data into require value
```
CpuidData: A9060300 00000000 00000000 00000000
CpuidMask: FFFFFFFF 00000000 00000000 00000000
```

# Attention:
+ SIP was completely disabled on both OC and Clover EFI
+ DummyPowerManagement is ENABLE in OC, this is not follow the Vanilia OC Guide (because my CPU require the function like NullCPUPowerManagement.kext to boot in, if you have any issues, just delete NullCPUPowerManagement.kext if you using Clover or Disable the DummyPowerManagement in OC config.plist at Kernel > Quirk
+ NVRAM > Writeflash is DISABLE in OC, this is not follow the Vanilia OC Guide (I don't know why this need to Disable, if not, the bootloader hang in OC: Watchdog status is 0. Change this value if your hack have issues.)
+ I'm using HFSPlusLegacy.efi instead of HFSPlus.efi (the same problem with NVRAM > Writeflash, mentioned above.)
+ These both above problem are described/fix like this [Reddit](https://www.reddit.com/r/hackintosh/comments/gn41rk/stuck_in_oc_watchdog_status_is_0/) post.

# Post-install:
+ (Only High Sierra) If you have NVIDIA graphics card, use this terminal command to install Web driver

```
bash <(curl -s https://raw.githubusercontent.com/Benjamin-Dobell/nvidia-update/master/nvidia-update.sh)
```
Code by [Benjamin-Dobell](https://github.com/Benjamin-Dobell/), use this [link](https://github.com/Benjamin-Dobell/nvidia-update/) to learn more.
+ (Only High Sierra) I installed CUDA driver too, get this in [here](https://www.nvidia.com/en-us/drivers/cuda/mac-driver-archive/)
+ Don't forget to add nvda_drv=1 in boot-args and select NVIDIAWeb on System Parameters (Clover Configuator)

# Credit
+ [hackintosh.vn](https://hackintosh.vn) for Vietnamese guides
+ [Olarila](https://olarila.com) for Clover English guides, configs
+ [Benjamin-Dobell](https://github.com/Benjamin-Dobell/) for NVIDIA Web scripts
+ [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) for OpenCore guides
