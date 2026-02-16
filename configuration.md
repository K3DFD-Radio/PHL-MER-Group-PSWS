## WSPRDaemon _aka WD_ Installation and Configuration - _includes ka9q-radio_
1. Login as user _wsprdaemon_\
> **Note** This assumes you have set the user _wsprdeamon_ to not require _sudo_ per the installation instructions. If you haven't, go back and complete that step.

1. Run the following commands to create the local wsprdaemon instance:
   - $cd ~
   - $git clone https://github.com/rrobinett/wsprdaemon.git
   - $cd wsprdaemon
   - $./wsprdaemon.sh -V
> **Note:** While the wsprdaemon.git repository is _public_, git can fail to recognize this and will challenge you for a user name and password. This may fail due to password authorization being disallowed at the command line. If this occurs, issue these two commands:\
         $git config --global --unset credential.helper\
         $GIT_TERMINAL_PROMPT=0 git clone https://github.com/rrobinett/wsprdaemon.git

2. In the wsprdaemon directory open the configuration file in the Nano text editor
   - $nano wsprdaemon.conf
> **Note:** Adjust these configuration items to match your PSWS PC environment. Refer to the [WSPRDaemon documents](https://wsprdaemon.readthedocs.io/en/master/configuration/wsprdaemon.conf.d/wsprdaemon.conf.html)

!/bin/bash\
_\# The previous line signals to the editor that it should use its 'bash' editing mode when editing this file_

_\# RAC setup enables WD supporters to access your machine remotely.  Get a RAC # from Rob Robinett. WD will run without this_
RADIOD_CPU_CORES="0-7"
WD_CPU_CORES="2-15"

_/# ka9q-radio/web parameters_
KA9Q_RADIO_COMMIT="main"
KA9Q_CONF_NAME="rx888-wsprdaemon"
KA9Q_WEB_COMMIT_CHECK="main"
KA9Q_WEB_TITLE="<Your Callsign>"

_/# To avoid overflowing the file system, the oldest wav files are deleted first when storage reaches 75%_
ARCHIVE_WAV_FILES="yes"

_\# WD always attempts to upload spots to wsprnet.org_
SIGNAL_LEVEL_UPLOAD="yes"
SIGNAL_LEVEL_UPLOAD_MODE="noise"  

_\# The name put in upload log records, the title bar of the graph, and the name used to view spots and noise at that server_
SIGNAL_LEVEL_UPLOAD_ID="<Your Callsign>"    

_\# If this variable is defined as "yes" AND SIGNAL_LEVEL_UPLOAD_ID is defined, then FTP graphs of the last 24 hours to http://wsprdaemon.org/graphs/_
SIGNAL_LEVEL_UPLOAD_GRAPHS="yes"   

_\# If this variable is defined as "yes" AND SIGNAL_LEVEL_UPLOAD_ID is defined, then make graphs visible at http://localhost/_
SIGNAL_LEVEL_LOCAL_GRAPHS="yes"    

_\# These two variables need to be defined in order to enable this WD GRAPE service. These values are obtained from the PSWS user account at https://pswsnetwork.caps.ua.edu/home. Together GRAPE_PSWS_ID + GRAPE_PSWS_TOKEN are the user+password used to authenticate rsync access to  WD1/grape.wsprdaemon.org_
                                                 
_\# SITE_ID has the form 'S000nnn' while INSTRUMENT has the form 'NNN'_
GRAPE_PSWS_ID="<Your Station ID>_<Your Instrument ID>"
          
_\# This value is the "token" created for that user account by the PSWS server.  It is a very long string with 0-9 and a-z characters in it_
GRAPE_PSWS_TOKEN="<TokenFromPSWSsite>"             

_\# After those variables are defined, the WD user must register this server with the GRAPE server by executing 'wdg p'.  This command needs to be run successfully only once after which automatic uploads to the GRAPE server are enabled

declare RECEIVER_LIST=/(
        "KA9Q_0                     wspr-pcm.local     <Your Callsign>         <Your Grid>    NULL"
        "KA9Q_0_WWV                   wwv-iq.local     <Your Callsign>         <Your Grid>    NULL"
)

declare WSPR_SCHEDULE=/(
    "00:00   KA9Q_0,2200,W2:F2:F5:F15:F30  KA9Q_0,630,W2:F2:F5  KA9Q_0,160,W2:F2:F5   KA9Q_0,80,W2:F2:F5    KA9Q_0,80eu,W2:F2:F5  KA9Q_0,60,W2:F2:F5  KA9Q_0,60eu,W2:F2:F5  KA9Q_0,40,W2:F2:F5
             KA9Q_0,30,W2:F2:F5            KA9Q_0,22,W2         KA9Q_0,20,W2:F2:F5    KA9Q_0,17,W2:F2:F5    KA9Q_0,15,W2:F2:F5    KA9Q_0,12,W2:F2:F5  KA9Q_0,10,W2:F2:F5
             KA9Q_0_WWV,WWV_2_5,I1         KA9Q_0_WWV,WWV_5,I1  KA9Q_0_WWV,WWV_10,I1  KA9Q_0_WWV,WWV_15,I1  KA9Q_0_WWV,WWV_20,I1  KA9Q_0_WWV,WWV_25,I1
             KA9Q_0_WWV,CHU_3,I1           KA9Q_0_WWV,CHU_7,I1  KA9Q_0_WWV,CHU_14,I1"
)
