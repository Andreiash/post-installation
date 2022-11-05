# Arch Post Installation Instructions

Configure environment after a fresh installation

## Packages to install

### Main Repo Packages

redshift xfce4-panel nodejs ripgrep fd diskonaut xf86-video-amdgpu ansible tree
vim fish bspwm sxhkd fzf nnn shellcheck syncthing viewnior git rsync mousepad
virtualbox thunderbird chromium pcmanfm dmenu feh jq vagrant docker
grub-btrfs evince qbittorrent

### AUR Packages

kcc kindlegen hakuneko-desktop timeshift pywal fd

## Remove pcspkr kernel module to disable system's beep sound

```
lsmod | grep '^pcspkr[[:space:]]\+' # check if beep is enabled
MODPROBE_FILE="/etc/modprobe.d/50-blacklist.conf"
sudo modprobe -r pcspkr && echo "blacklist pcspkr" >> '"$MODPROBE_FILE"
```

## Modify xorg file to avoid screen tearing (AMD)

Add this to `/etc/X11/xorg.conf.d/20-amd-gpu.conf`.

```
'Section "Device"
        Identifier "AMD Graphics"
        Driver     "radeon"
        Option     "TearFree"  "true"
EndSection'
```

## Deploy dotfiles

```
git clone https://www.gitlab.com/Andreias/dfiles.git
cd dfiles
./dfiles/dfiles.sh
```

## Install base-devel and yay

```
command -v yay # first check if yay is installed
sudo pacman -S --needed git base-devel
git clone https://aur.archlinux.org/yay.git
cd yay && makepkg -si
```

## Install vim-plug and plugins

```
PLUG_URL="https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim"
PLUG_PATH="$HOME/.vim/autoload/plug.vim"
curl -fLo "$PLUG_PATH" --create-dirs "$PLUG_URL"
vim +PlugInstall +qall
```

## Set default shell for sxhkd to "sh"

```
cat ~/.xinitrc # first check and see if the file exists
printf '#!/bin/bash' > ~/.xinitrc
printf "export SXHKD_SHELL='/usr/bin/sh'\n" >> .xinitrc
```
