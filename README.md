# VM for Home Lab

## Hardware

Beelink SER5 Mini PC @ USD350
* AMD Ryzen 5 5560U 6 Core(Up to 4GHz)
* 16GB DDR4 RAM 
* 500GB NVME M.2 SSD
* Mini Desktop Computer Support Dual HDMI2.0 4K@60Hz Output
* WiFi 6
* BT 5.2
* USB-C 

## Software
Pre-installed with Win 11 Pro

## Enable Hyper-V on Win 11 Pro

To enable the Microsoft Hyper-V feature, you must first enable virtualization in the motherboard’s UEFI (Unified Extensible Firmware Interface), and you can turn on Hyper-V from the “Windows Features” settings. 

You can follow the steps documented here: [Step-By-Step: Enabling Hyper-V for Use on Windows 11](https://techcommunity.microsoft.com/t5/educator-developer-blog/step-by-step-enabling-hyper-v-for-use-on-windows-11/ba-p/3745905)

## Shared Folders over Hyper-V

Setting up shared folders in Hyper-V is not a conventional thing to do. Unlike VirtualBox, Hyper-V is not a desktop exclusive hypervisor. To share folders between guest OS running on Hyper-V and the host operating system, we will use SMB file share to share a folder created on host machine with the guest. 





