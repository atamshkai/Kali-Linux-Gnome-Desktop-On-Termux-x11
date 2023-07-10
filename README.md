# Kali-Linux-Gnome-Desktop-On-Termux-x11

This is a preinstalled Kali-Linux Distro with Gnome Desktop.For Android 12 & 13,before you install it , disable phantom process killer. 

[Watch Video Here](https://youtu.be/UxmQSETvAOc) 

## Preview ![](https://raw.githubusercontent.com/atamshkai/Kali-Linux-Gnome-Desktop-On-Termux-x11/main/kali-linux-gnome.png) 

# To Do 

#### First,Download Kali-Linux Distro From Here. 
[Download](https://archive.org/download/kali.tar.xz/kali.tar.xz) 

## Installation 
Download kali.tar.xz to Device's Download folder first. 

### Install zsh 
``` 
pkg up -y && pkg i -y zsh wget
wget https://github.com/atamshkai/Termux-Zsh/raw/main/zsh.tar.xz 
tar -xvJf zsh.tar.xz && mv zsh/.* ~/ && rm -rf zsh && chsh -s zsh 
``` 
#### Then, 
``` 
echo "killall pulseaudio &>/dev/null" >>~/.zshrc 
``` 
```
echo "pulseaudio --start --exit-idle-time=-1; pacmd load-module module-native-protocol-tcp auth-ip-acl=127.0.0.1 auth-anonymous=1" >>~/.zshrc 
``` 
``` 
pkg up -y && pkg i -y x11-repo && pkg i -y proot-distro pulseaudio termux-x11-nightly 
``` 
``` 
termux-setup-storage 
```
### Add Kali-linux to proot-distro
```
echo "DISTRO_NAME='Kali (kali)'" >>~/../usr/etc/proot-distro/kali.sh
```
### Restore Kali-Linux Distro
```
proot-distro restore /sdcard/download/kali.tar.xz 
``` 
``` 
exit 
``` 
#### Login again to terminal 
Before login to proot,start termux-x11 first. 
``` 
termux-x11 :1 
``` 
#### Then,open another session & login 
``` 
echo "proot-distro login kali --shared-tmp --bind /dev/null:/proc/sys/kernal/cap_last_cap" >>~/../usr/bin/kali
```
#### Start Kali
```
kali
```
#### Then 
``` 
export XDG_CURRENT_DESKTOP=GNOME
export PULSE_SERVER=127.0.0.1
export DISPLAY=:1
export XDG_SESSION_TYPE=x11
service dbus start
sleep 3
gnome-shell --x11 --sm-disable &
``` 
OR 
``` 
gnome 
``` 
### Warning 
If you upgrade the system,the desktop will fail to launch. 

#### Fix it 
``` 
for file in $(find /usr -type f -iname "*login1*"); do mv -v $file "$file.back" done 
``` 
``` 
echo "chmod u+s /usr/lib/dbus-1.0/dbus-daemon-launch-helper" >> ~/.bashrc 
``` 
``` 
mv -v /usr/share/applications/gnome-sound-panel.desktop /usr/share/applications/gnome-sound-panel.desktop.back 
``` 
``` 
echo "export XDG_CURRENT_DESKTOP=GNOME" >> ~/.bashrc 
``` 
Login again 
``` 
exit 
``` 
## Manual Installation
```
apt update && apt install -y dbus-x11 gnome-shell gnome-shell-extension-dashtodock gnome-tweaks gedit gnome-terminal gnupg yaru-theme-gnome-shell yaru-theme-icon yaru-theme-gtk gnome-shell-extensions firefox-esr parole audacious pulseaudio
```
### Note
zsh shell will fail to launch gnome terminal
## Termux 
[Download](https://github.com/termux/termux-app/releases/download/v0.118.0/termux-app_v0.118.0+github-debug_universal.apk) 
## Termux-x11 
[Download](https://archive.org/download/termux-x11/app-universal-debug.apk) 
## Termux-x11 Custom Resolution
1920:1080
