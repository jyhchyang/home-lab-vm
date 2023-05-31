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

1. Search for “Turn Windows Features on or off” in the Start Menu 
2. Check the Service for NFS, SMB 1.0 and SMB Direct boxes.
3. Search for “Advanced Sharing Settings” in the Start Menu
4. Verify that Public Folder Sharing is Turned On
5. Check the box that does switch it on and save the changes
6. Create a Folder to keep our shareable contents. 
7. Right-click on this new folder, go to Properties → Sharing and Click on Share.
8. Copy the shared folder `\\PCName\Shared_Folder_Name` format.
9. On Linux guest, replace the backslashes to forward slashed, e.g. `//PCName/Shared_Folder_Name`
10. To access the contents of the shared folder, both the guest and host network should be on the same network.

If your guest VM uses the Default Switch option by Hyper-V to provide connectivity, then your VM can talk to the main Windows installation.
If your VM uses both Internal and External Switch (two virtual switches offered by hyper-V) it is important to note that both the host and guest must be on same network for SMB/CIFS file sharing to work.

## Mounting the Shared Folder on Guest

1. Install a simple cifs-client
```
$ sudo apt install cifs-utils
```

2. To mount it in a new directory called SharedFolder
```
$ mkdir ~/SharedFolder
```

3. To mount the folder, you need to tell Linux what your Windows user name is so it can authenticate against that name.
```
$ sudo mount.cifs //<NAME OF YOUR PC>/<SHARED FOLDER NAME> ~/SharedFolder -o user=<YOUR WINDOWS USERNAME>
```

4. To mount CIFS share permanently, create a credential file
```
nano ~/.smbcredentials
```

5. Insert the username and password for accessing the remote share:
```
username=administrator
password=password
```

6. To get your gid and uid
```
id <user_id>
```

7. Edit the fstab:
```
nano /etc/fstab
```

8. Add below line to the end and save it:
```
//<NAME OF YOUR PC>/<SHARED FOLDER NAME> /mnt/cifs cifs credentials=/<userid>/.smbcredentials,iocharset=utf8,gid=0,uid=0,file_mode=0777,dir_mode=0777 0 0
```








