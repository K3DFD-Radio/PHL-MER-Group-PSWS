# Installing and Configuring wsprdaemon + GPS Clock

## Table of Contents
1. [Installing wsprdaemon](#1-installing-wsprdaemon)
2. [Configuring wsprdaemon](#2-configuring-wsprdaemon)
3. [Setting up the GPS Disciplined Oscillator](#3-setting-up-the-gps-disciplined-oscillator)
4. [Setting up wsprdaemon to Run on the PSWS Computer](#4-setting-up-wsprdaemon-to-run-on-the-psws-computer)

---

## 1. Installing wsprdaemon

###Install prerequisite tools and utilities. Type `y` to agree to any prompts.

```bash
      sudo apt install btop nmap git tmux vim net-tools iputils-ping avahi-daemon libnss-mdns mdns-scan \
      avahi-utils avahi-discover build-essential make cmake gcc libairspy-dev libairspyhf-dev \
      libavahi-client-dev libbsd-dev libfftw3-dev libhackrf-dev libiniparser-dev libncurses5-dev \
      libopus-dev librtlsdr-dev libusb-1.0-0-dev libusb-dev portaudio19-dev libasound2-dev uuid-dev \
      rsync sox libsox-fmt-all opus-tools flac tcpdump libhdf5-dev libsamplerate-dev
```

### Configure passwordless sudo

Install neovim and edit the sudoers file:

```bash
      sudo apt install neovim
      sudo nvim /etc/sudoers.d/wsprsudo
```

In neovim, press `i` to enter insert mode and type:

```
      wsprdaemon ALL=(ALL) NOPASSWD: ALL
```

Press `Esc`, then type `:wq!` to save and exit.
> `w` = save, `q` = quit, `!` = force (required since the directory is protected)

### Clone the wsprdaemon repository

```bash
      sudo apt install git
      cd ~
      git clone https://github.com/rrobinett/wsprdaemon.git
      cd wsprdaemon
      ./wsprdaemon.sh -V
```

---

## 2. Configuring wsprdaemon

From inside your `~/wsprdaemon` directory, open the configuration file:

```bash
      nano wsprdaemon.conf
```

### Template configuration file

```bash
      #!/bin/bash
      
      ### These first two bash variables *must* be changed from their default values.
      ### To do so, uncomment the following two lines by removing the leading '#' and change the "<....>" fields
      # WSPRNET_REPORTER_ID="<YOUR_REPORTER_ID>
      # REPORTER_GRID="<YOUR_GRID>" #Ex. REPORTER_GRID="FN20vr" (NJIT's GRID Location)
      
      
      WSPRNET_REPORTER_ID="${WSPRNET_REPORTER_ID-<NOT_DEFINED>}"
      REPORTER_GRID="${REPORTER_GRID-<NOT_DEFINED>}"
      ANTENNA_DESCRIPTION="<NOT_DEFINED>"
      
      KA9Q_WEB_TITLE="${WSPRNET_REPORTER_ID}_@${REPORTER_GRID}_${ANTENNA_DESCRIPTION}"
      
      # WD stations contributing to the HamSCI.org Personal Space Weather Project obtain these values from their dashboard at https://pswsnetwork.caps.ua.edu
      # PSWS_STATION_ID="<PSWS_STATION_ID>"
      # PSWS_DEVICE_ID="<PSWS_DEVICE_ID>"
      
      # SIGNAL_LEVEL_UPLOAD="no"
      
      #SIGNAL_LEVEL_UPLOAD_GRAPHS="yes"
      
      declare RECEIVER_LIST=(
              "KA9Q_0         wspr-pcm.local  ${WSPRNET_REPORTER_ID}  ${REPORTER_GRID}  <SDR_PASSWORD_IF_NEEDED>"
              "KA9Q_0_WWV     wwv-iq.local    ${WSPRNET_REPORTER_ID}  ${REPORTER_GRID}  <SDR_PASSWORD_IF_NEEDED>"
      )
      
      declare WSPR_SCHEDULE_only_rx888=(
          "00:00   KA9Q_0,2200,W2:F2:F5:F15:F30  KA9Q_0,630,W2:F2:F5   KA9Q_0,160,W2:F2:F5  KA9Q_0,80,W2:F2:F5
                   KA9Q_0,80eu,W2:F2:F5          KA9Q_0,60,W2:F2:F5    KA9Q_0,60eu,W2:F2:F5 KA9Q_0,40,W2:F2:F5
                   KA9Q_0,30,W2:F2:F5            KA9Q_0,22,W2          KA9Q_0,20,W2:F2:F5   KA9Q_0,17,W2:F2:F5
                   KA9Q_0,15,W2:F2:F5            KA9Q_0,12,W2:F2:F5    KA9Q_0,10,W2:F2:F5   KA9Q_0,6,W2:F2:F5
      
                   KA9Q_0_WWV,WWVB,I1            KA9Q_0_WWV,WWV_2_5,I1 KA9Q_0_WWV,WWV_5,I1  KA9Q_0_WWV,WWV_10,I1
                   KA9Q_0_WWV,WWV_15,I1          KA9Q_0_WWV,WWV_20,I1  KA9Q_0_WWV,WWV_25,I1
                   KA9Q_0_WWV,CHU_3,I1           KA9Q_0_WWV,CHU_7,I1   KA9Q_0_WWV,CHU_14,I1"
      )
      
      declare WSPR_SCHEDULE=( "${WSPR_SCHEDULE_only_rx888[@]}" )
```

### Required edits

| Line | Action |
|------|--------|
| 5 | Uncomment and replace `<YOUR_REPORTER_ID>` with your FCC call sign (or club/university call sign, or a short nickname) |
| 6 | Uncomment and replace `<YOUR_GRID>` with your [grid square](https://www.qrz.com/gridmapper) — looks like `AA11aa` |
| 14 | Optionally update `ANTENNA_DESCRIPTION` (e.g., `80m Dipole`) |
| 19–20 | Uncomment and fill in `PSWS_STATION_ID` and `PSWS_DEVICE_ID` (see below) |
| 27 | Uncomment `SIGNAL_LEVEL_UPLOAD_GRAPHS="yes"` |

### Setting up your PSWS account

1. Create an account at the [PSWS Central Control System](https://pswsnetwork.caps.ua.edu)
2. Go to the **Station** tab and click **Add New Station**
3. Fill out the form *(only Station Nickname and Grid Square are required)*:
   - **Station Nickname:** Include your call sign and organization if applicable
   - **Grid Square:** Same as in the config file
   - **Elevation:** Meters above sea level
   - **Antenna:** Type of antenna installed
   - Add address and contact info, then click **Add Station**
4. From **View My Stations**, note your **Station ID** (e.g., `S000111`)
5. Click **Add New Instrument** and fill out the form *(Instrument and Instrument Type are required)*:

| Field | Description |
|-------|-------------|
| Instrument | Describe your instrument (e.g., `RX-888 MK II - Your PC`) |
| Date Instrument Added | Date you connect the instrument to the PSWS server |
| Date Instrument Removed | Date you shut down the instrument |
| Nickname | Useful if you have multiple identical instruments |
| Serial Number | Instrument serial number |
| Status | `Operational` or `Inactive` |
| Instrument Type | Select `rx888` from the drop-down |

6. Click **Add Instrument** and note your **Instrument ID** (e.g., `111`)

### Example completed configuration

```bash
#!/bin/bash

WSPRNET_REPORTER_ID="XX7XXX"
REPORTER_GRID="AA11aa"

WSPRNET_REPORTER_ID="${WSPRNET_REPORTER_ID-<NOT_DEFINED>}"
REPORTER_GRID="${REPORTER_GRID-<NOT_DEFINED>}"
ANTENNA_DESCRIPTION="<NOT_DEFINED>"

KA9Q_WEB_TITLE="${WSPRNET_REPORTER_ID}_@${REPORTER_GRID}_${ANTENNA_DESCRIPTION}"

PSWS_STATION_ID="S000111"
PSWS_DEVICE_ID="111"

# SIGNAL_LEVEL_UPLOAD="no"

SIGNAL_LEVEL_UPLOAD_GRAPHS="yes"

declare RECEIVER_LIST=(
        "KA9Q_0         wspr-pcm.local  ${WSPRNET_REPORTER_ID}  ${REPORTER_GRID}  <SDR_PASSWORD_IF_NEEDED>"
        "KA9Q_0_WWV     wwv-iq.local    ${WSPRNET_REPORTER_ID}  ${REPORTER_GRID}  <SDR_PASSWORD_IF_NEEDED>"
)

declare WSPR_SCHEDULE_only_rx888=(
    "00:00   KA9Q_0,2200,W2:F2:F5:F15:F30  KA9Q_0,630,W2:F2:F5   KA9Q_0,160,W2:F2:F5  KA9Q_0,80,W2:F2:F5
             KA9Q_0,80eu,W2:F2:F5          KA9Q_0,60,W2:F2:F5    KA9Q_0,60eu,W2:F2:F5 KA9Q_0,40,W2:F2:F5
             KA9Q_0,30,W2:F2:F5            KA9Q_0,22,W2          KA9Q_0,20,W2:F2:F5   KA9Q_0,17,W2:F2:F5
             KA9Q_0,15,W2:F2:F5            KA9Q_0,12,W2:F2:F5    KA9Q_0,10,W2:F2:F5   KA9Q_0,6,W2:F2:F5

             KA9Q_0_WWV,WWVB,I1            KA9Q_0_WWV,WWV_2_5,I1 KA9Q_0_WWV,WWV_5,I1  KA9Q_0_WWV,WWV_10,I1
             KA9Q_0_WWV,WWV_15,I1          KA9Q_0_WWV,WWV_20,I1  KA9Q_0_WWV,WWV_25,I1
             KA9Q_0_WWV,CHU_3,I1           KA9Q_0_WWV,CHU_7,I1   KA9Q_0_WWV,CHU_14,I1"
)

declare WSPR_SCHEDULE=( "${WSPR_SCHEDULE_only_rx888[@]}" )
```

Once editing is complete, press `Esc`, then type `:wq!` to save.

### Run the installer

```bash
./wsprdaemon.sh -V
```

> This will install many packages and could take **several hours** to complete.

When finished, you should see a message like:
> *"ka9q-radio added your user to the radio group, log out and log back in to save changes"*

**If you receive an error** such as `Update_ini_file_section_variable /etc/radio .....`:

Run the below -
```bash
3. ./wsprdaemon.sh -V` again
4. If the error persists, reboot:
```

```bash
sudo reboot now
```

Then re-run:
```bash
cd ~/wsprdaemon
./wsprdaemon.sh -V
```

Once complete, you should get a prompt indicating the **RX-888 MkII is not attached to a USB port** — this is expected at this stage.

---



## 4. Setting up wsprdaemon to Run on the PSWS Computer

### Final installation run

```bash
./wsprdaemon.sh -V
```

When prompted:
```bash
Enter file in which to save the key (/home/wsprdaemon/.ssh/id_ed25519):
```
Press **Enter** 3–4 times, including when asked for a passphrase.

### Register with the PSWS server

> The PSWS website is currently under construction. To be manually added to the server, email **wdengelke@retiree.ua.edu** with:
> Your generated SSH public key
> Your station details

### Enable services and reboot

```bash
sudo systemctl enable radiod@rx888-wsprdaemon
sudo systemctl enable ft8-decode.service
sudo systemctl enable ft4-decode.service
sudo reboot now
```

Then run:

```bash
cd ~/wsprdaemon
./wsprdaemon.sh -V
```

This time, the version number should print to the console.

### Start wsprdaemon

This time, it should print out the version number on the console.
Once that happens  
```bash
wd -A        # Start wsprdaemon and add it as a login startup item
wdg p        # Initialize PSWS recording
```  

If you run into any errors, you can reference the wsprdaemon Operation Guide.  
Then, to confirm that the server is running, run wds into the console. Then, you should get a display like this:
<img width="812" height="1267" alt="image" src="https://github.com/user-attachments/assets/e2f983be-cc8b-4a28-b341-6f569bcc1c7b" />


> If you encounter errors, refer to the [wsprdaemon Operation Guide](https://github.com/rrobinett/wsprdaemon).

### Verify operation

```bash
wds
```

You should see a status display showing all running jobs and daemons and your server should also now show up as active on the [PSWS Website](https://pswsnetwork.caps.ua.edu/home)
