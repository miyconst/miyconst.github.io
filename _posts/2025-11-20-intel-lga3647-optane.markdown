---
layout: post
title:  "Intel LGA 3647 and Optane RAM"
date:   2025-11-20 10:00:00 +0100
categories: hardware
tags: optane ram pram lga3647 intel xeon gold platinum
background: "#0071c5"
color: white
---

- **The article was written by [Ford Morris](https://www.linkedin.com/in/ford-morris-82ba3b228/) for my Discord server**.
- **With his permission I publish the article on my blog with some edits**.
- The original document is available here: [PMEM Budget Build Info Doc](https://docs.google.com/document/d/1DgcsK-FA8_SGgbfSotEQkfK_DrepOUvCZ5IQ7avjMwI/edit?tab=t.0).

----------

So there's a problem right now with DDR4 memory prices, and trying to spec a budget workstation build with LGA 2011 v3, LGA 2066, or LGA 3647 is really difficult right now.
A single stick of 2666mHz ECC memory on ebay is ~$20-25 for 8gb, ~$40-45 for 16gb, ~$100 for 32gb, or ~$170 for a 64gb LRDIMM OR RDIMM (2133 mHz and 2400 mHz pricing is a little better though).

But there's one secret way to get huge memory pools without breaking the bank, Intel Optane Persistent Memory DCPMM modules (Not to be confused with Intel Optane Memory, a feature of the Optane SSDs).
These are DIMM modules that occupy ram slots, have huge capacities, much better speeds and durability than NAND Flash, and in memory mode, the system recognizes the Optane DIMMs as your actual memory, while treating your DRAM as an L4 cache.

Currently, the first gen DDR4-2666 Intel Optane memory modules, compatible with Xeon Scalable 2nd Generation, cost
- ~$30 for 128gb DIMMs, [Link 0](https://ebay.us/zH5zy2), [Link 1](https://ebay.us/Osm354).
- ~$80 for 256gb DIMMs, [Link 0](https://ebay.us/4QDPNa), [Link 1](https://ebay.us/M7Kk9q).
- ~$195 for 512gb DIMMs, [Link 0](https://ebay.us/spemJ2), [Link 1](https://ebay.us/gvNKJs). 

So the problem now is getting a cheap platform to use Optane memory. To do this, you need both a Gold or Platinum Second Gen Xeon Scalable CPU (Xeon Gold 52 or 62, Xeon Platinum 82), and a motherboard that explicitly supports it.

## CPU

The CPU is simple because Xeon Scalable Second Gen has some great budget options, despite not being as good of pricing as the first gen Xeon Gold 6138.
Here is a list of the top candidates I found, in no particular order

- [Xeon Gold 5218, ~$20, 16c, 2.3-3.9 GHz](https://ebay.us/sEWdFl).
- [Xeon Gold 6226, ~$30, 12c, 2.7-3.7 GHz](https://ebay.us/tu94hy).
- [Xeon Gold 6230, ~$40, 20c, 2.1-3.9 GHz](https://ebay.us/CiaTcG).
- [Xeon Gold 6240, ~$28, 18c, 2.6-3.9 Ghz](https://ebay.us/eqh2jG).
- [Xeon Gold 6242, ~$33, 16c, 2.8-3.9 Ghz](https://ebay.us/sygruP).
- [Xeon Platinum 8259CL, ~$40, 24c, 2.5-3.5 GHz](https://ebay.us/YKYN0Z).
- [Xeon Platinum 8269CY, ~$100, 26c, 2.5-3.8 GHz](https://ebay.us/bvNb75).

**Important**:
- Most motherboards require BIOS mod to work with CL CPUs.
- Most motherboards require VRM mod to work with >205 W TDP CPUs.
- Many motherboards require VRM mod to work with >165 W TDP CPUs.

## Motherboard

Next is the motherboard platform, where we are looking for LGA 3647 motherboards that support it.
Most of these were built for First Gen Xeon Scalable (Skylake) and need a bios update to support Second Gen Xeon Scalable (Cascade Lake).

The options we have are certain workstations like the [Dell T7820](https://ebay.us/dYScPB), [T7920](https://ebay.us/3DMdnp), [HP Z6 G4](https://ebay.us/plszy2), [Z8 G4](https://ebay.us/ukPO7a),
and L[enovo P920](https://ebay.us/DfqWbL), along with some different Supermicro X11 motherboards I found that are made for standard ATX form factors.
The other important information about these motherboards pertaining to Optane is the amount of DIMM slots.

Xeon Scalable 2nd Gen has 6 memory channels and up to 12 DIMM slots per socket. Intel generally wants one Optane DIMM and one DRAM DIMM per channel for optimal performance,
but vendors can bend the rules a bit when using less than 12 DIMM Slots.

The rule of thumb is this: If you have 2 slots for some memory channels, place the Optane PMEM in the slot closer to the CPU and DRAM in the further slot for those channels
and only DRAM for all other channels with just one slot. If your motherboard only has 6 memory slots and it supports PMEM, refer to the motherboard specific manual,
or the manuals for the 6 slot workstations and motherboards I linked down below.

Generally, you will get:
- 6 PMEM 6 DRAM with 12 slots.
- 4 PMEM 6 DRAM with 10 slots.
- 2 PMEM 6 DRAM with 8 slots.
- 2 PMEM 4 DRAM with 6 slots.
- 4 PMEM 2 DRAM with HP Z6 G4.

Here is an official install guide by Intel: [Configuring Intel® Optane™ DC Persistent Memory for Best Performance | Intel Business](https://youtu.be/MtP_iUZfMWM?si=Vy70BzMJLfTLcUHO).

## Potential builds

Here are some of the motherboards or workstations and details regarding building with them.
I listed all the ones I know, including bad deals in case you can find a better price.

### HP Z8 G4

- Price: ~$400.
- CPU: 2 sockets.
- RAM: 12 slots per socket.
- PSU: 1125W or 1450W.
- Link: [eBay](https://ebay.us/NdtNgs).

This listing requires you to buy the 1st and 2nd slot HP CPU Coolers for $90 each or risk a $50 Dynatron aftermarket cooler for each.
Yes the first and second slot have differently designed HP coolers.

When filling all memory slots, put PMEM in the white slots and DRAM in the black slots.
For all possible configurations, refer to pages 21 and 22 of [INTEL® OPTANE™ DC PERSISTENT MEMORY: CONFIGURATION AND SETUP ON HP Z6 G4 AND Z8 G4 WORKSTATIONS](https://h10032.www1.hp.com/ctg/Manual/c06527302.pdf).

### HP Z6 G4

- Price: ~$370.
- CPU: 1 socket + optional riser board with 2nd socket.
- RAM: 6 slots per socket.
- PSU: 1000W.
- Link: [eBay](https://ebay.us/4ZuH6g).

PMEM configuration is weird but good on this workstation, allows for 2 PMEM 4 DRAM or 4 PMEM 2 DRAM per CPU.
Refer to page 20 for configurations [INTEL® OPTANE™ DC PERSISTENT MEMORY: CONFIGURATION AND SETUP ON HP Z6 G4 AND Z8 G4 WORKSTATIONS](https://h10032.www1.hp.com/ctg/Manual/c06527302.pdf).

### Lenovo P920

- Price: ~$600.
- CPU: 2 sockets.
- RAM: 8 slots per socket.
- PSU: 1400W.
- Link: [eBay](https://ebay.us/3sJE3e).

I only know this is supported because the P920 is listed under two Optane PMEM related vulnerability firmware fixes.
I think you should put PMEM in the 2 black slots and DRAM in the 6 white slots for each socket, refer to X11DPH-T manual linked on next page for reference.

[Here](https://support.lenovo.com/us/en/product_security/ps500413-intel-optane-dc-persistent-memory-for-windows-advisory) Lenovo lists P920 as receiving this PMEM related security patch.
[Here](https://support.lenovo.com/us/en/product_security/ps500668-intel-optane-pmem-management-software-advisory) Lenovo lists P920 as receiving this PMEM related security patch.

You will have to also buy a CPU cooler for the second CPU if you want to add it, I didn't investigate too hard into the P920 though.

### Lenovo P720

Does not support PMEM (?), but regardless its a good deal for an LGA 3637 build.

- Link: [eBay](https://ebay.us/J6nzpk).

### Dell Precision T7920 

- Price: ~$650
- CPU: 2 sockets.
- RAM: 12 slots per socket.
- PSU: 1100W or 1400W.
- Link: [eBay](https://ebay.us/gs4NAn).

I know it supports Optane PMEM because it says so here 
[Dell Precision 7920 Tower Owner's Manual](https://www.dell.com/support/manuals/en-us/oth-xlt7920/precision_7920_om_pub/memory-specifications?guid=guid-adacc70e-307f-4e34-b97c-8114ca1353bf&lang=en-us).

It seems that you would fill the 6 black slots with PMEM and 6 white slots with DRAM, judging from pictures, but I can't find a guide.
Refer to the HP Z8 G4 manual link for configurations.

### Dell Precision T7820

- Price: ~$380.
- CPU: 1 socket + optional riser board with 2nd socket.
- RAM: 6 slots per socket.
- PSU: 950W.
- Link: [eBay](https://ebay.us/k4UodH), [eBay](https://ebay.us/qUfHa8).

I know it supports Optane PMEM because it says so here,
[Dell Precision 7820 Tower Owner's Manual](https://www.dell.com/support/manuals/en-us/precision-7820-workstation/precision_7820_om_pub/memory-specifications?guid=guid-644d2756-8b52-4142-a7dc-dc898ae38dcc&lang=en-us).
No specific guide on memory, try referencing either the HP Z6 G4 or Supermicro 6 slot guides.

### Supermicro X11SPM-F

- Price: ~$200.
- CPU: 1 socket.
- RAM: 6 slots per socket.
- Size: mATX.
- Link: [eBay](https://ebay.us/o0RA41).

I know the board supports Optane PMEM because it says so here: [X11SPM-F](https://www.supermicro.com/en/products/motherboard/x11spm-f).

Supported PMEM configuration (2 PMEM 4 DRAM per CPU) at page 15 here:
[MEMORY CONFIGURATION FOR X11 UP/DP/MP MOTHERBOARDS](https://www.supermicro.com/support/resources/memory/X11_memory_config_guide.pdf).

### Supermicro X11DPH-T

- Price: ~$279.
- CPU: 2 sockets.
- RAM: 8 slots per socket.
- Size: E-ATX.
- Link: [eBay](). (https://ebay.us/m/wVEkrR)

I know the board supports Optane PMEM because it says so here: [X11DPH-T](https://www.supermicro.com/en/products/motherboard/x11dph-t).

Supported PMEM configuration (2 PMEM 6 DRAM per CPU) at page 18 here:
[MEMORY CONFIGURATION FOR X11 UP/DP/MP MOTHERBOARDS](https://www.supermicro.com/support/resources/memory/X11_memory_config_guide.pdf).

Out of the deals I found, I think I would get a Xeon Gold 6240, HP Z6 G4, 2 x 128GB PMEM, and used 3090 or used quadros with NVLink for all my PyTorch shenanigans.
The max memory per socket for Z6 G4 is apparently 384GB with normal DRAM, but considering they allow for a 4 PMEM 2 DRAM configuration,
I am guessing PMEM doesn't play by the same rules but I am respecting it anyways.

## Final notes

Some things to remember if you are actually going through with a build like this:

- Update the BIOS to support Cascade Lake CPUS and PMEM before installing.
- Look for explicit PMEM support for the motherboard itself, not based on a product category or chipset; a lot of very similar Supermicro motherboards do not support PMEM.
- Do not confuse Intel Optane Memory technology, the SSD feature, with PMEM.
- Figure out how to set the PMEM to Memory Mode rather than Application Direct or Mixed Mode.
- Application Direct mode is where the PMEM shows as a storage block device rather than memory, and an app specific API can be used to address information in it without having to copy to DRAM first.
- Mixed mode is when some PMEM is in Memory Mode while some is in Application Direct Mode.
- Look for max memory limits with each workstation or motherboard.
- Get a T-30 Torx bit screwdriver for installing CPUs, potentially a torque screwdriver that helps you apply the exact correct amount of force.
- Here is Intel's guide and some Level 1 Techs discussion.
- [How to Install an Intel® Xeon® Processor into an LGA3647 Socket](https://www.intel.com/content/www/us/en/support/articles/000023869/processors/intel-xeon-processors.html).
- [LGA 3647 torque specs](https://forums.servethehome.com/index.php?threads/lga-3647-torque-specs.44342/).
- Have fun!