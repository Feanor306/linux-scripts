# Artix GUI and Users
### Thanks to Luke Smith
[Luke After Fresh Artix Install Guide](https://www.youtube.com/watch?v=nSHOb8YU9Gw)  
**IF YOU INSTALL [larbs.xyz](https://larbs.xyz)**  
**IT DOES EVERYTHING IN THIS GUIIDE AUTOMATICALLY**  

## Create user and set password
useradd -m -g wheel feanor  
passwd feanor  

## Permissions for user
nano|vim /etc/sudoers  
**uncomment, all users of wheel group no pass req**  
%wheel ALL=(ALL) NOPASSWD: ALL   
**no need to reinsert password on different terminals**  
Defaults !tty_tickets  

## Install X.org
pacman -S xorg-server xorg-xinit

## Install i3 window manager
pacman -S i3-gaps i3status rxvt-unicode dmenu

## Install fonts
pacman -S ttf-linux-libertine ttf-inconsolata  
pacman -S noto-fonts  
**set fonts manually in XML**  
~/.config/fontconfig/fonts.conf  

## Auto X server starts i3
~/.xinitrc  
exec i3  

## Start X server
startx

## Switch TTY
CTRL + ALT + F{1-4} -> new tty  
ALT + LEFT / RIGHT -> change tty  

## xfce4 desktop environment alternative
pacman -S xfce4  
~/.xinitrc  
exec xfce4-session  

## Intel Graphics drivers
pacman -S xf86-video-intel libxrandr xorg-xrandr  
xrandr -> list resolution list  
**to add new resolution**  
[ARCH WIKI Xrandr page](https://wiki.archlinux.org/index.php/Xrandr#Adding_undetected_resolutions)  

## login
sudo pacman -S lightdm lightdm-gtk-greeter  
sudo systemctl enable lightdm.service  

## user startup and settings
~/.profile  
~/.bash_profile  

## generate terminal color scheme from walpaper
wal -i .config/wall.png

## Refresh BASH
source ~/.bashrc

## Recommended packages
**Notes**  
cherrytree vnotes zim  
**Fuzzy Search**  
fzf  
**Multithread Grep**  
ripgrep  
**Window managers (Also over SSH)**  
GNU screen  
tmux