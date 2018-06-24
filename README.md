# Installing Ubuntu Desktop on PetaLinux (Xilinx ZC702 - Zynq-7000 AP SoC)

### Setp 1
Make 2 partitions on an USB drive, which would hold the bootable version of PetaUbuntu.

USB Device --
      
      -- Partition 1 should be more than 1.5 Gb and should be of FAT32 format. Partition 1 should be named as BOOT
      -- Partition 2 should be more than 2.5 Gb and should be of Ext3/Ext4 format, which is specifically used by Linux systems and most of the time not discorverable by other OS. Partition 2 should be named as rootfs.
    
*N.B.* You could name each parition anyhting you want but naming them as BOOT and rootfs would make it easier to remember which partition contains which kind of info for ZC702 to be booted up.
More on partitioning the USB drive could be found from http://www.wiki.xilinx.com/Prepare+Boot+Medium

### Setp 2
Download the latest version of *PetaLinux* from http://www.wiki.xilinx.com/Zynq+Releases

For this example I clicked on the *Zynq 2018.2 Release* and then went to the Donwload section to download the *2018.2-zc702-release.tar.xz* file for ZC702 Zynq model.

After downloading the zip file, open terminal. I am assuming that you are using Linux system yourself to create PetaLinux bootable version for your ZC702.

Go to the download folder in the terminal such as -->

      $ cd Downloads
      $ tar xf 2018.2-zc702-release.tar.xz
     
You would see that all the contents of the compressed file would be extracted to a file in the same folder with name, "2018.2-zc702-release". Investigate the contents of the folder. This folder should consist of the following files:
     
     -- BOOT.BIN
     -- image.ub
     -- system.bit
     -- system.dtb
     -- u-boot.elf
     -- zynq_fsbl.elf
     
Use the following command to copy the files to Partition 1 (BOOT) of the bootable USB as follows:

    $ sudo mount /dev/sdc1 /media/username/BOOT
    $ cp -r 2018.2-zc702-release/* /media/username/BOOT
    $ umount /dev/sdc1
    
*N.B.* Use a device manager to investigate the mounting port for both the paritions of the bootable USB. FOr my OS (Ubuntu), the mounting devices were /dev/sdc1 and /dev/sdc2 respectively. And in order to access these paritions I had to navigate to /media/my_username/BOOT and /media/my_username/rootfs respectively. Here, replace my_username / username with your appropriate username for similar systems.

*Good news, we are half done!*

Now, you need to download the rootfs files required for partition 2 of the bootable USB. 
According to http://www.wiki.xilinx.com/Ubuntu+on+Zynq you need to download the rootfs folders/files, which is the root file system based on Ubuntu's core file system in particular the armhf release of Ubuntu 12.10 (Quantal Quetzal). But since this version is very old and ubuntu-core is now renamed to ubuntu-base. But since Xlinix ZC702 uses arm based optimisation, which is only provided in the armhf release of Ubuntu 12.10 (Qunatal Quetzal), you need to download it from the following link:

http://www.wiki.xilinx.com/file/view/zynq-ubuntu-core-12.10-core-armhf-rootfs.tar.xz/423293908/zynq-ubuntu-core-12.10-core-armhf-rootfs.tar.xz

[To be continued....]
