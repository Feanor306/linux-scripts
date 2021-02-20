# Artix Linux Installation Guide
### **Thanks to Luke Smith**  
[Luke Smith Artix install video](https://www.youtube.com/watch?v=nCc_4fSYzRA)  
[Artix Wiki Install](https://wiki.artixlinux.org/Main/Installation)  

## Create Bootable USB / CD
[Download Artix](https://artixlinux.org/download.php)  
base-runit latest release  

## Boot, install
After artix boot log in as  
Artix login: root  
Password: artix  

## Determine if system is running EFI vs Legacy boot
ls /sys/firmware/efi/efivars  
if exists -> UEFI  

## Check partitions
lsblk -> check partitions
  
**NOTE**  
**the rest of this guide we will use "sdc" partition**  
**change it to sd{a|b|c} according to your needs**  

## Format partitions
fdisk /dev/sdc -> format partition sd{a|b|c}  
d {partition_id} -> delete partition_id  
p -> list partitions  

**sdc1**  
n (p/e) (default partition_num) (default first_sector) (+1G last_sector)  
**sdc2**  
n (p/e) (default partition_num) (default first_sector) (+30G last_sector)  
**sdc3**  
n (p/e) (default partition_num) (default first_sector) (default last_sector)   

w -> write new partitions to disk  

## Set file system for partition
mkfs.ext4 /dev/sdc3  
mkfs.ext4 /dev/sdc2  
mkfs.ext4 /dev/sdc1  
**Must use FAT for UEFI boot systems**  
mkfs.FAT -F32 /dev/sdc1  

## Set mountpoints for partitions
mount /dev/sdc2 /mnt  
mkdir /mnt/home  
mkdir /mnt/boot  
mount /dev/sdc1 /mnt/boot  
mount /dev/sdc3 /mnt/home  

## Install Artix & Linux
basestrap /mnt base base-devel runit elogind-runit linux linux-firmware  

## Install text editor
pacman -S nano  
pacman -S vim|nvim  

## Set mounting at boot in file
fstabgen -U /mnt >> /mnt/etc/fstab  

## Get into installed OS
artix-chroot /mnt  
bash (if not in bash)  

## Re-arrange mirror list for better download speed
vim|nano /etc/pacman.d/mirrorlist  

## Set system clock
**use double TAB path completion**  
ln -sf /usr/share/zoneinfo/(Region)/(City) /etc/localtime  
**check if it was successful**  
ls -l /etc/localtime  
**hadware clock**  
hwclock --systohc  
**uncomment desired locales**  
vim|nano /etc/locale.gen  
**generate locales**  
locale-gen  
**set system locale**  
vim|nano /etc/locale.conf  
LANG=en_US.UTF-8 

## Setup network
### Install network manager and dhcp client
pacman -S networkmanager networkmanager-runit  
pacman -S dhcpcd  
### Auto-start NetworkManager
ln -s /etc/runit/sv/NetworkManager/ /etc/runit/runsvdir/current  
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

## Get LARBS
reboot and login as root   
[larbs.xyz](https://larbs.xyz)  

```
curl -LO larbs.xyz/larbs.sh  
sh larbs.sh  
```