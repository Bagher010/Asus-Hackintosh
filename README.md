
# Asus Zephyrus Hackintosh (GU502GU 2019 Model)

## Table of Contents
- [Introduction](#introduction)
- [System Specifications](#system-specifications)
- [Prerequisites](#prerequisites)
- [Creating the macOS Installer](#creating-the-macos-installer)
- [BIOS Configuration](#bios-configuration)
- [Installation Steps](#installation-steps)
- [Post-Installation](#post-installation)
- [Kexts and Tools](#kexts-and-tools)
- [Configuration Details](#configuration-details)
- [Common Issues and Fixes](#common-issues-and-fixes)
- [Updating OpenCore and Kexts](#updating-opencore-and-kexts)
- [Acknowledgements](#acknowledgements)
- [Disclaimer](#disclaimer)
- [License](#license)

## Introduction
This repository contains the necessary files and instructions for installing macOS on an Asus Zephyrus GU502GU (2019) using OpenCore. Follow these steps to transform your laptop into a fully functional Hackintosh.

## System Specifications
- **Model**: Asus Zephyrus GU502GU
- **Processor**: Intel Core i7-9750H
- **Graphics**: NVIDIA GeForce GTX 1660 Ti (unsupported, disabled in macOS), Intel UHD Graphics 630
- **Memory**: 16GB DDR4
- **Storage**: 512GB NVMe SSD
- **Audio**: Realtek ALC294
- **Wi-Fi**: Intel Wireless-AC 9560

## Prerequisites
- A USB flash drive (16GB or larger)
- A copy of macOS (latest version preferred)
- A secondary Mac, Windows, or Linux machine for creating the USB installer
- Basic understanding of Hackintosh principles

## Creating the macOS Installer
1. **Download macOS**:
   - Obtain macOS from the App Store or use [gibMacOS](https://github.com/corpnewt/gibMacOS) on Windows/Linux.

2. **Create the USB Installer**:
   - Use the `createinstallmedia` command:
     ```sh
     sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/USB
     ```

3. **Copy EFI Folder**:
   - Copy the `EFI` folder from this repository to the EFI partition of your USB drive.

## BIOS Configuration
Configure your BIOS settings as follows:
- Disable Secure Boot
- Enable CSM (Compatibility Support Module)
- Set SATA mode to AHCI
- Disable Serial Port
- Disable VT-d (recommended for initial setup)

## Installation Steps
1. **Boot from USB**:
   - Insert the USB installer and boot your Asus Zephyrus from it by pressing `Esc` or `F2` during startup.

2. **Install macOS**:
   - Follow the macOS installer instructions.
   - Use Disk Utility to partition and format your drive as APFS.

3. **Post-Installation**:
   - Boot into macOS using the USB drive.
   - Mount the EFI partition of your system drive and copy the `EFI` folder from the USB drive to the system drive.

## Post-Installation
After successfully installing macOS, perform the following steps:
1. **Copy EFI Folder**:
   - Mount the EFI partition of your system drive and copy the `EFI` folder from the USB drive to it.

2. **Install Necessary Kexts**:
   - Ensure all required kexts are installed in the `EFI/OC/Kexts` directory.

3. **Configure OpenCore**:
   - Adjust your `config.plist` file for your specific hardware setup.

## Kexts and Tools
This setup utilizes the following kexts and tools:
- **Lilu.kext**: Essential for various patches.
- **WhateverGreen.kext**: Graphics support.
- **AppleALC.kext**: Audio support.
- **VirtualSMC.kext**: System management.
- **IntelMausi.kext**: Ethernet support.
- **AirportItlwm.kext**: Intel Wi-Fi support.
- **USBInjectAll.kext**: USB support.
- **NVMeFix.kext**: NVMe SSD support.
- **HfsPlus.efi**: HFS+ file system support.
- **OpenRuntime.efi**: OpenCore runtime services.

## Configuration Details
Detailed configurations included in the `config.plist`:
- **ACPI Patches**:
  - `SSDT-EC.aml`: Embedded Controller patch.
  - `SSDT-PLUG.aml`: CPU power management.
- **Boot Arguments**:
  - `-v keepsyms=1 debug=0x100`: Verbose mode and debugging.
- **Device Properties**:
  - Specific patches for hardware compatibility.
- **SMBIOS**:
  - Using `MacBookPro15,1` for better compatibility.

## Common Issues and Fixes

### Boot Loop
- **Fix**: Check your ACPI patches in `config.plist`.

### No Audio
- **Fix**: Ensure `AppleALC.kext` is configured with the correct layout ID in `config.plist`.

### Wi-Fi Not Working
- **Fix**: Confirm `AirportItlwm.kext` is present in `EFI/OC/Kexts` and referenced in `config.plist`.

## Updating OpenCore and Kexts
1. **OpenCore**:
   - Follow the [Dortania guide](https://dortania.github.io/OpenCore-Post-Install/universal/update.html) for updating OpenCore.
2. **Kexts**:
   - Download latest versions and replace existing kexts in `EFI/OC/Kexts`.

## Acknowledgements
Special thanks to:
- [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) for the OpenCore guide.
- [Acidanthera](https://github.com/acidanthera) for providing essential Hackintosh tools.

## Disclaimer
This guide is for educational purposes only. Use at your own risk. The author is not responsible for any damage resulting from following this guide.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
