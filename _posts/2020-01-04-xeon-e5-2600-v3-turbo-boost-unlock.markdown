---
layout: post
title:  "Xeon E5-2600 V3 Turbo Boost Unlock"
date:   2020-01-04 18:43:45 +0100
categories: hardware cpu intel
tags: x99 lga2011 lga2011-3 xeon turbo boost bios unlock
background: "#139aff"
---

## 2022 Q3 update

- [S3TurboTool guide in russian](https://xeon-e5450.ru/socket-2011-3/e5-2600-v3/dobavlyaem-anlok-v-bios-raz-i-navsegda-cherez-s3turbotool/).
- [Ultimate Patcher Tool v2.2 for C612/X99 Firmware](https://nalex.me/ultimate-patcher-tool/).
- [Download ready-made FFS drivers and related software](https://1drv.ms/u/s!AtZZXDjjb94k61HFsD8WMI5vGh1l?e=wMMElc).
- [Mi899 - X99 Tool Set | read, write BIOS & unlock turbo-boost with a few mouse clicks.](https://github.com/miyconst/Mi899).

### LGA 2011-3 (X99) platform overview and status update in 2022 Q3

<iframe width="700" height="394" src="https://www.youtube.com/embed/AW0QgQNbBwA?start=553" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vRiOjd2ZBfs-NMrp0iYZAXAoOKsBnNavKQNQz9ECcL3Bf8U0gwo5ot6jil54O636397tgEMJIsw1fAn/embed?start=false&loop=false&delayms=60000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

## Method 1: Inject FFS driver straight into the BIOS.

*This is an outdated method, use S3TurboTool instead.*

This is a step by step guide of how to unlock Xeon E5-2600 V3 Turbo Boost frequency on all CPU cores using Chinese X99 motherboards and modified BIOS with a build in FFS driver. This method is OS independent and does not require EFI driver installation / re-installation.

<iframe width="700" height="394" src="https://www.youtube.com/embed/YymioiX9SFg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Required files

Download archive required for this guide.

- From Microsoft One Drive: [`x99-tu-ffs.zip`](https://1drv.ms/u/s!AtZZXDjjb94k61IdfWbVDXsd9WJX?e=LmC613).
- Ready made BIOS files for the lazy users - from [Microsoft One Drive](https://1drv.ms/u/s!AtZZXDjjb94k61HFsD8WMI5vGh1l?e=wMMElc).


**Hashes of the `x99-tu-ffs.zip` file:**

```
MD5: 6eeeff1123513e08499283f3719f16d9
SHA1: 52299ba3f0988551bcdf9bc51b13e07c5c1d3ec6
SHA256: 04d32938b330328097b88b2b5c03b976e7a7a3dbe6adbdd9e66d1994f698ef66
```

To validate hashes of the file execute the following commands:

```
certutil -hashfile x99-tu-ffs.zip MD5
certutil -hashfile x99-tu-ffs.zip SHA1
certutil -hashfile x99-tu-ffs.zip SHA256
```

### Google Slides Presentation

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vQQ5-qzfzbhz5WbxPCoqGCbuKBSvr0TnqY8CvEaBWAHnnRrq_tgdv7wy9EcB1D-qESi6lTK41IJzGqV/embed?start=false&loop=false&delayms=60000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

<hr/>

## Method 2: Manual EFI driver installation.

This is a step by step guide of how to unlock Xeon E5-2600 V3 Turbo Boost frequency on all CPU cores using Chinese X99 motherboards and manual EFI driver installation. This method was written for and tested with Windows 10 Pro x64.

- **! IMPORTANT**: The step "6. Windows driver installation" does not seem to be required any more. First validate if Turbo Boost Unlock works without it. Install Windows drivers only if unlock does not work without them.
- **! IMPORTANT**: Use the `V3DUAL.EFI` driver for dual socket motherboards. Google Slides presentation has been updated, but the video guide is not possible to update.

<iframe width="700" height="394" src="https://www.youtube.com/embed/VkwEvATIgW0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Required files

Download required archive for this guide.

- From Microsoft One Drive: [`x99-tu.zip`](https://1drv.ms/u/s!AtZZXDjjb94k61MMADe8-0EYA_6p?e=JVOXv6).

**Hashes of the `x99-tu.zip` file:**

```
MD5: 272621266752a1df69cfa57c88a3f2df
SHA1: e6c43b03cabf3d21b8b023f21c7d64c2fc09bc6e
SHA256: 88a9cc5d15d3ac59e896600c6c2706ca0cd99a55b45be6e18874df2b7c23d2bd
```

To validate hashes of the file execute the following commands:

```
certutil -hashfile x99-tu.zip MD5
certutil -hashfile x99-tu.zip SHA1
certutil -hashfile x99-tu.zip SHA256
```

### Google Slides Presentation

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vRJ8w24z1u9vY7WlyHzsAPeCHSn_lbpD4dfJzG40u8S_hyAc3_qpLjD-yJG2k4i-ojKLW8KziYC9gtW/embed?start=false&loop=true&delayms=60000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>

## Review of the Chinese X99 Motherboards

### JingSha X99 D4

<iframe width="560" height="315" src="https://www.youtube.com/embed/H0OzFSGt2Dg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### JingSha X99 Dual

<iframe width="560" height="315" src="https://www.youtube.com/embed/F1mIj2xlc-g" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Huananzhi X99-TF

<iframe width="560" height="315" src="https://www.youtube.com/embed/ctuOXMLATW4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Huananzhi X99-8M

<iframe width="560" height="315" src="https://www.youtube.com/embed/dIsU-rxj-l0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Machinist X99Z

<iframe width="560" height="315" src="https://www.youtube.com/embed/uW-8ljvNoQo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Runing X99 V1.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/oqxplG4wT8c" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### PlexHD / Atermiter X99

<iframe width="560" height="315" src="https://www.youtube.com/embed/FfIj0rU1hmA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>