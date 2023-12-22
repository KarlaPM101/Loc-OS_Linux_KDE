#!/usr/bin/env bash

##################################################
## Instalar Dependencias
##################################################

## Calamares y Refractasnapshot
apt -y install refractasnapshot-base calamares calamares-settings-loc-os

## LiveTools
apt -y install live-boot live-config-doc live-config-sysvinit live-config live-tools live-boot-initramfs-tools

## ISO Tools
apt -y install xorriso genisoimage squashfs-tools

## GVFS
apt -y install gvfs-common gvfs-daemons gvfs-libs gvfs

## SYSLinux
apt -y install syslinux syslinux-common

## Grub
apt -y install grub-efi grub-pc-bin

## GNUStep
apt -y install gnustep-base-common gnustep-base-runtime gnustep-common

## Polkit
apt -y install policykit-1 polkitd-pkla p11-kit

## Misc. Tools
apt -y install xorg zenity xapps-common uno-libs-private toilet tree unar caca-utils acl btrfs-progs cryptsetup gcr glpkg  gparted lynx mtools ntpsec user-setup yad libduktape207 mlocate keyutils

## Firmwares
apt -y install firmware-atheros firmware-b43-installer firmware-brcm80211 firmware-iwlwifi firmware-libertas firmware-linux-nonfree firmware-linux firmware-misc-nonfree firmware-qlogic firmware-realtek-rtl8723cs-bt firmware-realtek firmware-samsung

## Addons
apt -y install chromium kde-spectacle vlc kamera kate ark kcalc gwenview neofetch okular unrar-free unzip webapp-manager zip libreoffice-calc libreoffice-writer


##################################################
## Corrección locales
##################################################

echo "QT_QPA_PLATFORMTHEME=gtk2" > /etc/environtment

echo "
LANG=en_US.UTF-8
LC_ALL=en_US.UTF-8
LC_ADDRESS=en_US.UTF-8
LC_IDENTIFICATION=en_US.UTF-8
LC_MEASUREMENT=en_US.UTF-8
LC_MONETARY=en_US.UTF-8
LC_NAME=en_US.UTF-8
LC_NUMERIC=en_US.UTF-8
LC_PAPER=en_US.UTF-8
LC_TELEPHONE=en_US.UTF-8
LC_TIME=en_US.UTF-8
LANGUAGE=en_US.UTF-8
" > /etc/locale.conf

echo "KEYMAP=us
" > /etc/vconsole.conf

echo "America/New_York" > /etc/timezone

echo 'Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
        Option "XkbLayout" "us"
EndSection
' > /etc/X11/xorg.conf.d/00-keyboard.conf

echo "export LC_CTYPE=en_US.UTF-8
export LC_ALL=en_US.UTF-8" > /home/live/.bashrc

echo "export LC_CTYPE=en_US.UTF-8
export LC_ALL=en_US.UTF-8" > /root/.bashrc

echo "en_US.UTF-8 UTF-8
C.UTF-8 UTF-8" > /etc/locale.gen

locale-gen


##################################################
## Configurar Refractasnapshot
##################################################
wget -O /etc/refractasnapshot.conf https://staging.karlaperezyt.com/locoskde/src/refractasnapshot/refractasnapshot.etc_conf.txt
wget -O /usr/lib/refractasnapshot/iso/isolinux/splash.png https://staging.karlaperezyt.com/locoskde/src/refractasnapshot/splash.png
wget -O /usr/lib/refractasnapshot/snapshot_exclude.list https://staging.karlaperezyt.com/locoskde/src/refractasnapshot/snapshot_exclude.list.txt
apt -y remove amd64-microcode intel-microcode


##################################################
## Configurar Grub
##################################################
wget -O /etc/default/grub https://staging.karlaperezyt.com/locoskde/src/grub/grub.txt
wget -O /etc/default/grub.ucf-dist https://staging.karlaperezyt.com/locoskde/src/grub/grub.ucf-dist.txt
wget -O /etc/default/keyboard https://staging.karlaperezyt.com/locoskde/src/grub/keyboard.txt
wget -O /etc/default/locale https://staging.karlaperezyt.com/locoskde/src/grub/locale.txt
wget -O /etc/grub.d/10_linux https://staging.karlaperezyt.com/locoskde/src/grub/10_linux.txt

wget -O /tmp/grub_theme.tar.gz https://staging.karlaperezyt.com/locoskde/src/grub/theme_locos.tar.gz

mkdir -p /boot/grub/themes/Loc-OS/
tar -xf /tmp/grub_theme.tar.gz -C /boot/grub/themes/Loc-OS
rm /tmp/grub_theme.tar.gz

update-grub

##################################################
## Configurar Init
##################################################
wget -O /etc/initramfs-tools/initramfs.conf https://staging.karlaperezyt.com/locoskde/src/init/initramfs.conf.txt
wget -O /etc/initramfs-tools/conf.d/calamares-safe-initramfs.conf https://staging.karlaperezyt.com/locoskde/src/init/calamares-safe-initramfs.conf.txt
rm /etc/initramfs-tools/conf.d/resume

wget -O /etc/modprobe.d/amd64-microcode-blacklist.conf https://staging.karlaperezyt.com/locoskde/src/modprobe/amd64-microcode-blacklist.conf.txt
wget -O /etc/modprobe.d/intel-microcode-blacklist.conf https://staging.karlaperezyt.com/locoskde/src/modprobe/intel-microcode-blacklist.conf.txt

update-initramfs -u

##################################################
## Configurar PolicyKit
##################################################
mkdir -p /etc/PolicyKit
wget -O /etc/PolicyKit/PolicyKit.conf https://staging.karlaperezyt.com/locoskde/src/policykit/PolicyKit.conf.txt

##################################################
## Reemplazar NetworkManager a CMST
##################################################
apt -y install cmst
apt -y purge network-manager


reboot
