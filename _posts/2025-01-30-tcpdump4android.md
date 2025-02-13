---
title: 'tcpdump to Capture Packets on Android'
date: 2025-01-30
permalink: /posts/2025-01-30-tcpdump4android/
tags:
  - Android
  - tcpdump
  - Networking
---

## 1. Check The Architecture Version of The Phone
- ```abd shell```
- ```getprop ro.product.cpu.abi```
- Google Pixel 8a is arm64-v8a, meaning you should download 64-bit tcpdump from [tcpdump](https://www.androidtcpdump.com/android-tcpdump/downloads64bit).

## 2. Push tcpdump to The Phone
- ```adb push <path-to-downloaded-tcpdump> /data/local/tmp```

## 3. Capture All Packets on The Phone
- ```abd shell```
- ```su```
- ```cd /data/local/tmp/```
- ```chmod +x ./tcpdump```
- ```tcpdump -i any -w /sdcard/capture.pcap```
- Ctrl + C
- ```exit```
- ```adb pull /sdcard/capture.pcap <path-to-save-the-file>```

## 4. Other Useful Commands
- Check the package name of an app: ```adb shell an monitor```, and then open the app.
- adb man:
  - [-i interface]
  - [-w outputfile.pcap]
  - [--print]
  - [-D show-available-ports]
- Check PID: ```adb shell ps | grep <package-name>```
  - e.g., ```adb shell ps | grep com.facebook.stella```
- Find target file: ```find / -name <filename-or-packagename> 2>/dev/null```
  - e.g., ```find / -name btsnoop_hci.log 2>/dev/null```
  - >> ```/data/misc/bluetooth/logs/btsnoop_hci.log```
