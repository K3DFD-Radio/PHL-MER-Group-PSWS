## Hardware Mods, DXE Active Antenna, BeeLink PC Linux Server Install and WSPRDdaemon Configuration

The actual construction style and design of the RX888 WSPRDaemon SDR PSWS is up to the builder although certain tasks are requied regardless of how the build is performed. The use of the below cabinet, layout and hardware is not required but represents the quality that was put into the K3DFD PSWS build. How you do it is of course, up to you. Regardless, the system must meet the operational performance levels to provide useful data to HamSCI.

Essentially, the entire PSWS consists of: BeeLink SER Pro 7i 16-32GB 8-core NUC PC with Linux 24.04.x server and WSPRDaemon installed, a RX888 MkII 16-bit ADC Software-defined Radio that provides 30Mhz of spectrum coverage, a Leo Bodnar LBE-1420 GPS-disciplined Oscillator that drives the RX888 clock for GPS sourced timing, a Turn Island Systems (Dual) 30Mhz Filter-preamp to provide antialiasing filtering of signals above 30Mhz, and a low-noise DX Engineering RSEAV1 active vertical antenna.  

The components are mounted on an aluminum plate held in place by 3D printed hold downs, M3 hardware, 3M self-adhesive tie-down pads contained in a Zulkit aluminum cabinet. All internal connections consists of high-quality SMA connectors, coax and USB cables. 12VDC is provided to the PSWS components and the active antenna by 1.2 amp linear power supplies. Do not use inexpensive switching supplies. All DC lines are choked to reduce or eliminate any potention RF.

## Reference and instruction manuals -  
[RX888 MkII SDR Source](https://dc4ku.com/.cm4all/uproc.php/0/SDR%20-%20TEST-BERICHTE/RX888_english.pdf?cdp=a&_=1806ad658e7)  
[TAPR Clock kit and thermal Pad](https://turnislandsystems.com/wp-content/uploads/2024/05/RX888-Kit-2.pdf)    
[Leo Bodnae LBE-1420 GPS Disciplined Oscillator](https://github.com/simontheu/lbe-1420)  
[TIS 30Mhz Filter-preamp](https://turnislandsystems.com/wp-content/uploads/2024/10/Filter-Preamp-v1-rev-6.pdf)  
[DX Engineering DXE-RSEAV1 Active Antenna](https://static.dxengineering.com/global/images/instructions/dxe-rseav-1fvi.pdf?_gl=1*aiifno*_gcl_au*MjY1MDA5NDMzLjE3NzcxMjkxODI.*_ga*ODc1MzkyNjAxLjE3NzcxMjkxODI.*_ga_NZB590FMHY*czE3Nzg1MjAwMzUkbzYkZzEkdDE3Nzg1MjAwNTgkajM3JGwwJGgw)

### Component Layout  
In this instance the system components are mounted on a [6"x8"x1/16" 6061/T651 Aluminum Sheet Metal aluminum plate](https://www.amazon.com/PATIKIL-Aluminum-Protective-Rectangle-Lndustry/dp/B0DHR7TLNX?pd_rd_w=YnrUL&content-id=amzn1.sym.6bb79025-718b-4ad1-b8ec-68027fb35564&pf_rd_p=6bb79025-718b-4ad1-b8ec-68027fb35564&pf_rd_r=T4XHH2GPPG2ZPEGDFS6F&pd_rd_wg=xPK13&pd_rd_r=6daeec44-af98-4005-ae55-ffafdbc088e7&pd_rd_i=B0DHR7TLNX&ref_=pd_bap_d_grid_rp_hxwhrp_sspa_dk_bia_0_18_t&th=1) and contained in a [Zultech 9.1"x7.3"x3.9" Project Enclosure](https://www.amazon.com/dp/B08Y7GWKGR) using metric M3 hardware  
<img width="1143" height="796" alt="image" src="https://github.com/user-attachments/assets/4a2492c1-d869-4780-b1e3-4608127e056e" />  

### Drill Baseplate Mounting Holes
Use a 4mm drill bit to open holes in the aluminum base plateplate and use M3 screws and nuts to place and affix the 3D hold downs. 
<img width="1143" height="796" alt="image" src="https://github.com/user-attachments/assets/cc9186c5-f339-4bc0-ba5c-c18ac4f96f91" />  

### 3D printed Component Hold Downs
You can use these .stl file to print the component hold down parts that affix the RX888, GPSDO and Filter-Preamp to the aluminum plate. ABS recommended although .20mm layer / 20% infill PLA works well  
[.stl file for RX888 MkII SDR](https://drive.google.com/file/d/11iTI1NAHCLrqhb-Ud5RXdYGEvIffmVQV/view?usp=sharing)  
[.stl file for Leo Bodnar LBE-1420](https://drive.google.com/file/d/18yck0PaMf3_px7qnixWy3uBU1HxInkka/view?usp=sharing)  
[.stl file for Turn Island Systems 30Mhz Filter-Preamp](https://drive.google.com/file/d/1gPSx4msNTrLTgFopmkgazG57UBLr8tAZ/view?usp=sharing)  
<img width="1143" height="767" alt="image" src="https://github.com/user-attachments/assets/6318063e-6c47-48c7-a323-7d009c39c269" />  

## Perform Required RX888 clock-Thermal Kit Installation, DXE-RSEAV1 Antenna Bias-T Disable and LBE-1420 Clock Freq Configuration

### Open up the RX888 MkII SDR and install the TAPR Clock and Thermal Pad kit  

Before connecting the RX888 MkII SDR, some hardware modifications are required. The internal oscillator does not meet the 10 mHz accuracy requirement, so the Leo Bodnar LBE-1420 external clock must be connected and configured for 27MHz. Additionally, a thermal pad should be added to the bottom of the board to address heat dissipation. Refer to the [RX888 Clock Kit - Thermal Pad Manual](https://turnislandsystems.com/wp-content/uploads/2024/05/RX888-Kit-2.pdf) for modification instructions and see below:  

Remove the endplate from the RX888 MkII SDR on the side with the USB socket. As shown below and in the above instructions, install the Clock and Thermal kit to the SDR. Exercise caution when attaching the coax's u.FL connector to the center of the board. Remove the plastic jumper to disable the internal clock and activate the Bodner GPS DO.  

Also, attach the rubber pad to the underside of the SDR's board and the copper tape to the exposed side of the pad. This side will face and press against the body of the SDR to improve heat transfer.   

<img width="1143" height="585" alt="image" src="https://github.com/user-attachments/assets/c923a7ea-6167-4dcb-9652-7dc2c4a7bda2" />

---
## Assemble and Configure the DX Engineering DXE-RSEAV-1 Short Vertical Active Antenna
The first task is to change the internal J2 and J3 jumper settings to disable the Bias-T power source feature. Move both J2 and J3 jumpers from the 1-2 position to the 2-3 position. Then the required 12VDC will be supplied to the type-F connector on the front of the antenna box.
<img width="1143" height="796" alt="image" src="https://github.com/user-attachments/assets/1a676475-a87c-4fe0-bac0-027ff0272290" />

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

This completes the required component modifications
  
Install Linux Server and WSPRDaemon on the BeeLink SER Pro NUC PC  
<img width="1143" height="796" alt="image" src="https://github.com/user-attachments/assets/2f2aa991-23fe-4a95-b3bd-38fa137843d9" />

## Next Step  
### [Follow the HamSCI instructions to configure the Beelink PC with Linux 24.04.n and WSPRDaemon](https://github.com/HamSCI/PSWS_Documentation/wiki/HF-wsprdaemon-Receiver)  

## Return Here  


