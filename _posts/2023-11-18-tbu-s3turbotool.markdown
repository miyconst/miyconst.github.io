---
layout: post
title:  "Xeon E5 V3 Turbo Boost Unlock with S3TurboTool"
date:   2023-11-18 17:38:23 +0100
categories: hardware cpu intel
tags: x99 lga2011 lga2011-3 xeon turbo boost bios unlock
background: "#139aff"
---

# Xeon E5 V3 Turbo Boost Unlock with S3TurboTool - step by step guide

You can download all required files and tools from my Microsoft One Drive: [Miyconst Hardware / LGA 2011-3 / TBU 2023 Q4](https://1drv.ms/f/s!AtZZXDjjb94kgstOpEk-fIkQxCXCAg?e=PlNcgE).

## Remove the `06F2` CPU microcode

1. Launch the `mmtool_a5.exe` application.
2. Click the `[Load Image]` button and select your BIOS file.
3. Navigate to the `[Cpu Patch]` tab.
4. Find and delete all entries from the table where `CPU ID` equals to `06F2`.
5. Save the modified BIOS.

![mmtool_a5 - step 1](/assets/2023-11-18-tbu-s3turbotool/mmtool_a5-00.png)
![mmtool_a5 - step 2](/assets/2023-11-18-tbu-s3turbotool/mmtool_a5-01.png)
![mmtool_a5 - step 3](/assets/2023-11-18-tbu-s3turbotool/mmtool_a5-02.png)

## Set CPU C State options

1. Launch the `AMIBCP5.exe` application.
2. Open the BIOS file saved in the previous step.
3. In the left tree find the `CPU C State Control` option, usually it's located at the following path: `Common RefCode Configuration` → `IntelRCSetup` → `Advanced Power Management Configuration` → `CPU C State Control`.
4. Set the following values:
    - `Package C State limit` to `C2 state`.
    - `CPU C3 report` to `Enable`.
    - `CPU C6 report` to `Disable`.
5. Close AMIBCP5 application and agree to save changes.

![AMIBCP5 settings for single socket motherboards](/assets/2023-11-18-tbu-s3turbotool/amibcp-single-socket.png)

## Inject required TBU driver - Single Socket

1. Launch the `UEFITool.exe` application.
2. Open the BIOS file saved in the previous step.
3. Inside `Intel image` → `BIOS region` search for entry `PchS3Peim` with UID `271DD6F2-54CB-45E6-8585-8C923C1AC706`.
4. Right-click on the `PchS3Peim` entry and select `[Replace as is ...]`.
5. Select the desired `.ffs` file you want to inject.
6. Save the changes.

![UEFI Tool settings for single socket motherboards](/assets/2023-11-18-tbu-s3turbotool/uefitool-single-socket.png)

## Inject required TBU driver - Dual Socket

1. Launch the `UEFITool.exe` application.
2. Open the BIOS file saved in the previous step.
3. Inside `Intel image` → `BIOS region` search for the pre-last entry `FFSv2` with UID `8C8CE578-8A3D-4F1C-9935-896185C32DD3`.
4. Inside find the last DXE entry, in my case it case UID `A0327FE0-1FDA-4E5B-905D-B510C45A61D0`.
5. Right-click on it and select `[Insert after ...]`.
6. Select the desired `.ffs` file you want to inject.
7. Save the changes.

![UEFI Tool settings for single socket motherboards](/assets/2023-11-18-tbu-s3turbotool/uefitool-dual-socket-00.png)
![UEFI Tool settings for single socket motherboards](/assets/2023-11-18-tbu-s3turbotool/uefitool-dual-socket-01.png)

## Flash the BIOS

- Flash the BIOS, see how below.
- Reboot and go into BIOS settings.
- Restore BIOS defaults.
- Save changes and reboot.
- Go into BIOS again if you want to adjust extra settings.

To flash the modded BIOS you have the following options:

- [Mi899](https://github.com/miyconst/Mi899) if you trust my app and don't want to bother with console (command line) yourself.
- FPT and AFU applications, see the syntax below.
- External flash programmer if the BIOS is locked for software flash: [🇬🇧 CH341a – minimal usage guide | how to read & write a motherboard BIOS](https://youtu.be/4qX2zihB6UE?si=vXVf4Fo430RfLJ05).

Extra notes:

- The `.rom` and `.bin` file extensions do not matter as long as you have a binary BIOS file.
- Make sure to buy a programmer with a voltage switch, like this one: [CH341A Programmer V1.7 1.8V - 5.0V](https://s.click.aliexpress.com/e/_DkgHwT5).

### FPT syntax

To save / dump the current BIOS execute the following:

```
fptw64.exe -d bios-file-name.bin
```

To flash BIOS from a file execute the following:

```
fptw64.exe -f bios-file-name.bin
```

Make sure to run console (CMD) as administrator and replace `bios-file-name.bin` with the actual file name.

### AFU syntax

To save / dump the current BIOS execute the following:

**Important**: AFU saves only half of the BIOS (8MB) instead of the full BIOS (16MB). Such dump can be flashed with AFU, but not with FPT.

```
AFUWINx64.exe bios-file-name.bin /O
```

To flash BIOS from a file execute the following:

```
AFUWINx64.exe bios-file-name.bin /P /B /N /X
```

## The UEFI system does not boot after TBU

This is a known UEFI bug of the LGA 2011-3 X99 platform. The fix is simple:

1. Shut down the computer.
2. Disconnect the power cord.
3. Disconnect all storage devices.
4. Turn on the computer.
5. Go to the BIOS and restore defaults.
6. Save changes and restart.
7. Go to the BIOS and apply any extra settings you wish, such as RAM timings. This is an optional step.
8. Turn off the computer and disconnect the power cord.
9. Connect all storage devices back.
10. Turn on the computer, it should work properly.

## Extra links

- [Xeon E5-2600 V3 Turbo Boost Unlock](https://miyconst.github.io/hardware/cpu/intel/2020/01/04/xeon-e5-2600-v3-turbo-boost-unlock.html).
- [🇬🇧 CH341a – minimal usage guide, how to read & write a motherboard BIOS](https://youtu.be/4qX2zihB6UE?si=vXVf4Fo430RfLJ05).
- [🇬🇧 Mi899 – X99 Tool Set, read, write BIOS & unlock turbo-boost with a few mouse clicks](https://youtu.be/bO2t790vhg8?si=K6n61THJs5AWSsQW).
- [🇬🇧 Resizable BAR on LGA 2011-3 X99 – how to enable and get extra performance](https://youtu.be/vcJDWMpxpjE?si=QOibXP_UBVaNrdZx).
- [GitHub: Mi899](https://github.com/miyconst/Mi899).
- [GitHub: ReBarUEFI](https://github.com/xCuri0/ReBarUEFI/releases).
- [GitHub: UEFITool](https://github.com/LongSoft/UEFITool/releases/tag/0.28.0).
- Join my [Discord](https://discord.gg/m2b3f2B9x9) to ask questions.