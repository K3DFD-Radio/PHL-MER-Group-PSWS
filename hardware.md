## Hardware Mods, Configuration, BeeLing PC Linux Install & System Build  

## Reference and instruction manuals -  
RX888 MkII SDR Source: [here](https://dc4ku.com/.cm4all/uproc.php/0/SDR%20-%20TEST-BERICHTE/RX888_english.pdf?cdp=a&_=1806ad658e7)  
Clock kit and thermal Pad: [here](https://turnislandsystems.com/wp-content/uploads/2024/05/RX888-Kit-2.pdf)    
GPS Disciplined Oscillator: [here](https://github.com/simontheu/lbe-1420)  
Filter-preamp: [here](https://turnislandsystems.com/wp-content/uploads/2024/10/Filter-Preamp-v1-rev-6.pdf)  

### Component Layout  
In this instance the system components are mounted on a [6"x8"x1/16" 6061/T651 Aluminum Sheet Metal aluminum plate](https://www.amazon.com/PATIKIL-Aluminum-Protective-Rectangle-Lndustry/dp/B0DHR7TLNX?pd_rd_w=YnrUL&content-id=amzn1.sym.6bb79025-718b-4ad1-b8ec-68027fb35564&pf_rd_p=6bb79025-718b-4ad1-b8ec-68027fb35564&pf_rd_r=T4XHH2GPPG2ZPEGDFS6F&pd_rd_wg=xPK13&pd_rd_r=6daeec44-af98-4005-ae55-ffafdbc088e7&pd_rd_i=B0DHR7TLNX&ref_=pd_bap_d_grid_rp_hxwhrp_sspa_dk_bia_0_18_t&th=1) and contained in a [Zultech 9.1"x7.3"x3.9" Project Enclosure](https://www.amazon.com/dp/B08Y7GWKGR) using metric M3 hardware  
<img width="1143" height="796" alt="image" src="https://github.com/user-attachments/assets/4a2492c1-d869-4780-b1e3-4608127e056e" />  

### Drill Baseplate Mounting Holes
Use a 4mm drill bit to open holes in the aluminum base plateplate and use M3 screws and nuts to place and affix the 3D hold downs. 
<img width="1143" height="796" alt="image" src="https://github.com/user-attachments/assets/cc9186c5-f339-4bc0-ba5c-c18ac4f96f91" />  


### 3D print Component Hold Downs
You can use these .stl file to print the component hold down parts that affix the RX888, GPSDO and Filter-Preamp to the aluminum plate.
<img width="1143" height="767" alt="image" src="https://github.com/user-attachments/assets/6318063e-6c47-48c7-a323-7d009c39c269" />


## Required RX888 SDR mods and Leo Bodnar GPSDO configuration tasks before completing the PSWS build.  

### Open up the RX888 MkII SDR and install the TAPR Clock and Thermal Pad kit  

Before connecting the RX888 MkII SDR, some hardware modifications are required. The internal oscillator does not meet the 10 mHz accuracy requirement, so the Leo Bodnar LBE-1420 external clock must be connected and configured for 27MHz. Additionally, a thermal pad should be added to the bottom of the board to address heat dissipation. Refer to the [RX888 Clock Kit - Thermal Pad Manual](https://turnislandsystems.com/wp-content/uploads/2024/05/RX888-Kit-2.pdf) for modification instructions and see below:  

Remove the endplate from the RX888 MkII SDR on the side with the USB socket. As shown below and in the above instructions, install the Clock and Thermal kit to the SDR. Exercise caution when attaching the coax's u.FL connector to the center of the board. Remove the plastic jumper to disable the internal clock and activate the Bodner GPS DO.  

Also, attach the rubber pad to the underside of the SDR's board and the copper tape to the exposed side of the pad. This side will face and press against the body of the SDR to improve heat transfer.   

<img width="1143" height="585" alt="image" src="https://github.com/user-attachments/assets/c923a7ea-6167-4dcb-9652-7dc2c4a7bda2" />

### Configure the Leo Bodnard LBE-1420 GPS clock output

1. Visit the [Leo Bodnar website](http://www.leobodnar.com/shop/) and select your GPS Disciplined Oscillator model and download the configuration software for your operating system. Note: Use a different PC  than the PSWS Beelink to run the Bodnar configuration software.
3. Connect the GPS to your PC — the LED will light up and the software will respond
4. In the `OUT1` box, enter `27000000` and click **Set** > This sets the output to **27 MHz**, which is the required clock frequency for the RX-888
5. Disconnect the GPS from your PC


Connect the GPS clock's **OUTPUT 1 SMA connector** to the RX-888, then connect both devices to the PSWS computer via USB.

> 📷 **Receiver Setup Schematic:** The Beelink PC, RX-888 Receiver, and GPS Disciplined Oscillator are connected as follows:
> - 🟡 Yellow — GPS Oscillator to RX-888
> - 🔴 Red — GPS Oscillator to PC
> - 🟢 Green — RX-888 to PC

---
### [Follow the HamSCI instructions to configure the Beelink PC with Linux 24.04.n and WSPRDaemon](https://github.com/HamSCI/PSWS_Documentation/wiki/HF-wsprdaemon-Receiver)  



