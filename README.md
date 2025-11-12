# Lenovo Yoga C640-13IML OpenCore EFI

![OpenCore](https://img.shields.io/badge/OpenCore-0.9.8-blue.svg)
![macOS](https://img.shields.io/badge/macOS-Ventura_|_Sonoma-orange.svg)

A complete OpenCore EFI folder for installing macOS (Ventura & Sonoma) on the Lenovo Yoga C640-13IML.



## ⚠️ Disclaimer

This project is for educational purposes only. I am not responsible for any damage to your device, data loss, or any other issues that may arise from using this EFI. You are performing this installation at your own risk.

Please note that this EFI is specifically tailored for my hardware configuration. While it may work for similar models, it's not guaranteed.
**If you are using a stock device, this will forsure not work because the "Intel Wireless-AC 9560" which came with my device and usually comes with all Yoga C640's has been replaced with an Realtek chip (which macOS has no support for so I ended up taking that out too and started using a USB dongle instead.**
*Installation was done using an offline installer I made in a mac*

## 💻 Hardware Specifications

This EFI is built for the following hardware. If your specs differ (especially Wi-Fi or Audio), you may need to adjust the Kexts and `config.plist`.
I have added the hardware information of my current device in the Report.json file, if it helps you, it helps you I guess.

| Component | Model |
| :--- | :--- |
| **CPU** | 10th Gen Intel Core i7-10210U (Comet Lake-U) |
| **iGPU** | Intel UHD Graphics |
| **Audio** | Realtek ALC285 |
| **Trackpad** | I2C HID Trackpad |
| **Touchscreen** | I2C HID Touchscreen |
| **Storage** | NVMe SSD |

## ✅ Hardware Status

This build is highly stable and suitable for daily use.

### What Works
* **Graphics:** Intel UHD Graphics with full QE/CI (Metal supported).
* **Audio:** Speakers and 3.5mm headphone jack (via `layout-id=15`).
* **Trackpad:** Full multi-touch gestures.
* **USB:** All ports (Type-A and Type-C) working.
* **Battery:** Correct battery status and power management.
* **Sleep/Wake:** Working correctly.
* **Keyboard:** All keys and function keys (brightness, volume).
* **iServices:** iMessage, FaceTime, App Store, etc. (with a valid SMBIOS).

### What Doesn't Work
* **Fingerprint Sensor:** **Will never work.** macOS does not support this hardware.
* **Internal LTE USIM Card:** Not working (no Hackintosh has ever had a USIM Card support, and to be honest I don't even care to make this work).
* **Touchscreen:** I don't need it to work as touchscreens in laptops are a gimmick anyway, so I don't know whether it is even possible to make this work.

---

## 🚀 How to Install

This guide assumes you are familiar with the basic Hackintosh installation process.

### 1. Read the Guide
Start by reading the official **[Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)**. Do not skip this. This ReadMe provides a *pre-built* EFI, but the guide explains *how* to create the installer and what to do.

### 2. Prepare the USB Installer
1.  Create a macOS Ventura or Sonoma USB installer using the method from the Dortania guide.
2.  Download the [latest release](https://github.com/n1soryu/lenovo-c640-13iml-opcore-efi/releases) of this repository.
3.  Mount the EFI partition of your USB drive.
4.  Copy the `EFI` folder from this repository to the root of your USB's EFI partition.

### 3. Generate Your SMBIOS
**This is not optional!** You must generate your own unique SMBIOS information to use iServices.
1.  Download [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).
2.  Run the script and select "Generate SMBIOS".
3.  Use the `MacBookPro16,3` model.
4.  Open your `EFI/OC/config.plist` file with [ProperTree](https://github.com/corpnewt/ProperTree).
5.  Navigate to `PlatformInfo > Generic`.
6.  Copy and paste your generated `Serial`, `Board Serial` (MLB), and `SmUUID` (SystemUUID) into the corresponding fields.
7.  Save the `config.plist`.

### 4. BIOS Settings
You must configure your laptop's BIOS before attempting to boot.

* **Security**
    * `Secure Boot`: **Disabled**
* **Configuration**
    * `Intel Virtual Technology` (VT-x): **Enabled**
    * `Intel Hyper-Threading`: **Enabled**
    * `Intel SGX`: **Disabled**
* **Boot**
    * `Fast Boot`: **Disabled**
    * `Boot Mode`: **UEFI**

---

## 🔧 Post-Install
After installation, you must:
1.  Mount your main drive's EFI partition.
2.  Copy the `EFI` folder (with your unique SMBIOS) from your USB drive to your main drive's EFI partition.
3.  Reboot without the USB drive.

## 🙏 Credits

This EFI would not be possible without the hard work of the entire Hackintosh community.
* **[Acidanthera](https://github.com/acidanthera)** for OpenCore and most essential Kexts (Lilu, WhateverGreen, VirtualSMC, etc.)
* **[Dortania](https://dortania.github.io/OpenCore-Install-Guide/)** for the comprehensive installation guide.
* **[VoodooI2C Team](https://github.com/VoodooI2C)** for touchscreen and trackpad support.
* **[CorpNewt](https://github.com/corpnewt)** for GenSMBIOS, ProperTree, and other utilities.
