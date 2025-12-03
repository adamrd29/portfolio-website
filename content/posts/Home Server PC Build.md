+++
title = 'Home Server PC Build'
date = 2025-05-08T15:47:05+01:00
draft = false
+++
## Introduction
Maintaining control and privacy over the technology I use on a day-to-day basis has always been something that I have strived towards and when combined with my long-term interest of exploring technology, self-hosting became an very interesting avenue that I couldn't turn my head away from. The idea of running my own services instead of relying on third-party platforms presented the perfect opportunity to take control over my data while developing valuable skills in server management and system administration. With this in mind, I decided to build myself a server that would be the foundation of my journey.

### Platform
As the baseline for this build, the AM4 platform was selected for two key reasons: first and foremost it has support for ECC memory; As a server that is set to be operational 24/7, I wanted to prioritise reliability and I saw ECC as a key part of this. The second reason was availability. AM4 is a very mature platform with an abundance of hardware, making it a great way to get ECC memory at a reasonable price point. 

### Case - Jonsbo N2
The first objective of the server chassis was to be small, which this case manages excellently by being just 25cm in all directions. This case was also ideal for the hot-swap hard drive bays, keeping maintenance and expansion far easier than more closed-off cases. The final reason for this pick was purely aesthetics, this server will be fairly visible and I wanted to ensure that this server was never an eyesore, something which I believe this case manages excellently.

### Processor - AMD Ryzen 7 Pro 4750G
The Ryzen 7 Pro 4750G in particular was selected as there was no plan to add a dedicated GPU to this build and so an APU was needed so I could interface with the server for initial setup/future administration. However, as only the “Pro” series of AM4 APUs support ECC my choices to satisfy both conditions were limited to this particular line. To narrow the search, I began looking at the Ryzen 7 line of CPUs to give the server plenty of cores for high performance across multiple virtual machines. The final roadblock was the “Pro” series of Ryzen APUs are typically OEM only, limiting my options to the APUs available on the second hand market. This finally led me to the 4750G as I was able to source it for a good price from Ebay.


### CPU Cooler - AMD Wraith Stealth
This was a choice made out of convenience above anything else. As an OEM CPU there was no bundled CPU cooler and instead of sourcing an aftermarket cooler, I instead opted for the AMD Wraith Stealth as I just so happened to it in storage from when I built my Gaming PC. It meets the height limitations of the PC case, and has plenty of cooling capacity for my processor making it an acceptable choice. If I were to upgrade in the future I would look towards the Noctua NH-L12 Ghost S1 but for now that doesn't seem necessary.

### Motherboard - Gigabyte B550I AORUS PRO AX
For the motherboard I was limited to motherboards from either ASRock or Gigabyte as they seem to be the only manufacturers that consistently supported ECC memory across their models. Continuing on from this, the Gigabyte B550I AORUS PRO AX was an appealing choice due to it having multiple M.2 slots to maximise expansion in such a small form factor, as well as its integrated 2.5 gigabit NIC which will bre greatly appreciated when it comes to large file transfers across the local network.

### RAM - Micron 2x1​6GB DDR4-3​200 ECC UD​IMMs
While ECC was a clear requirement for this build, I also didn’t wish to sacrifice too much in terms of performance with how reliant Ryzen is on high speed memory, leading my search towards 3200MHZ RAM as this was the highest speed available for unregistered ECC UDIMMs. 32GB was selected as the overall capacity for this build for a balance between having plenty of RAM to work with, and cost effectiveness as unregistered ECC DIMMs can be quite pricey.

### Power Supply - Asus ROG LOKI 750 W 80+ Platinum
A reliable power supply was priority as unexpected power outages come with not only service disruptions, but potential for more severe issues like data corruption, this was why I went with a power supply that is regarded as among best in class for the SFX formfactor. On top of that, the Platinum efficiency rating helps keep the server’s power draw and heat output as low as possible, which is a nice bonus for a system that’s running 24/7. Furthermore, this power supply features a zero-rpm mode when running at low power and with the low power required by this server, it is likely that the fan will never have to spin, improving acoustic performance.


### Storage:
#### Boot Drive - Crucial MX500 500GB
With both M.2 drives on the motherboard set to be occupied for other uses, I instead looked towards SATA SSDs for my boot drive at the expense of some speed, which wasn't particularly important regardless. With a DRAM cache and Crucials reputation, I was confident that this drive would be plenty fast and reliable for this use case.

#### Hard Drives - 3x WD Red Plus 4TB: 
For my bulk storage I went with WD Red Plus drives as not only are they a reliable pick, they are also widely regarded as some of the quietest NAS focused hard drives, aligning them with the objective of keeping server noise minimal. Three 4TB drives were selected due to their excellent price to capacity and facilitating the use of the RAID Z1 configuration to keep one drive as parity. Furthermore, 8TBs of storage was more than plenty for my needs and using 3 out of 5 drive bays left me with room for expansion if I find it necessary in the future.


### Extras
#### Silverstone ECS07 M.2 SATA Expansion Card
A major limitation of the Mini-ITX platform within AM4 is that the motherboards max out at 4 SATA ports. With up to 5 Hard Drives and an SSD to attach, I found myself 2 SATA ports short. To address this I purchased a SATA expansion card which sacrifices an M.2 slot for 5 extra SATA slots, making it perfect as an attachment point for all five hard drive bays, while the boot SSD can simply use a motherboard sata port.

#### Google Coral M.2 TPU
At some point during the lifespan of this server, I also want to open up the possibility to run an NVR for completely local AI processing of home security cameras. To do this in a resource efficient way I looked towards the Coral series of TPU which are well supported amongst open source NVR systems such as Frigate. While another solution would've been a dedicated GPU, this seemed like a far less efficient option that went against this servers desire to keep power low.

#### Noctua NF-A12x25 120mm fan + Noctua NA-FG1-12 Sx2 Fan Grills
The 120x15mm fan and restrictive fan grill that come in with the Jonsbo N2 by default are known to be quite loud and would compromise the quiet operation of the system. To fix this, I replaced the Fan with the ever-popular Noctua NF-A12x25 attached to a Noctua fan grill that was far less restrictive than the one bundled with the case. Together I hoped this combination would help take me a step closer to my goal of silent operation while also improving the cooling performance of my hard drives.

### Operating System - Proxmox
For the operating system, I looked towards hypervisor OSs that would allow me the flexibility to run a variety of virtual machines and containers depending on the requirements of the service I am hosting, forming the backbone of my self-hosted stack. For this purpose Proxmox seemed like the easy choice as an open-source linux based OS that makes virtualisation management extremely easy from a web interface, meaning that I almost never have to interact with the server directly. The lack of license fees was also a huge positive, as it keeps my homelab more affordable as apposed to other hypervisor OSs such as EXSi.

## Issues
### Boot Drive Power
One delay that this build suffered was an inability to power the boot SSD as the sata power cable bundled with the power supply features only right angled cables which are incompatible with this case as the SSD sits right against the top shell, instead requiring a straight sata power cable. Fixing this required the ordering of a 30cm sata power cable from CableMod that could directly replace the multi-riight angled power. Upon arrival this cable cleared up this issue.


### SATA Backplane Cables
With the addition of a fan that was 10mm thicker than the one included, there was now very little space between the sata backplane and the fan grill. This required me to be very careful with my cable connector thickness as to not break the backplane through interference between cables and the fan. For this reason I ordered right angled sata cables as well as an adaptor that would allow me to power both molex connectors required by the backplane with a two right angled connectors. With this space saving, I was just about able to fit all of my cabling as well as the improved fan without requiring any modification to the case itself.