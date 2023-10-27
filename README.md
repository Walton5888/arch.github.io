# arch.github.io
# Installing Arch Linux on VMware Workstation for Mac

These instructions will guide you through the process of installing the Arch distribution of Linux on VMware Workstation for a Mac, and then installing the Gnome desktop envioirnment. 

## Requirements

- Install VMware Workstation.
- Download the Arch iso (https://archlinux.org/download/).
- Connect to the internet

## Step 1: Create a New Virtual Machine

1. Open VMware Workstation.
2. Click the 'File' tab and then ‘New Virtual Machine.'
3. When prompted to select an image file, select the installed Arch iso.
4. Follow the install guide, setting the proper parameters for adequate operation. 

## Step 2: Boot the Arch Linux Installation

1. Begin the initialization process of the VM.
2. Boot from the ISO and select 'Boot Arch Linux (x86_64)'.

## Step 3: Update System Clock and Update Packages

Execute the following command in your shell:
timedatectl set-ntp true #Syncs the system’s clock with NTP servers. 

## Step 4: Partitioning your disk
use cfdisk or fdisk to partition the disk to desired settings.

## Step 5: Mounting and Setting the Format for Partitions
Execute the following commands in your shell:
mkfs.ext4 /dev/sda1
mount/ /dev/sda1/mnt 
#These commands both format the partition and mount it to /mnt. 

## Step 6: Install the Arch System
Type the following command into your shell:
pacstrap /mnt base linux linux-firmware
#Install’s arch’s base system.

## Step 7: Create an fstab file.
Type the following command into your terminal:
genfstab -U /mnt >> /mnt/etc/fstab
# An fstab file is created to manage the mounts of the filesystem. 

## Step 8: Boot into the new system. 
Type the following command into your shell:
arch-chroot /mnt
#Boots into the Arch system.

## Step 9: Provide Time Zone
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
Replace the region and city sections with the time zone you reside in.

## Step 10: Set your preferred locale information
Type the following commands into your shell:
echo 'en_US.UTF-8 UTF-8' > /etc/locale.gen
locale-gen
echo 'LANG=en_US.UTF-8' > /etc/locale.conf
#Sets the character encoding, collation, and language preferences

##Step 11 Set Hostname 
Type the following command into your shell: 
echo 'your-hostname' > /etc/hostname
#Sets the user’s preferred name as the host. 

## Step 12: Set Network Configuration:
Type the following commands into your shell: 
#for wired connections
systemctl enable dhcpd
#Enables the network manager
systemctl enable NetworkManager 

## Step 13: Create System Users
Type the following commands into your shell:
# Create user 'codi'
useradd -m -g users -G wheel -s /bin/bash codi
# Set the password for 'codi'
passwd GraceHopper1906


# Creates user profile 'zane'
useradd -m -g users -G wheel -s /bin/bash zane
# Set login credentials for ‘zane'
passwd GraceHopper1906

##Step 14: Giving Users Sudo Permissions
Type the following commands into your shell.
#Switches the root user.
su
#Make changes to the sudoers file.
visudo
#Grants sudo permissions to users.
%wheel ALL=(ALL) ALL
#Grants sudo permissions to zane and codi users.
zane ALL=(ALL) ALL
codi ALL=(ALL) ALL
#Save and exit the file. 

## Step 15: Install a Bootloader
Type the following commands into your shell:
# Installs the GRUB bootloader
pacman -S grub
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg

## Step 16: Install a Desktop Environment (GNOME)
pacman -S xorg-server xorg-xinit gnome
systemctl enable gdm

## Step 17: Logout and Restart the System
exit
umount -R /mnt
reboot

## Step 18: Completion
#Your task is complete. 





