# Arch Post Installation Instructions

Configure environment after a fresh installation

## Packages to install

### Main Repo Packages

redshift xfce4-panel nodejs ripgrep fd diskonaut xf86-video-amdgpu ansible tree
vim fish bspwm sxhkd fzf nnn shellcheck syncthing viewnior git rsync mousepad
virtualbox thunderbird chromium pcmanfm dmenu feh jq vagrant docker
grub-btrfs evince qbittorrent alacritty xdotool mesa p7zip jre-openjdk

### AUR Packages

kcc kindlegen hakuneko-desktop timeshift python-pywal

## Avoid screen tearing (tear free rendering)

Add this to `/etc/X11/xorg.conf.d/20-amd-gpu.conf`:

```
Section "Device"
        Identifier "AMD"
        Driver     "amdgpu"
        Option     "TearFree"  "true"
EndSection
```

## Deploy dotfiles

```
gti clone git@github.com:Andreiash/post-installation.git && ./dfiles/dfiles.sh
```

## Install vim-plug and plugins

```
curl -fLO HOME/.vim/autoload/plug.vim \
--create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
vim +PlugInstall +qall
```

## Other (optional)

### Set default shell for sxhkd to "sh"

```
cat "$HOME/.xinitrc" # check if file exists
echo -e '#!/bin/bash\nexport SXHKD_SHELL="/usr/bin/sh"' > "$HOME/.xinitrc"
```

### Remove pcspkr kernel module to disable system's beep sound

```
lsmod | grep '^pcspkr[[:space:]]\+' # check if beep is enabled
sudo modprobe -r pcspkr && echo "blacklist pcspkr" >> \
/etc/modprobe.d/50-blacklist.conf
```
