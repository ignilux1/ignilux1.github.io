---
title: 'tcpdump to Capture Packets on Android'
date: 2025-01-25
permalink: /posts/2025-01-30-tcpdump4android/
tags:
  - Android
  - tcpdump
  - Networking
---

## 1. Check The Version of The Phone
- ```abd shell```
- ```getprop ro.product.cpu.abi```
- Google Pixel 8a is arm64-v8a, meaning you should download 64-bit tcpdump from [tcpdump](https://www.androidtcpdump.com/android-tcpdump/downloads64bit).

## 2. Push tcpdump to The Phone
- ```adb push <path-to-downloaded-tcpdump> /data/local/tmp```
- 

## 3. Capture All Packets on The Phone
- ```abd shell```
- ```su```
- ```cd /data/local/tmp/```
- ```chmod +x ./tcpdump```
- ```tcpdump -i any -w /sdcard/capture.pcap```
- ```exit```
- ```adb pull /sdcard/capture.pcap <path-to-save-the-file>```
