# ARCH LINUX INSTALL USING ARCHFI GUI

### Guides
[Chris Titus](https://www.youtube.com/watch?v=YbXHU7W7Its) 
[Techhut](https://www.youtube.com/watch?v=u2l54FMgWq4) 

## Create Bootable USB from ISO
[Download Arch](https://archlinux.org/download/)
**Windows** (DD image) -> [Rufus](https://rufus.ie/)
**Linux** 
dd if={path_to_arch_iso_file} of=/dev/sd{a|b|c} status="progress"

## Boot into Live ISO
**optional - install wget and pacman-contrib**
pacman -Sy
pacman -S wget pacman-contrib

## Determine if system is running EFI vs Legacy boot
ls /sys/firmware/efi/efivars  
if exists -> UEFI  

## GET ARCHFI SCRIPT
curl -L archfi.sf.net/archfi > archfi
sh archfi

## Partitions
GPT Partition table
/dev/sda1   -> if no UEFI, leave ~50MB formatted but without file system
/dev/sda2   -> ext4(if UEFI use FAT) /boot  300-500MB
/dev/sda3   -> linux-swap                   ~same size as RAM
/dev/sda4   -> ext4 /                       ~50GB
/dev/sda5   -> ext4 /home                   all remaining space
