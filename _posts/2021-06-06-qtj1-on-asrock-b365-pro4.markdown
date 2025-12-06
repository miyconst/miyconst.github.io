---
layout: post
title:  "Core i9 QTJ1 on AsRock B365 Pro4"
date:   2021-06-06 08:58:43 +0100
categories: hardware cpu intel
tags: lga1151 b365 asrock bios coffeetime qtj1 qtj2 qqls qqlt
background: "#666666"
color: white
---

## ❗ My BIOS collection for LGA 1151 motherboards

- URL: [One Drive / Miyconst Hardware / LGA 1151](https://1drv.ms/u/s!AtZZXDjjb94kgaBNzu_leKHHQzHKdQ?e=sVNfe6).
- Password: `mi8`.

### Currently available motherboards:

- Gigabyte GA-Z170-HD3P.
- Asus Z170-P.
- Asus Rog Strix Z270H Gaming.
- AsRock B365 Pro4.
- MSI Z370-A Pro.

## BIOS modification using Coffee Time 0.92

- [AsRock B365 Pro4 official page](https://www.asrock.com/mb/intel/b365%20pro4/index.asp).
- [Download ready made BIOS for QTJ1, QJT2, QQLS, QQLT](https://1drv.ms/u/s!AtZZXDjjb94kgZwb5fMlbzMOdvc0GA?e=UTOYhR).
- [CH341a - minimal usage guide, how to read and write a motherboard BIOS](https://miyconst.github.io/hardware/2020/07/13/ch341a-guide.html).

### 1. Replace Intel Management Engine (IME)

Use `11.7.0.3307 | Corporate` version from the provided options.

![](/assets/2021-06-06-asrock-b365-pro4/step-00-ime.png)

### 2. Disable Intel Management Engine (IME)

![](/assets/2021-06-06-asrock-b365-pro4/step-01-ime.png)

### 3. Replace VBIOS

Use `1062` version from the provided options.

![](/assets/2021-06-06-asrock-b365-pro4/step-02-vbios.png)

### 4. Replace GOP driver

Use `9.0.1107` version from the provided options.

![](/assets/2021-06-06-asrock-b365-pro4/step-03-gop.png)

### 5. Apply red patches

**Important**: the `PCIe` patch is required for PCI-E slots. If the patch is not available it means that CoffeeTime is not able to properly apply it with the current BIOS. In this case you have to try an older version of your motherboard's BIOS.

![](/assets/2021-06-06-asrock-b365-pro4/step-04-patches.png)

### 6. Inject CPU microcodes

- `906ED`: Comet Lake QTJ1, QTJ2.
- `906EA`: Coffee Lake QNCT.
- `906EC`: Coffee Lake QQLT, QQLS.
- `506EB`: Kaby Lake QL3X, QL2X.
- `506E3`: Kaby Lake Xeon E3 V5.
- `906E9`: Kaby Lake Xeon E3 V6.


![](/assets/2021-06-06-asrock-b365-pro4/step-05-microcodes.png)
