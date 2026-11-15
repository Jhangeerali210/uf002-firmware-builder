# UF002 Custom Firmware Builder

This repository builds a custom Linux boot image for the **UF002_MB_V02** 4G WiFi Dongle (Qualcomm MSM8909 Snapdragon 210).

## What This Does

- Downloads MSM8909 mainline Linux kernel
- Compiles it with **UF002_MB_V02-specific DTS** (correct USB + WiFi regulators)
- Creates a flashable `boot.img`

## USB Regulator Fix (Why Previous Attempts Failed)

The UF002_MB_V02 board uses:
- `PM8909_L2` → USB VDD_DIG @ 1.2V
- `PM8909_L7` → USB HSUSB_1p8 @ 1.8V  
- `PM8909_L13` → USB HSUSB_3p3 @ 3.075V

This was confirmed by live inspection of the stock Android 3.10 kernel.

## How to Build

1. Click **Actions** tab above
2. Click **Build UF002 Custom Boot Image**
3. Click **Run workflow** → **Run workflow**
4. Wait ~40 minutes
5. Download `uf002-custom-boot-*.zip` from Artifacts

## How to Flash

```bash
# Test WITHOUT flashing (safe - RAM boot)
fastboot boot uf002-custom-boot.img

# If USB shows up in Windows, then permanently flash:
fastboot flash boot uf002-custom-boot.img
```

## Recovery

Device: `FD_4 + GND` → EDL 9008 → `restore.bat` = 100% factory restore
