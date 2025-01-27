---
title: 'How to Root a Google Pixel 8a'
date: 2025-01-25
permalink: /posts/2025-01-25-root-pixel-8a/
tags:
  - Android
  - Root
  - Google Pixel
---


Google Pixel 8a (Android version 14) is rootable using Magisk by patching init_boot.img and flashing the patched image file to Pixel 8a.

[TOC]

## 0. Preparation
- ```adb``` is required for Android app development (see details in Section 3).
- ```fastboot``` is needed to unlock the device bootloader and flash it with a new system image (see details in Section 3).
- Download factory image from [Images](https://developers.google.com/android/images#akita): Click on corresponding ```Link``` based on your build number on your phone.
- Extract ```init_boot.img``` from the downloaded zip file. Save and remember this file.

## 1. Enable Developer Options
Go to: Settings > About phone > Tap on "Build number" for 7 times to enable ```Developer Options```.

## 2. Enable OEM Unlocking and USB Debugging
Go to: Settings > System > Developer options > Enable ```OEM unlocking``` and ```USB debugging```.

## 3. Setup adb and fastboot
1. Go to [Tools](https://developer.android.com/tools/releases/platform-tools), and download ```platform-tools``` (it's a folder named ```platform-tools```, including tools like adb, fastboot).
2. Set environment variables (optional): 
   1. Open a terminal on Mac;
   2. Type ```sudo nano ~/.zshrc```;
   3. Type ```export PATH=$PATH:/Users/xxx/.../platform-tools``` to the last line;
   4. Ctrl + o to write out;
   5. Ctrl + x to exit;
   6. Type ```source ~/.zshrc``` on the terminal;
   7. Check the availability of adb and fastboot: ```adb --version``` and ```fastboot --version```. If the version number are showed, then you are good with adb and fastboot.

## 4. Unlock The Bootloader
1. Reboot into the bootloader: ```adb reboot bootloader```.
2. Unlock the bootloader: ```fastboot flashing unlock```.
3. Reboot: ```fastboot reboot```.

## 5. Re-Enable The Developer Options
1. Tap on ```Build number``` for 7 times
2. Enable ```Usb-debugging```.
3. ```OEM unlocking``` should state: Bootloader is already unlocked. If not, go back to previous steps to double check those details.

## 6. Transfer init_boot.img from Mac to phone
1. Open a terminal on Mac.
2. ```adb devices``` to check if the phone is connected to the Mac.
3. ```adb push <init_boot>.img /sdcard/Download/```.
4. To check the transfer, use ```adb shell``` to access the directory of the phone, and then direct to ```/sdcard/Download/``` to check.
5. ```exit``` to exit adb shell.

## 7. Transfer the Magisk from the Mac to Pixel 8a and Installation
1. ```adb push /PATH/TO/YOUR/Magisk-xx.apk /sdcard/Download```.
2. Find the transferred Magisk.xx.apk in the app Files and tap on it, it will be installed on the phone.

## 8. Patch the init_boot.img
1. Open the Magisk app.
2. Select Magis install and ```Select and Patch a File```.
3. Select the init_boot.img and then click on ```LET'S GO```. 

## 9. Transfer the patched init_boot.img back to the Mac
```adb pull <patched_init_boot_image>.img /PATH/ON/YOUR/MAC```

## 10. Flash patched image
1. ```adb reboot bootloader```.
2. ```fastboot flash init_boot <patched_init_boot_image>.img``` (not ```fastboot flash boot <patched_init_boot_image>.img```).
3. ```fastboot reboot```.

## 11. Verify
Download app named ```Root Check``` (since Root Checker is not available in Android 14).

## 12. Troubles and Solutions
1. If you want to restart the process or have no idea what is going wrong, go to [FactoryReset](https://developers.google.com/android/images#akita): Click on the corresponding ```Flash``` to factory reset your phone based on your build number on your phone.
2. Remember it's ```init_boot.img```, rather than ```boot.img```.