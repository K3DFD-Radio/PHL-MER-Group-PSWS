## WSPRDaemon _aka WD_ Installation and Configuration - _includes ka9q-radio_
1. Login as user _wsprdaemon_
> **Note** This assumes you have set the user _wsprdeamon_ to not require _sudo_ per the installation instructions. If you haven't, [go back](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/installation.md) and complete that step.

2. Clone the _wsprdaemon_ github repository
```
   $cd ~
   $git clone https://github.com/rrobinett/wsprdaemon.git
   $cd wsprdaemon
   $./wsprdaemon.sh -V
```

> **Note:** While the wsprdaemon.git repository is _public_, git can fail to recognize this and will challenge you for a user name and password. This may fail due to password authorization being disallowed at the command line. If this occurs, issue these two commands:\
```
   $git config --global --unset credential.helper\
   $GIT_TERMINAL_PROMPT=0 git clone https://github.com/rrobinett/wsprdaemon.git
```
2. In the wsprdaemon directory open the configuration file in the Nano text editor
```
   $nano wsprdaemon.conf
```
> **Note:** Adjust these configuration items to match your PSWS PC environment. Refer to the [WSPRDaemon documents](https://wsprdaemon.readthedocs.io/en/master/configuration/wsprdaemon.conf.d/wsprdaemon.conf.html)

```
#!/bin/bash
#### The previous line signals to the vim editor that it should use its 'bash' editing mode when editing this file

### These first two bash variables *must* be changed from their default values.
### To do so, uncomment the following two lines by removing the leading '#' and change the "<....>" fields
WSPRNET_REPORTER_ID="<YOUR_REPORTER_ID>" #Ex. WSPRNET_REPORTER_ID="K2MFF" (NJIT's FCC Callsign)
REPORTER_GRID="<YOUR_GRID>" #Ex. REPORTER_GRID="FN20vr" (NJIT's GRID Location)


WSPRNET_REPORTER_ID="${WSPRNET_REPORTER_ID-<NOT_DEFINED>}"           ### The ID of spots uploaded to wsprnet.org by this site
REPORTER_GRID="${REPORTER_GRID-<NOT_DEFINED>}"
ANTENNA_DESCRIPTION="<NOT_DEFINED>"   ### If defined, this is included in the reports to PSKReporter e.g '80m Dipole' and displayed on the KA9Q-web page

KA9Q_WEB_TITLE="${WSPRNET_REPORTER_ID}_@${REPORTER_GRID}_${ANTENNA_DESCRIPTION}"

### WD stations contirbuting to the HamSCI.org Personal Space Weather Project obtain these values from their dashboard at https://pswsnetwork.caps.ua.edu
PSWS_STATION_ID="<PSWS_STATION_ID>" #Ex. PSWS_STATION_ID="S000333"
PSWS_DEVICE_ID="<PSWS_DEVICE_ID>" #Ex. PSWS_DEVICE_ID="352"

### The default is to upload extented spot and background noise level data to wsprdaemon.org.  These are small files, so they add little to the site's Internet bandwidth usage
# SIGNAL_LEVEL_UPLOAD="no"

## If "yes" the site uploads a 150 KByte .png file to wsprnet.org where it can be viewed at http://wsprdaemon.org/graphs/${WSPRNET_REPORTER_ID}/
## Since better, configurable Grafana graphs are available from the wsprdeamon.org, to conserve your site's Internet usage I now discourage the use of this feature
#SIGNAL_LEVEL_UPLOAD_GRAPHS="yes"

declare RECEIVER_LIST=(
        "KA9Q_0                     wspr-pcm.local     ${WSPRNET_REPORTER_ID}        ${REPORTER_GRID}    <SDR_PASSWORD_IF_NEEDED>"
        "KA9Q_0_WWV                   wwv-iq.local     ${WSPRNET_REPORTER_ID}        ${REPORTER_GRID}    <SDR_PASSWORD_IF_NEEDED>"
)

### Here are two examples of WSPR_SCHEDULEs.  Much more complex SDR configurations and schedules are desribed in wd_template_full.conf
declare WSPR_SCHEDULE_only_rx888=(
    "00:00             KA9Q_0,2200,W2:F2:F5:F15:F30  KA9Q_0,630,W2:F2:F5  KA9Q_0,160,W2:F2:F5   KA9Q_0,80,W2:F2:F5  KA9Q_0,80eu,W2:F2:F5  KA9Q_0,60,W2:F2:F5  KA9Q_0,60eu,W2:F2:F5  KA9Q_0,40,W2:F2:F5
                       KA9Q_0,30,W2:F2:F5            KA9Q_0,22,W2         KA9Q_0,20,W2:F2:F5    KA9Q_0,17,W2:F2:F5  KA9Q_0,15,W2:F2:F5    KA9Q_0,12,W2:F2:F5  KA9Q_0,10,W2:F2:F5    KA9Q_0,6,W2:F2:F5

                       KA9Q_0_WWV,WWVB,I1            KA9Q_0_WWV,WWV_2_5,I1  KA9Q_0_WWV,WWV_5,I1  KA9Q_0_WWV,WWV_10,I1   KA9Q_0_WWV,WWV_15,I1  KA9Q_0_WWV,WWV_20,I1  KA9Q_0_WWV,WWV_25,I1
                       KA9Q_0_WWV,CHU_3,I1           KA9Q_0_WWV,CHU_7,I1    KA9Q_0_WWV,CHU_14,I1"
)

### Configure the Kiwi in 8 channel mode and this WSPR_SCHEDULE configuration will use the 6 audio-only Kiwi channels to record spots on the most trafficed WSPR bands
###    while leaving the 2 Kiwi waterfall channels free for listeners

### Default to use the WSPR_SCHEDULE_only_rx888 schedule
declare WSPR_SCHEDULE=( "${WSPR_SCHEDULE_only_rx888[@]}" )

### Source: https://hamsci.jmclynch.org/wsprdaemon-install.html
```
