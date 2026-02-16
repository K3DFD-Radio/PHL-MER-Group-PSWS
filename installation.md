### BIOS Settings
1. Boot the computer and bring you to the BIOS setup screen by using the key specific to your computer and make the following changes:
2. Smart CPU_Fan Mode -Full-On mode
3. AC Loss Control - Always On
4. Save and Exit

### Ubuntu Linux Installation
1. Create a bootable USB drive with Ubuntu 24.04 Server LTS
2. Boot target PC from USB drive. From options menu, select Try or Install Ubuntu Server with Enter
3. Configure for WiFi or Ethernet as appropriate. Connect to your network and note the MAC and IP addresses. Test the connection if possible
4. Deselect any option to set up disk as an LVM group. No compression or encryption.
5. Select Use Entire Disk for OS installation
6. Set up SSH and SFTP options if presented
7. Begin installation
8. When prompted, create a default user named 'wsprdaemon' with a password of your choice. Write the password down for future reference
9. When OS installation is complete, remove USB drive and reboot when prompted

### Update the OS
1. Login as wsprdeamon
2. Add the wsprdeamon user to the _sudo_ group
      - $sudo usermod -aG sudo wsprdaemon
4. Update the OS
      - $sudo apt update
      - $sudo apt update
5. Disable Snap if installed and running
      - $sudo apt autoremove --purge snapd gnome-software-plugin-snap
      - $sudo apt-mark hold snapd

### Dependency and Library Updates and Installations
1. There are a large number of dependencies and tools to be installed. 
      - sudo apt update && sudo apt install -y \
avahi-daemon avahi-discover avahi-utils btop build-essential \
flac gcc git iputils-ping libairspy-dev libairspyhf-dev \
libbsd-dev libfftw3-dev libhdf5-dev libiniparser-dev \
libmp3lame-dev libncurses-dev libogg-dev libopus-dev \
libopusfile-dev librtlsdr-dev libsamplerate-dev libsox-fmt-all \
libusb-1.0-0-dev libvorbis-dev mdns-scan net-tools nmap \
opus-tools portaudio19-dev tmux uuid-dev

2. Perform the above command. Should the make and compilation of ka9q-radio fail due to an unsatisfied dependency, it is most likely caused by a _legacy_ version not being installed. The compilation will generate error that may indicate which _legacy_ versions are not installed. In this case, refer to the table of dependencies in this [Legacy Library Link](https://docs.google.com/document/d/1jV4VKLIG7WG_zo5QeVL_GuvDyBTwUfN-SVxozEXIAcE/edit?usp=sharing) and install each one.

3. Next, to configure the system to run sudo commands without a password, add text to /etc/sudoers.d/wsprsudo using the Nano editor:
      - $sudo nano /etc/sudoers.d/wsprsudo
      - Add the line wsprdaemon ALL=(ALL) NOPASSWD: ALL:
      - Write the file and quit Nano


   

      
