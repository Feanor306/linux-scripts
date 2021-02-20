# PACKAGE MANAGER (ARCH LINUX)

## Update all packages
sudo pacman -Syu

## Search for package
pacman -Ss {search text}

## Uninstall + remove dependencies
sudo pacman -Rns {package name}

## Clean up package cache
sudo pacman -Sc

## List all packages
pacman -Q  
pacman -Qe -> only explicitly installed, no dependencies  
pacman -Qe | wc -l -> get count  
pacman -Qeq -> removes version numbers  
pacman -Qn -> main repositories  
pacman -Qm -> AUR  
pacman -Qdt -> no longer required dependencies 

## Pacman config
sudo vim|nano /etc/pacman.conf  
Color -> Activate colors
ILoveCandy -> Pacman download bar

## Mirror list
vim|nano /etc/pacman.d/mirrorlist

## INSTALL AUR PACKAGE
[Arch Wiki](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_and_upgrading_packages)
clone git repo  
makepkg -si  

## File system usage
df -h