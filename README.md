# ThinkPad Hackintosh EFI Folder (Thinkintosh)

This is my custom **EFI folder** for running macOS on a ThinkPad laptop. I decided to share my EFI setup on GitHub for easy access and as a backup in case I ever need to restore my configuration (which happened previously). 

Everything has been thoroughly tested (so far) and works out of the box, including:
- **Dual battery support**
- **Sleep functionality**
- **HDMI screen extending/duplicating**
- **Software updates**

The difference between my setup and rest I found online, is minimalistic approach without bloated up EFI. Everything inside is there because it **needs** to be there.

Dual battery support is achieved using `SMCBatteryManager` and `ECEnabler` kexts alongside `SSDT-BATC.aml` SSDT. `YogaSMC` kext adds CPU fan speed measurements and reliable battery readouts (e.g. cycle count). HDMI setup is done under `DeviceProperties` with *framebuffer-con1* patching guide from [Dortania](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/kaby-lake.html#deviceproperties$0).

USB mapping fixes many sleep related issues, and as such was the main reason behind mapping all the ports and internal devices like integrated camera. Graphical loading interface is present to give additional layer to Macintosh similarity.

For compatibility issues, and avoiding EFI rewriting, it is recommended to boot macOS Ventura (13.x.x). T470 has similar specifications as 13" **MacBook Pro** with Core i5 7360U processor from mid-2017, hence why `macbookpro14,1` SMBIOS is best-fit solution when generating most important Hackintosh info.

All above guides are to be found on Dortania OpenCore installation page with more explanations on why everything used is as is.

## Hardware Specs :computer:

- **Model**: ThinkPad T470
- **CPU**: Intel Core i5 7300U
- **RAM**: 16 GB DDR4 RAM (Crucial and SK Hynx sticks)
- **Storage**: 256 GB NVMe Lense SSD
- **Graphics**: Intel HD Graphics 620
- **Wireless**: Intel Dual Band Wireless-AC 8265
- **Ethernet**: Intel Ethernet Connection I219-LM
  
## Features :bulb:

- **Dual Battery Support**: Both internal and external batteries are properly recognised and function as expected.
- **Sleep**: System can go to sleep and wake up without any issues.
- **HDMI**: HDMI works for screen extension and duplication.
- **Software Updates**: Software updates can be applied via the Mac App Store without issues.

## Exclusions :no_entry_sign:

- **Touchscreen**: I decided not to use drivers for the touchscreen, as I dislike the feel of it. This setup does **not** support touchscreen functionality.
- **Fingerprint sensor**: There is currently no way of emulating Validity 0097 device in macOS.

## Installation Instructions :pushpin:

This build supports `OpenCore` 1.0.5 boot-loader. **Do not** use it with `Clover`.

1. **Prerequisites**:
   - A ThinkPad T470 laptop with same specs.
   - A macOS USB installer.
   - A UEFI-compatible boot method.
   - **Important** [corpnewt GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) for SMIOS configuration as current `config.plist` contains zeros.

2. **Steps**:
   1. Download and extract the latest **OpenCorePkg** version and create a bootable USB installer. Detailed steps are provided in [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/prerequisites.html) which I recommend reading.
   2. Follow [Dortania OpenCore](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/kaby-lake.html#platforminfo) on how to generate `PlatformInfo`.
   3. Replace the EFI folder on your USB installer with the one from this repository.
   4. Boot into the USB installer and perform a fresh macOS installation. When greeted with boot-loader, press `SPACE` to display install option (usually named `OPENCORE (dmg)` or `USB DEVICE (dmg)`).
   5. Once macOS is installed, mount the EFI partition from installation medium to macOS drive. Reboot and boot from the newly installed macOS drive.

3. **Post-installation**:
   - Make sure to configure any necessary kexts or settings depending on your specific model (such as Wi-Fi and audio).
   - Follow any additional troubleshooting steps if something isn't working right.
   - (*Optional*, recommended) Enable HiDPI using the [xzhih One-Key-Hidpi](https://github.com/xzhih/one-key-hidpi) to preserve eyesight as UX elements on 1920 x 1080 screen tend to be barely visible.

## Important Notes :heavy_exclamation_mark:

- This setup is intended for **ThinkPad** hardware. While it may work on other laptops, there is no guarantee of compatibility due system definitions and kexts being tailored for the ThinkPad T470. Other Intel processors would add a bit more context.
- The `EFI` folder is optimised for use with **OpenCore**. If you’re using **Clover**, you may need to adjust some settings accordingly and pray Ave Maria.

## License :clipboard:

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments :heart_eyes:

- Thanks to the Hackintosh community and all Dortania guides out there making this project "relatively" easy.
- Special thanks to those who maintain and develop OpenCore, SSDTs, and various kexts which made this possible.

---

Feel free to modify the repository to suit your needs, and please report any issues or improvements!
