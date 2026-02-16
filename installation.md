### BIOS Settings
1. Boot the computer and bring you to the BIOS setup screen by using the key specific to your computer and make the following changes:
2. Smart CPU_Fan Mode -Full-On mode
3. AC Loss Control - Always On
4. Save and Exit

### Ubuntu Linux Installation
1. Create a bootable USB drive with Ubuntu 24.04 Server LTS
2. Boot PC from USB drive and from options menu, select Try or Install Ubuntu Server with Enter
3. Configure for WiFi or Ethernet as appropriate. Connect to you network and note the MAC and IP addresses. Test the connection if possible
4. Deselect any option to set up this disk as an LVM group
5. Select Use Entire Disk for OS installation
6. Set up SSH and SFTP options if presented
7. Begin installation
8. When prompted, create a default user named 'wsprdaemon' with a password of your choice. Write the password down for future reference
9. When OS installation is complete, remove USB drive and reboot when prompted

### Update the OS
1. Login as wsprdeamon
2. Update the OS
   *$sudo apt update
   *$sudo apt upgrade
3. Disable Snap if installed and running
   *$sudo apt autoremove --purge snapd gnome-software-plugin-snap
   *$sudo apt-mark hold snapd
