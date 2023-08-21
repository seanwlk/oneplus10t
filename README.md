# Boot image dumps for Oneplus 10T - CPH2415

Since oneplus stopped releasing firmware Zips it's very troublesome to root their devices. I created this repo to help people have fast access to the needed files for rooting the devices.

# How
It's relatively easy, you can do it yourself but I will try to keep this repo updated with the latest files. The way I get the boot file is from downloading the **full** OTA zip from [OxygenUpdater](https://github.com/oxygen-updater/oxygen-updater) for the 10T then extracting the payload.bin and from that one i can get the boot.img with [payload-dumper-go](https://github.com/ssut/payload-dumper-go)

Command for payload-dumper-go
```bash
payload-dumper-go.exe -p boot payload.bin
```
After that I just take the stock boot image and patch it from within the magisk app.

# Flash patched boot image from fastboot
I assume you already know that you need to have unlocked bootloader to do this. After that you just need to flash to current A/B active slot by running the following command
```bash
fastboot flash boot magisk_patched-boot.img
```
This should flash on the currently active slot but if you want to know which it is you have to `fastboot getvar all` and look for `current-slot` after which you can use `boot_a` and `boot_b` accordingly in the previously mentioned flash command instead of just `boot`

# How to keep magisk after OTA without fastboot
You can patch the boot image without using fastboot and therefore use the files in this repository only as a fallback. To keep the root you need to run the OTA update through [OneplusLocalUpgrade](https://github.com/seanwlk/oneplus10t/blob/main/OPLocalUpdate_For_Android12.apk) then you have to open Magisk app **BEFORE** rebooting the device after the OTA installation completed and from there use the option `Install` -> `Install to Inactive Slot`. Else you'll have to flash again the patched boot image from [here](https://github.com/seanwlk/oneplus10t/releases) or after you extracted your own

# Download
All files are available from [releases](https://github.com/seanwlk/oneplus10t/releases)

# Disclaimer
I am not responsible for bricked devices or other issues. The images are releases as is and generally tested on my own device beforehand.
