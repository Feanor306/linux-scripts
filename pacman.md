# PACKAGE MANAGER

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

## pacman config
sudo vim|nano /etc/pacman.conf
Color
ILoveCandy

## mirror list
vim|nano /etc/pacman.d/mirrorlist

## INSTALL AUR PACKAGE
clone git repo
makepkg -si

## File system usage
df -h