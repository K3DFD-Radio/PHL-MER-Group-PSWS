# **HamSCI Personal Space Weather Station - K3DFD Adaptation**

## **HF RX888 WSPRdaemon Receiver — Installation & Configuration Guide**

---

## **Overview**

The HF RX888 WSPRDaemon Receiver is the core HF listening component of the HamSCI Personal Space Weather Station (PSWS). This guide walks through the complete setup: configuring the BIOS, installing Ubuntu Server - with improved usability modifications, setting up the Leo Bodnar GPS-disciplined oscillator and RX-888 MkII SDR, running the wsprdaemon software and connecting to the HamSCI servers.

---

## **Part 1 — BIOS Configuration**

Before installing the OS, you may to configure two important BIOS settings on the Beelink mini PC: fan speed (to prevent overheating) and power-loss behavior (so the system restarts automatically after a power outage). This only applies if you are using the recommended Beelink PC.

1. Plug in the Beelink PC and connect it to a monitor via HDMI or DisplayPort. Connect a keyboard — no mouse is needed.  
2. Power on the PC and immediately tap **Delete** repeatedly to enter the BIOS setup screen. If the OS boots instead, shut down and try again.  
3. Once in BIOS, navigate to the **Advanced** tab using the arrow keys.  
4. Go to **Smart Fan Function → Smart CPU\_Fan Mode**, then select **Full On Mode**. Press **Escape** to return to the Advanced tab.  
5. Go to **AMD CBS → FCH Common Options → Ac Power Loss Options → Ac Loss Control**, then select **Always On**. Press **Escape** to return to the Advanced tab.  
6. Navigate to **Save & Exit → Save Changes and Exit**, then confirm with **Yes**.

The system will now restart automatically after power outages, and the fans will always run at full speed.

---

## **Part 2 — Installing Ubuntu Server**

### **Preparing the Installation Media**

You'll need a USB flash drive with at least 8 GB of space and an Ubuntu Server **24.04 LTS** .iso disk image, downloaded from the [Ubuntu website](https://ubuntu.com).

**On Windows 10/11 — using Rufus:**

1. Download and open [Rufus](https://rufus.ie).  
2. Insert the USB drive and select it from the **Device** dropdown.  
3. Click **Select** and navigate to the Ubuntu .iso file.  
4. Make sure **File System** is set to **FAT32** (not NTFS).  
5. Click **Start** and confirm that the drive will be erased. Accept the default formatting option if prompted.  
6. When complete, eject and remove the USB drive.

**On macOS or Linux — using Balena Etcher:**

1. Download and open [Balena Etcher](https://etcher.balena.io).  
2. Insert the USB drive.  
3. Click **Flash from File** and select the Ubuntu .iso.  
4. Click **Select Target** and choose your USB drive.  
5. Click **Flash\!** and wait for it to finish. Eject and remove the USB drive when done.

### **Running the OS Installer**

1. With the PC powered off, insert the USB drive.  
2. Power on the PC and immediately and repeatedly press **F7** to enter the Boot Menu. *(If you're using a different PC, look up its boot menu key.)*  
3. In the Boot Menu, select the USB drive. If both a **UEFI** and a non-UEFI option appear, choose the **UEFI** option.  
4. A menu will appear. Select **Try or Install Ubuntu Server** and press **Enter**. Scrolling text is normal — everything is working.  
5. Select **English** as your language and press **Space**.  
6. Leave the keyboard layout at its default and select **Done**.  
7. Scroll to **Ubuntu Server (minimized)**, select it with **Space**, then move down to **Done** and press **Enter**. 

### **Connecting to the Network**

**If using wired Ethernet:** Simply plug in the cable and skip to step 4 below, otherwise if using Wi-Fi:**

1. On the network screen, find the **wlo1** section. Below it you'll see a MAC address (formatted like 12:34:a5:b6:7c) — write this down, as you may need it to register the device on a university or institutional network.  
2. Select **wlo1**, choose **Edit Wifi**, then **Choose a visible network**, and connect to your Wi-Fi network.  
3. Leave the proxy address blank and select **Done**.  
4. Wait for the network test to complete. When the top of the screen reads **This mirror location passed tests**, select **Done**.

### **Finishing the Installation**

1. If prompted to update the installer, select **Update to the new installer** and wait.  
2. On the storage configuration screen, **deselect** the option labeled **Set up this disk as an LVM group** (the brackets should be empty). Leave **Use an entire disk** enabled. Select **Done**.  
3. Review the storage summary and select **Done**, then confirm the destructive action by selecting **Continue**.  
4. Set up your user account. **Recommended username: wsprdaemon.** Whatever you choose, write down both the username and password. Select **Done**.  
5. On the Ubuntu Pro screen, select **Skip for Now**.  
6. Configure SSH if desired (useful if you have a VPN and want remote access), then continue.  
7. Select any applicable third-party drivers, then **Continue**.  
8. Do not install any extra software from the next screen — select **Done**.  
9. Wait 5–10 minutes for installation to complete. When **Reboot Now** appears, select it.  
10. When prompted to remove the installation media, remove the USB drive and press **Enter**.

---

## **Part 3 — Configuring the Operating System**

### **Log In and Update the System**

Log in with the username and password you created. Then run the following commands to update all pre-installed software. You'll be prompted for your password, and may be asked to confirm with **y**:
```
sudo apt update  
sudo apt upgrade
```
Wait for each command to finish — you'll know it's done when the terminal prompt reappears as \[username\]@\[server-name\]:\~$.

Next, disable **snap** (a software management tool that can auto-update programs and interfere with wsprdaemon's scripts):
```
sudo apt autoremove \--purge snapd gnome-software-plugin-snap  
sudo apt-mark hold snapd
```

### **Install Prerequisites**

Install the required tools and libraries with the following command (type **y** to any prompts):
      
```
sudo apt install btop nmap git tmux vim net-tools iputils-ping avahi-daemon libnss-mdns mdns-scan avahi-utils avahi-discover build-essential make cmake gcc libairspy-dev libairspyhf-dev libavahi-client-dev libbsd-dev libfftw3-dev libhackrf-dev libiniparser-dev libncurses5-dev libopus-dev librtlsdr-dev libusb-1.0-0-dev libusb-dev portaudio19-dev libasound2-dev uuid-dev rsync sox libsox-fmt-all opus-tools flac tcpdump libhdf5-dev libsamplerate-dev
```

### **Allow Password-Free sudo**

wsprdaemon's scripts require the ability to run sudo commands without a password prompt. To configure this:

1. Optional: Install the **neovim** text editor or just use the Nano editor.

```
sudo apt install neovim
```

2. Open the sudoers configuration file:

```
sudo nvim /etc/sudoers.d/wsprsudo
```

3. Enter insert mode and type the following <ins>exactly</ins>:

```
wsprdaemon ALL=(ALL) NOPASSWD: ALL
```

4. Press **Escape**, then type :wq\! and press **Enter** to save and exit. *(The \! is needed because the directory is write-protected.)*

---

## **Part 4 — Installing wsprdaemon**

Install **git** and then clone the wsprdaemon repository:

```
sudo apt install git  
cd \~  
git clone https://github.com/rrobinett/wsprdaemon.git  
cd wsprdaemon  
./wsprdaemon.sh \-V
```

This will run the setup script and create a template configuration file for you to edit.

---

## **Part 5 — Configuring wsprdaemon**

### **Gather Your Station Information First**

Before editing the configuration file, you'll need:

* Your FCC callsign (or club/university callsign, or a short nickname)  
* Your **Maidenhead grid square** — look yours up at [https://www.levinecentral.com/ham/grid\_square.php](https://www.levinecentral.com/ham/grid_square.php) using your callsign or ZIP code. It will look like AA11aa.  
* A **PSWS account** with a Station ID and Token (see below).

### **Set Up Your PSWS Account**

1. Create an account at the [PSWS Central Control System website](https://pswsnetwork.caps.ua.edu/home).  
2. Go to the **Station** tab and click **Add New Station**. Fill out the form:  
   * **Station Nickname:** Include your callsign, and your organization name if applicable.  
   * **Grid Square:** Same one you found above.  
   * **Elevation:** In meters above sea level.  
   * **Antenna:** Describe your antenna setup.  
   * Add your address and contact info, then click **Add Station**.  
3. Select **View My Stations** and note your **Station ID** — it looks like S000111.  
4. Click your station and note your **Token** — a long string of letters and numbers. This is your secret authentication key.  
5. Scroll down and click **Add New Instrument**. Fill out the form:  
   * **Instrument:** e.g., RX-888 MK II \- Beelink Mini PC  
   * **Date Instrument Added / Removed:** As appropriate.  
   * **Nickname:** Useful if you have multiple instruments.  
   * **Serial Number:** From your RX-888.  
   * **Status:** Operational or inactive.  
   * **Instrument Type:** Select **rx888** from the dropdown.  
6. Click **Add Instrument** and note your **Instrument ID** — it looks like 111.

Your full GRAPE\_PSWS\_ID will be S000111\_111 (Station ID underscore Instrument ID).

### **Edit the Configuration File**

From inside the \~/wsprdaemon directory, open the config file:

bash  
nvim wsprdaemon.conf

Press **i** to enter insert mode. Replace any existing contents with the following, substituting your own values for all placeholders in \< \>:

bash  
**\#\!/bin/bash**  
\#\#\# The previous line signals to the vim editor that it should use its 'bash' editing mode when editing this file

WD\_CPU\_CORES\="8-15"  
RADIOD\_CPU\_CORES\="0-7"

KA9Q\_RADIO\_COMMIT\="main"  
KA9Q\_CONF\_NAME\="rx888-wsprdaemon"  
KA9Q\_WEB\_COMMIT\_CHECK\="main"  
KA9Q\_WEB\_TITLE\="\<Your Callsign\>"

\#\#\# Since these wav files are uncompressed audio they are quite large.  A 30 minute wav file which might contain a FST4W-1800 signal will be almost 50 MBytes  
\#\#\# To avoid overflowing the \~/wsprdaemon/wav-archive.d file system, if that wave file will fill more than 75% of the file system, then some of the oldest wav files are deleted first  
ARCHIVE\_WAV\_FILES\="yes"

\#\#\# Whether and how to upload extended spots to wsprdaemon.org.  WD always attempts to upload spots to wsprnet.org  
SIGNAL\_LEVEL\_UPLOAD\="yes"  
\#\#\# SIGNAL\_LEVEL\_UPLOAD="no"         \=\> (Default) Only upload spots directly to wsprnet.org   

SIGNAL\_LEVEL\_UPLOAD\_MODE\="noise"      
\#\#\# SIGNAL\_LEVEL\_UPLOAD\_MODE="noise" \=\> In addition, upload extended spots and noise data to wsprdaemon.org  
\#\#\# SIGNAL\_LEVEL\_UPLOAD\_MODE="proxy" \=\> Don't directly upload spots to wsprdaemon.org.  Instead, after uploading extended spots and noise data to wsprdaemon.org have it regenerate and upload those spots to wsprnet.org          
\#\#\# This mode minimizes the use of Internet bandwidth, but makes getting spots to wsprnet.org dependent upon the wsprdameon.org services.

\#\#\# If SIGNAL\_LEVEL\_UPLOAD in NOT "no", then you must modify SIGNAL\_LEVEL\_UPLOAD\_ID from "K2MFF" to your call sign.  SIGNAL\_LEVEL\_UPLOAD\_ID cannot include '/  
SIGNAL\_LEVEL\_UPLOAD\_ID\="\<Your Callsign\>"      
\#\#\# The name put in upload log records, the title bar of the graph, and the name used to view spots and noise at that server

SIGNAL\_LEVEL\_UPLOAD\_GRAPHS\="yes"     
\#\#\# If this variable is defined as "yes" AND SIGNAL\_LEVEL\_UPLOAD\_ID is defined, then FTP graphs of the last 24 hours to http://wsprdaemon.org/graphs/

SIGNAL\_LEVEL\_LOCAL\_GRAPHS\="yes"      
\#\#\# If this variable is defined as "yes" AND SIGNAL\_LEVEL\_UPLOAD\_ID is defined, then make graphs visible at http://localhost/

\#\#\# These two variables need to be defined in order to enable this WD GRAPE service:

\#\#\# If this and GRAPE\_PSWS\_TOKEN are both defined, then each day soon after 00:00 UDT WD will upload the previous day's 24\_hour\_10sps-iq.wav file  
\#\#\# GRAPE\_PSWS\_ID has the form \<SITE\_ID\>\_\<INSTRUMENT\_ID\>,  where those values are obtained from a PSWS user account which assigns these values for this site+receiver.  That PSWS site is at https://pswsnetwork.caps.ua.edu/home                                                     
\#\#\# SITE\_ID has the form 'S000nnn' while INSTRUMENT has the form 'NNN'  
GRAPE\_PSWS\_ID\="\<Your Station ID\>\_\<Your Instrument ID\>"  
            
\#\#\# This value is the "token" created for that user account by the PSWS server.  It is a very long string with 0-9 and a-z characters in it  
GRAPE\_PSWS\_TOKEN\="\<TokenFromPSWSsite\>"             

\#\#\# Together GRAPE\_PSWS\_ID \+ GRAPE\_PSWS\_ are the user+password used to authenticate rsync access to  WD1/grape.wsprdaemon.org  
\#\#\# After those variables are defined, the WD user must register this server with the GRAPE server by executing 'wdg p'.  This command needs to be run successfully only once after which automatic uploads to the GRAPE server are enabled

declare RECEIVER\_LIST\=(  
        "KA9Q\_0                     wspr-pcm.local     \<Your Callsign\>         \<Your Grid\>    NULL"  
        "KA9Q\_0\_WWV                   wwv-iq.local     \<Your Callsign\>         \<Your Grid\>    NULL"  
)

declare WSPR\_SCHEDULE\=(  
    "00:00   KA9Q\_0,2200,W2:F2:F5:F15:F30  KA9Q\_0,630,W2:F2:F5  KA9Q\_0,160,W2:F2:F5   KA9Q\_0,80,W2:F2:F5    KA9Q\_0,80eu,W2:F2:F5  KA9Q\_0,60,W2:F2:F5  KA9Q\_0,60eu,W2:F2:F5  KA9Q\_0,40,W2:F2:F5  
             KA9Q\_0,30,W2:F2:F5            KA9Q\_0,22,W2         KA9Q\_0,20,W2:F2:F5    KA9Q\_0,17,W2:F2:F5    KA9Q\_0,15,W2:F2:F5    KA9Q\_0,12,W2:F2:F5  KA9Q\_0,10,W2:F2:F5  
             KA9Q\_0\_WWV,WWV\_2\_5,I1         KA9Q\_0\_WWV,WWV\_5,I1  KA9Q\_0\_WWV,WWV\_10,I1  KA9Q\_0\_WWV,WWV\_15,I1  KA9Q\_0\_WWV,WWV\_20,I1  KA9Q\_0\_WWV,WWV\_25,I1  
             KA9Q\_0\_WWV,CHU\_3,I1           KA9Q\_0\_WWV,CHU\_7,I1  KA9Q\_0\_WWV,CHU\_14,I1"  
)

When finished, press **Escape**, then type :wq\! and press **Enter** to save.

### **Run the Setup Script**

bash  
./wsprdaemon.sh \-V

This will install many packages and may take **several hours**. When it finishes, you should see a message about ka9q-radio adding your user to the radio group — log out and log back in when prompted.

**Troubleshooting:** If you see an error like Update\_ini\_file\_section\_variable /etc/radio ....., run ./wsprdaemon.sh \-V again. If the error persists, reboot and retry:

bash  
sudo reboot now  
cd \~/wsprdaemon  
./wsprdaemon.sh \-V

When the script completes successfully, you should get a prompt indicating the RX-888 MkII is not yet attached to a USB port — that's expected. You'll connect it in the next step.

---

## **Part 6 — Setting Up the GPS-Disciplined Oscillator and RX-888**

### **Hardware Modifications to the RX-888**

Before connecting the RX-888 to anything, two hardware modifications are recommended:

* **External clock:** The RX-888's internal oscillator doesn't meet the 10 MHz accuracy required for PSWS. You'll need to connect it to an external clock source (the Leo Bodnar GPSDO).  
* **Thermal pad:** The RX-888 can run very hot. Adding a large thermal pad to the bottom of the board helps manage heat.

Both items are included in the **RX888 Clock Kit and Thermal Pad**. Follow the instructions in the [RX888 Clock Kit Manual](https://www.rx-sdr.com) for these modifications.

### **Configuring the Leo Bodnar GPSDO**

1. On your personal computer, go to the [Leobodnar website](http://www.leobodnar.com) and locate your specific GPS Disciplined Oscillator model.  
2. Download the configuration software for your operating system from that page.  
3. Open the configuration software and connect the GPSDO to your personal computer via USB. The LED on the GPSDO will light up when connected.  
4. In the **OUT1** box, enter 27000000 and click **Set**. This sets the output to 27 MHz, which is the clock frequency required by the RX-888.  
5. Disconnect the GPSDO from your personal computer.

### **Physical Connections**

Connect everything as follows:

* GPSDO **OUTPUT 1** SMA connector → RX-888 external clock input (yellow cable)  
* GPSDO → Beelink PC via USB (red cable)  
* RX-888 → Beelink PC via USB (green cable)

The color coding above matches the diagram in the original documentation.

---

## **Part 7 — Final wsprdaemon Setup**

### **Run the Setup Script Again**

With the GPSDO and RX-888 now connected, run:

bash  
./wsprdaemon.sh \-V

This time, the script should proceed without errors. When it prompts:

Enter file in which to save the key (/home/wsprdaemon/.ssh/id\_ed25519):

Simply press **Enter** 3–4 times (including when asked for a passphrase — leave it blank).

### **Register Your Station with the PSWS Server**

**Note:** As of this writing, the PSWS website is still under construction and cannot automatically provision new stations. To get your station added, email **wdengelke@retiree.ua.edu** with your SSH public key (just generated above) along with your station details.

### **Enable System Services and Reboot**

bash  
sudo systemctl enable radiod@rx888-wsprdaemon  
sudo systemctl enable ft8-decode.service  
sudo systemctl enable ft4-decode.service  
sudo reboot now

After rebooting, run the setup script one final time:

bash  
cd \~/wsprdaemon  
./wsprdaemon.sh \-V

This time, it should print the version number on the console without errors.

### **Start wsprdaemon**

bash  
wd \-A

This starts wsprdaemon and configures it to launch automatically on boot.

### **Initialize PSWS Recording**

bash  
wdg p

If you encounter errors, consult the [wsprdaemon Operation Guide](https://github.com/rrobinett/wsprdaemon).

### **Verify the Station is Running**

bash  
wds

You should see a status display confirming the receiver is active. Your station should also appear as active on the [PSWS website](https://pswsnetwork.caps.ua.edu/home).

---

*Guide based on the HamSCI PSWS\_Documentation wiki. For the latest updates, see the [GitHub repository](https://github.com/HamSCI/PSWS_Documentation).*


