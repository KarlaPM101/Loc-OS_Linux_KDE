#!/usr/bin/env bash

##################################################
## Limpiar Systemd
##################################################
apt purge *systemd* && update-grub
#reboot

##################################################
## Configurar APT
##################################################
wget -O /etc/apt/sources.list https://staging.karlaperezyt.com/locoskde/src/apt/sources.list.txt
wget -O /sbin/sources-final https://staging.karlaperezyt.com/locoskde/src/apt/sources-final.txt
wget -O /sbin/sources-media https://staging.karlaperezyt.com/locoskde/src/apt/sources-media.txt
apt update


##################################################
## Instalar KDE Plasma (base minima)
##################################################
apt -y install kde-plasma-desktop


reboot
