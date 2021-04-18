# Arch Linux Installation Guide
### Guides
[Luke Smith Arch install video](https://www.youtube.com/watch?v=4PBqpX0_UOc) 
[Distro Tube Arch install video](https://www.youtube.com/watch?v=PQgyW10xD8s)
[Arch Wiki Install](https://wiki.archlinux.org/index.php/Installation_guide)

## Create Bootable USB from ISO
[Download Arch](https://archlinux.org/download/)
**Windows** (DD image) -> [Rufus](https://rufus.ie/)
**Linux** 
dd if={path_to_arch_iso_file} of=/dev/sd{a|b|c} status="progress"

## Determine if system is running EFI vs Legacy boot
ls /sys/firmware/efi/efivars  
if exists -> UEFI  

## Check partitions
lsblk -> check partitions

## Make sure internet connection is up
ping 8.8.8.8
**wifi-menu on laptop**

**NOTE**  
**the rest of this guide we will use "sdc" partition**  
**change it to sd{a|b|c} according to your needs**  

## Format partitions
fdisk /dev/sdc -> format partition sd{a|b|c}  
**delete all partitions**
d {partition_id} -> delete partition_id  
p -> list partitions  

**sdc1** -> **boot partition**  
n (p/e) (default partition_num) (default first_sector) (+1G last_sector)  
**sdc2** -> ****
n (p/e) (default partition_num) (default first_sector) (+30G last_sector)  
**sdc3**  
n (p/e) (default partition_num) (default first_sector) (default last_sector)   
**swap** -> **swap partition for hibernation**
use ~150% of your RAM as second partition (sdc2)

w -> write new partitions to disk  

## Set file system for partition
mkfs.ext4 /dev/sdc3  
mkfs.ext4 /dev/sdc2  
mkfs.ext4 /dev/sdc1  
**Must use FAT for UEFI boot systems**  
mkfs.FAT -F32 /dev/sdc1  
**if you have swap as /dev/sdc2**
swapon /dev/sdb2

## Set mountpoints for partitions
mount /dev/sdc2 /mnt  
mkdir /mnt/home  
mkdir /mnt/boot  
mount /dev/sdc1 /mnt/boot  
mount /dev/sdc3 /mnt/home  

## Install Arch & Linux
pacstrap /mnt base base-devel linux linux-firmware vim

## Set mounting at boot in file
genfstab -U /mnt >> /mnt/etc/fstab  

## Get into installed OS
arch-chroot /mnt  
bash (if not in bash)  

## Setup network
### Install network manager 
pacman -S networkmanager 
### Auto-start NetworkManager
systemctl enable NetworkManager
### Create hostname and hosts
vim|nano /etc/hostname -> {hostname} like desktop  
vim|nano /etc/hosts  

```
127.0.0.1        localhost  
::1              localhost  
127.0.1.1        myhostname.localdomain	myhostname
```

## Install Grub
pacman -S grub 

**Classic Boot**  
grub-install --target=i386-pc /dev/sdc  
**UEFI**  
grub-install --target=x86_64-efi --efi-directory=esp --bootloader-id=GRUB  

**Generate grub config**  
grub-mkconfig -o /boot/grub/grub.cfg  

## Set system password
passwd  

## Set system clock & Locale
**use double TAB path completion**  
ln -sf /usr/share/zoneinfo/(Region)/(City) /etc/localtime  
**check if it was successful**  
ls -l /etc/localtime  
**hardware clock**  
hwclock --systohc  
**uncomment desired locales**  
vim|nano /etc/locale.gen  
**generate locales**  
locale-gen  
**set system locale**  
vim|nano /etc/locale.conf  
LANG=en_US.UTF-8 