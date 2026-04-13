# Hardware Diagram
<img width="1254" height="712" alt="PSWS drawio" src="https://github.com/user-attachments/assets/51a333b6-179d-403c-b5b3-31d64b3e0da9" />  

### Reference and instruction manuals -

RX888 MkII SDR Source: [here](https://dc4ku.com/.cm4all/uproc.php/0/SDR%20-%20TEST-BERICHTE/RX888_english.pdf?cdp=a&_=1806ad658e7)  
Clock kit and thermal Pad: [here](https://turnislandsystems.com/wp-content/uploads/2024/05/RX888-Kit-2.pdf)  
GPS Disciplined Oscillator: [here](https://github.com/simontheu/lbe-1420)  
Filter-preamp: [here](https://turnislandsystems.com/wp-content/uploads/2024/10/Filter-Preamp-v1-rev-6.pdf)
###

## 1. Install the RX888 Clock Kit and Thermal Pad

> **Note:** Before connecting the RX888 MkII SDR, some hardware modifications are required. The internal oscillator does not meet the 10 mHz accuracy requirement, so the Leo Bodnar LBE-1420 external clock must be connected. Additionally, a thermal pad should be added to the bottom of the board to address heat dissipation. Refer to the [RX888 Clock Kit - Thermal Pad Manual](https://turnislandsystems.com/wp-content/uploads/2024/05/RX888-Kit-2.pdf) for modification instructions and see below:

Remove the endplate from the RX888 MkII SDR on the side with the USB socket. As shown below and in the above .pdf instructions, install the Clock and Thermal kit to the SDR. Exercise caution when attaching the coax's u.FL connector to the center of the board. Remove the plastic jumper to disable the internal clock and activate the Bodner GPS DO.  

Also, attach the rubber pad to the underside of the SDR's board and the copper tape to the exposed side of the pad. This side will face and press against the body of the SDR to improve heat transfer.   

<img width="938" height="415" alt="image" src="https://github.com/user-attachments/assets/7294a112-8c9e-4b74-93a5-f1bf47e866ba" />  


### Configure the GPS clock output

1. Visit the [Leobodnar website](http://www.leobodnar.com/shop/) and select your GPS Disciplined Oscillator model
2. Download the configuration software for your operating system
3. Connect the GPS to your personal computer — the LED will light up and the software will respond
4. In the `OUT1` box, enter `27000000` and click **Set**
   > This sets the output to **27 MHz**, which is the required clock frequency for the RX-888
5. Disconnect the GPS from your personal computer

### Component Layout
In this instance the system components are mounted on an 8" X 6.5" aluminum sheet and contained in a [Zultech 9.1" x 7.3" x 3.9" Project Enclosure](https://www.amazon.com/dp/B08Y7GWKGR)
![PXL_20260410_221232372 MP~2](https://github.com/user-attachments/assets/1a9a317c-5d46-4505-9145-090bfe5736d8)

### Set the LBE-1420 GPS DO's clock output for 27.000Mhz

Connect the GPS clock's **OUTPUT 1 SMA connector** to the RX-888, then connect both devices to the PSWS computer via USB.

> 📷 **Receiver Setup Schematic:** The Beelink PC, RX-888 Receiver, and GPS Disciplined Oscillator are connected as follows:
> - 🟡 Yellow — GPS Oscillator to RX-888
> - 🔴 Red — GPS Oscillator to PC
> - 🟢 Green — RX-888 to PC


---
### Next Step: Configure the [WSPRDeamon software](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/configuration.md)

