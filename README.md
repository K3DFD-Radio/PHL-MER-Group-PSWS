# PHIL-MER-HamSCI-PSWS
The PHL-MER (Philadelphia-Mercer County, NJ) PSWS Group's HamSCI RX888WSPRDaemon SDR Personal Space Weather Station.

> **Note:** This will be an 'essential' PSWS build. It will not incorporate WSPR transmitter, VLF or Magnetometer modules
---

## HamSCI RX888 WSPRDaemon SDR Station

This repository documents the build of a **Personal Space Weather Station (PSWS)** node. This is a cooperative project involving a subgroup of Delaware Valley Radio Association (DVRA) members in association with **HamSCI**.

> **Note:** While the participants are DVRA members, this project is independent of and not in association with the DVRA.

### Project Overview

The goal of the PSWS project is to create a geographically distributed, multi-instrument system for ground-based space environment measurements. Data from this node is aggregated into a central HamSCI database for space science research, specifically for analyzing phenomena like **Traveling Ionospheric Disturbances (TIDs)**. Technically, it is a Wide spectrum receiving system that reports data in multiple formats:  WSPR/FST4w and Doppler shift monitoring in the Digital RF DRF format.  This data is useful for studying behavior of the ionosphere.

This repository documents the PHIL-MER PSWS Group's process in the building, configuration, maintenance, operation and ongoing improvement of it's HamSCI PSWS located in maidenhead grid FN20lb.

### Technology Stack and Target Radio Sources

The essential **RX888WSPRDaemon SDR** node is a low-cost, high-precision receiver designed for scientific data collection:

* **SDR:** [RX888 Software Defined Radio](https://www.amazon.com/Receiver-Luminum-Industrial-Beautiful-1kHz%E2%80%9164Mhz/dp/B09FZW89L8)
* **Alternative Source:** [OpenSourceLabs](https://opensourcesdrlab.com/products/rx888-mkii-16bit-sdr-receiver-radio-ltc2208-adc-upgrade-rx888-1)
* **SDR Support:** [TAPR RX-888 Clock kit and thermal pad](https://tapr.org/product/rx888-clock-kit-and-thermal-pad/)
* **Filter-Preamp:** [Turn Island Systems Low pass filter and preamp](https://turnislandsystems.com/product/filter-preamp-v1/)
* **Computer:** [Minimim AMD Ryzen 5 or Intel i5 processor 2 GHz/4 cores, 8 GB memory, 250 GB SSD or AMD Ryzen 7 or Intel i7 2 GHz /8 cores, 32 GB memory. Recommended Beelink PC](https://www.amazon.com/Beelink-SER5-Computer-Graphics-Support/dp/B0D6G965B)
* **Operting System:** HamSCI spec'd off-the-shelf Linux-based system - [Ubuntu 24.04 Server LTE](https://ubuntu.com/download/server).
* **Timing:** [Leo Bodnar GPS-Disciplined Oscillator GPSDO includes GPS patch antenna](https://www.leobodnar.com/shop/index.php?main_page=product_info&cPath=107&products_id=393&zenid=0c06e05cfbe1ec87514a52daab4ec452)
* **Power Supply:** [Low noise linear 5vdc Power Supply for SDR and GPSDO](https://www.amazon.com/SOLUPEAK-External-Adapter-Upgrade-Electronics/dp/B0F4DQ7859?xpid=KC5FPTd_ZmI4F)
* **Antenna:** TBD
* **Integration:** [High-quality SMA connection cables](https://www.dxengineering.com/parts/cew-316ds001-2), [hardware](https://www.amazon.com/Saddle-Mounts-Tapping-Organizer-Holders/dp/B09B97326Z).

### Target Radio Sources
* **Target:** Monitoring WWV frequency Doppler shift and WSPR signals.

### Internet Connectivity

* **Data backhaul to HamSCI/WSPRnet**

### Research & Collaboration

Coordinated by the **University of Scranton**, this project supports a global network of "Citizen Science" monitors. Key partners include:

* **TAPR** (Tucson Amateur Packet Radio)
* **NJIT** Center for Solar-Terrestrial Research
* **MIT** Haystack Observatory
* **Case Western Reserve University**

---
## System Build and Integration

### BIOS Settings
1. Boot the computer and bring you to the BIOS setup screen by using the key specific to your computer
2. In the BIOS setting:
....* Smart Fan Function then press Enter to enter the sub menu. From there, select Smart CPU_Fan Mode using again Enter, and then move the cursor up to Full on Mode and select it
Press Escape to exit the sub menus, until you return to the Advanced tab again
Now, move down to AMD CBS and press Enter into the sub menu, then select FCH Common Options, then move down to Ac Power Loss Options and press Enter. Enter over Ac Loss Control, move the cursor down to Always On and select it
Return to the Advanced Tab. Then, move to the Save & Exit tab, move down to Save Changes and Exit, and select Yes to confirm the changes
You have now configured the computer to automatically turn back on in case of a power outage, and set the internal fans to always run at full speed to prevent overheating


---
## ka9q-radio Configuration

---
## HamSCI Backhaul Data Upload

