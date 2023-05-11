
# switch-stack

My Nintendo Switch CFW stack and maintenance guide.

Disclaimer: For personal use. Other than this readme file, I am not the author of any contents contained within this repository.

# Current Stack

| Order | Component      | Concern                      | Version                                                                   | Latest                                                                                                                                | Depends On   |
| ----- | -------------- | ---------------------------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| 0     | Atmosphere     | CFW                          | [1.5.3](https://github.com/Atmosphere-NX/Atmosphere/releases/tag/1.5.3)   | [![~](https://img.shields.io/github/v/release/Atmosphere-NX/Atmosphere?label=)](https://github.com/Atmosphere-NX/Atmosphere/releases) |              |
| 0     | Hekate - Nyx   | Bootloader                   | [6.0.4](https://github.com/CTCaer/hekate/releases/tag/v6.0.4)             | [![~](https://img.shields.io/github/v/release/CTCaer/hekate?label=)](https://github.com/CTCaer/hekate/releases)                       |              |
| 0     | Sigpatches     | Signature patches            | [2023-05-08](https://sigmapatches.coomer.party/sigpatches.zip?2023-05-08) | [Download](https://sigmapatches.coomer.party/sigpatches.zip)                                                                          |              |
| 1     | nx-ovlloader   | Overlay Support              | [1.0.6](https://github.com/WerWolv/nx-ovlloader/releases/tag/v1.0.6)      | [![~](https://img.shields.io/github/v/release/WerWolv/nx-ovlloader?label=)](https://github.com/WerWolv/nx-ovlloader/releases)         |              |
| 1     | Tesla-Menu     | Overlay Support              | [1.2.0](https://github.com/WerWolv/Tesla-Menu/releases/tag/v1.2.0)        | [![~](https://img.shields.io/github/v/release/WerWolv/Tesla-Menu?label=)](https://github.com/WerWolv/Tesla-Menu/releases)             | nx-ovlloader |
| 1     | Fizeau         | Color Temperature Management | [2.4.1](https://github.com/averne/Fizeau/releases/tag/v2.4.1)             | [![~](https://img.shields.io/github/v/release/averne/Fizeau?label=)](https://github.com/averne/Fizeau/releases)                       | Tesla-Menu   |
| 1     | sys-clk        | Overclocking                 | [1.0.3](https://github.com/retronx-team/sys-clk/releases/tag/1.0.3)       | [![~](https://img.shields.io/github/v/release/retronx-team/sys-clk?label=)](https://github.com/retronx-team/sys-clk/releases)         | Tesla-Menu   |
| 1     | MissionControl | Bluetooth Controller Support | [0.9.0](https://github.com/ndeadly/MissionControl/releases/tag/v0.9.0)    | [![~](https://img.shields.io/github/v/release/ndeadly/MissionControl?label=)](https://github.com/ndeadly/MissionControl/releases)     |              |

Additional payloads

| Name         | Version                                                                |
| ------------ | ---------------------------------------------------------------------- |
| Lockpick_RCM | [1.9.10](https://github.com/shchmue/Lockpick_RCM/releases/tag/v1.9.10) |

# Utilities

| Category | Concern           | Name         | Source                                                                                                                   |
| -------- | ----------------- | ------------ | ------------------------------------------------------------------------------------------------------------------------ |
| Required | Payload injection | TegraRcmGUI  | [eliboa/TegraRcmGUI](https://github.com/eliboa/TegraRcmGUI) / [Releases](https://github.com/eliboa/TegraRcmGUI/releases) |
| Required | NSP installation  | NS-USBloader | [developersu/ns-usbloader](https://github.com/developersu/ns-usbloader) / [Releases](developersu/ns-usbloader/releases)  |
| Optional | NRO to NSP        | NTON         | [rlaphoenix/nton](https://github.com/rlaphoenix/nton)                                                                    |

# SD Setup

## Required

### CFW: Atmosphère (AMS)

[Atmosphere-NX/Atmosphere](https://github.com/Atmosphere-NX/Atmosphere) / [Releases](https://github.com/Atmosphere-NX/Atmosphere/releases)

> `fusee.bin` (lightweight bootloader) is not required

### Bootloader: Hekate - Nyx

[CTCaer/hekate](https://github.com/CTCaer/hekate) / [Releases](https://github.com/CTCaer/hekate/releases)

#### Configuration

Refer to [the docs](https://github.com/CTCaer/hekate#bootloader-configuration) and the [template](https://github.com/CTCaer/hekate/blob/master/res/hekate_ipl_template.ini).

`/bootloader/hekate_ipl.ini`

``` ini
[config]
autoboot=0
autoboot_list=0
bootwait=3
autohosoff=1
autonogc=1
updater2p=1

[CFW - emuMMC]
icon=bootloader/res/emu_boot.bmp
fss0=atmosphere/package3
emummcforce=1

[CFW - sysMMC]
icon=bootloader/res/sys_cfw_boot.bmp
fss0=atmosphere/package3
emummc_force_disable=1

[Stock]
icon=bootloader/res/stock_boot.bmp
fss0=atmosphere/package3
emummc_force_disable=1
stock=1

[Fusee]
icon=bootloader/res/icon_payload.bmp
payload=bootloader/payloads/fusee.bin
```

### Sigpatches

[Download latest](https://sigmapatches.coomer.party/sigpatches.zip)

### 90DNS

See [90DNS: DNS server for blocking all Nintendo Servers | GBAtemp](https://gbatemp.net/threads/90dns-dns-server-for-blocking-all-nintendo-servers.516234/)

> [to be replaced?](https://rentry.org/AvoidSwitchBan)

## Core

### sys-clk

[retronx-team/sys-clk](https://github.com/retronx-team/sys-clk) / [Releases](https://github.com/retronx-team/sys-clk/releases)

#### Configuration

Refer to [the docs](https://github.com/retronx-team/sys-clk#config) and the [template](https://github.com/retronx-team/sys-clk/blob/develop/config.ini.template).

> Can more simply be set in the overlay menu.

Recommended upper limits (MHz):

- CPU: 1224
- GPU: 921
- MEM: 1600 (docked default)

### NSP Installer: Awoo

[Huntereb/Awoo-Installer](https://github.com/Huntereb/Awoo-Installer) / [Releases](https://github.com/Huntereb/Awoo-Installer/releases)

### Save Manager: JKSV / Checkpoint

[J-D-K/JKSV](https://github.com/J-D-K/JKSV) / [Releases](https://github.com/J-D-K/JKSV/releases)

[BernardoGiordano/Checkpoint](https://github.com/BernardoGiordano/Checkpoint) / [Releases](https://github.com/BernardoGiordano/Checkpoint/releases)

## Optional

### Themes: NXThemes installer

[exelix11/SwitchThemeInjector](https://github.com/exelix11/SwitchThemeInjector) / [Releases](https://github.com/exelix11/SwitchThemeInjector/releases) / `NXThemesInstaller.nro`

### FTP Server (daemon): sys-ftpd

[cathery/sys-ftpd](https://github.com/cathery/sys-ftpd) / [Releases](https://github.com/cathery/sys-ftpd/releases)

### Firmware Downloader: Kefir

[rashevskyv/kefir-updater](https://github.com/rashevskyv/kefir-updater) / [Releases](https://github.com/rashevskyv/kefir-updater/releases)

### SNES Emulator: pEMU

[Cpasjuste/pemu](https://github.com/Cpasjuste/pemu) / [Releases](https://github.com/Cpasjuste/pemu/releases) / `psnes.nro`

# Maintenance

## Updating Firmware

See [Switch Firmwares | Darthsternie's Firmware Archive](https://darthsternie.net/switch-firmwares/).

Install with Daybreak (bundled with Atmosphere).

# Payloads

[shchmue/Lockpick_RCM](https://github.com/shchmue/Lockpick_RCM) / [Releases](https://github.com/shchmue/Lockpick_RCM/releases)
