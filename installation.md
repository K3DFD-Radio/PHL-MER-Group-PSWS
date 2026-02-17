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
6. Set up SSH option if presented
7. Begin installation
8. When prompted, create a default user named 'wsprdaemon' with a password of your choice. Write the password down for future reference
9. When OS installation is complete, remove USB drive and reboot when prompted

### Update the OS
1. Login as wsprdeamon
2. Add the wsprdeamon user to the _sudo_ group
      - $sudo usermod -aG sudo wsprdaemon
4. Update the OS
```      
      sudo apt update
      sudo apt update
```
5. Disable Snap if installed and running
``` 
      sudo apt autoremove --purge snapd gnome-software-plugin-snap
      sudo apt-mark hold snapd
```
6. If not automatically created, create a wsprdaemon home directory and set permissions
```
      sudo mkdir /home/wsprdaemon
      sudo chown wsprdaemon:wsprdaemon /home/wsprdaemon
      sudo chmod 755 /home/wsprdaemon
```
8. As a precaution, force change your shell evironment to _bash_ instead of _sh_
```
      sudo chsh -s /bin/bash wsprdaemon
```
10. Exit and log back in again as user _wsprdaemon_
     
### Set the system up for automatic reboot in case of power failure. 
> ** Note ** This is optional for systems without battery backup
1. Create systemd override directory
```
      sudo mkdir -p /etc/systemd/system/getty@tty1.service.d
      sudo nano /etc/systemd/system/getty@tty1.service.d/autologin.conf
      sudo systemctl daemon-reload
      sudo systemctl enable getty@tty1.service
```
### Establish a TMux session to run wsprdaemon and btop monitoring. This session starts when wsprdaemon logs in
1. Install TMux
```
      sudo apt install tmux
```
3. Install Btop
```
      sudo apt install btop
```
4. Edit _wsprdaemon_ user environment to start _wsprdaemon_ and _btop_
```
      nano ~/.bash_profile
```

### Auto-start tmux session for PSWS monitoring and create the session if it does't exist
1. Edit the wsprdaemon user's ~/.bash_profile and add the following lines
```
      if [[ -z "$TMUX" ]] && [[ -n "$SSH_TTY" || "$(tty)" == "/dev/tty1" ]]; then
          if ! tmux has-session -t psws 2>/dev/null; then
              # Create new session with btop
              tmux new-session -d -s psws -n monitoring 'btop'
              tmux new-window -t psws -n wsprdaemon
              tmux new-window -t psws -n bash
              tmux select-window -t psws:bash
      fi
    tmux attach-session -t psws
fi
```
2. Save ~/.bash_profile

3. Test
```
      exit
```
4. If this test fails and tmux does not start, edit the ~/.bashrc with the same lines and $exit again

### Dependency and Library Updates and Installations
1. There are a large number of dependencies and tools to be installed. 
```
$sudo apt update && sudo apt install -y \
avahi-daemon avahi-discover avahi-utils btop build-essential \
flac gcc git iputils-ping libairspy-dev libairspyhf-dev \
libbsd-dev libfftw3-dev libhdf5-dev libiniparser-dev \
libmp3lame-dev libncurses-dev libogg-dev libopus-dev \
libopusfile-dev librtlsdr-dev libsamplerate-dev libsox-fmt-all \
libusb-1.0-0-dev libvorbis-dev mdns-scan net-tools nmap \
opus-tools portaudio19-dev tmux uuid-dev
```
2. Perform the above dependency and utils installations. Should wsprdaemon (and possibly ka9q-radio) fail to run due to an unsatisfied dependency, it is most likely caused by a _legacy_ version not being installed. In this case, refer to the table of dependencies in this [Legacy Library Link](https://docs.google.com/document/d/1jV4VKLIG7WG_zo5QeVL_GuvDyBTwUfN-SVxozEXIAcE/edit?usp=sharing) and install each one.

3. Install an ssh server and start it. This is to allow access for administration from authorized clients. Suggest Putty ssh client.
```
      sudo systemctl enable ssh
      sudo systemctl start ssh
      sudo systemctl status ssh
```
4. Confirm that ssh is running. Look for message 'Starting ssh.server - Open BSD Secure Shell server... Server listening on 0.0.0.0 port 22

5. Configure UFW to allow ssh on port 22
   ```
      sudo ufw allow ssh
      sudo ufw enable ssh
      sudo ufw status
   ```
6. Get the PC's IP address and note it
```
      ip addr show
```
7. Next, to configure the system to run sudo commands without a password, add text to /etc/sudoers.d/wsprsudo using the Nano editor:
```
      sudo nano /etc/sudoers.d/wsprsudo
```
8. Write the following line to the file, save and quit
```
      wsprdaemon ALL=(ALL) NOPASSWD: ALL:      
```
> **Note:** If Nano fails with permission errors, use redirect as follow to write directly to the /etc/sudoers.d/wsprsudo file\
```
      touch /etc/sudoers.d/wsprsudo\
      echo "wsprdaemon ALL=(ALL) NOPASSWD: ALL:" | sudo tee /etc/sudoers.d/wsprsudo
```
9. This completes the essential build of the Ubuntu 24.04 Server LTS instance. Directions for installing useful Linux tools and performance monitoring utilities will be provided in the [optimization] file.

10. Next, click on this [Configuration](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/configuration.md) link to install and configure the WSPRdaemon SDR environment, which includes the ka9q-radio application



   
