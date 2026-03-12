# PHIL-MER-HamSCI-PSWS
The PHL-MER (Philadelphia-Mercer County, NJ) PSWS Group's HamSCI RX888WSPRDaemon SDR Personal Space Weather Station.
> **Note:** This will be an 'essential' PSWS build. It will not incorporate WSPR transmitter, VLF or Magnetometer modules
---
## HamSCI RX888 WSPRDaemon SDR Station
This repository documents the build of a **Personal Space Weather Station (PSWS)** node. This is a cooperative project involving a subgroup of Delaware Valley Radio Association (DVRA) members in association with **HamSCI**.
> **Note:** While the participants are DVRA members, this project is independent of and not in association with the DVRA.
### Project Overview

The goal of the PSWS project is to create a geographically distributed, multi-instrument system for ground-based space environment measurements. Data from this node is aggregated into a central HamSCI database for space science research, specifically for analyzing phenomena like **Traveling Ionospheric Disturbances (TIDs)**. Technically, it is a Wide spectrum receiving system that reports data in multiple formats:  WSPR/FST4w and Doppler shift monitoring in the Digital RF _DRF_ format.  This data is useful for studying the behavior of the ionosphere.

WSPRDeamon itelf is a Linux-based service designed to operate as a reliable, autonomous appliance for amateur radio operators and researchers. Its primary function is to decode WSPR and FST4W spots from one or more Software-Defined Radios (SDRs) and reliably upload them to public databases like wsprnet.org. The project emphasizes high reliability, advanced features, and scientific data collection, going far beyond the capabilities of standard tools like WSJT-X. It is the 'engine' behind the Personal Space Weather System and has been developed by Rob Robinette at [WSPRDaemon](https://wsprdaemon.readthedocs.io/en/master/index.html).

This repository documents the PHIL-MER PSWS Group's process of building, configuring, operating and improving it's HamSCI PSWS, located in maidenhead grid FN20lb at the QTH of K3DFD in the Fox Chase section of Philadelphia, Pa.

### Technology Stack and Target Radio Sources
The essential **RX888WSPRDaemon SDR** node is a low-cost, high-precision receiver designed for scientific data collection:

* **SDR:** [RX888 Software Defined Radio](https://www.amazon.com/Receiver-Luminum-Industrial-Beautiful-1kHz%E2%80%9164Mhz/dp/B09FZW89L8) | [Instructions](https://github.com/ik1xpv/ExtIO_sddc)
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
* **Target:** Monitoring [WWV](https://www.nist.gov/pml/time-and-frequency-division/time-distribution/radio-station-wwv) and [CHU](https://nrc.canada.ca/en/certifications-evaluations-standards/canadas-official-time/nrc-shortwave-station-broadcasts-chu) time standard frequency Doppler shift, FT4, FT8 and [WSPR](https://wspr.rocks/) signals.

### Internet Connectivity
* **Data backhaul to HamSCI/WSPRnet**

### Research & Collaboration
Coordinated by the **University of Scranton**, this project supports a global network of "Citizen Science" monitors. Key partners include:

* **TAPR** [Tucson Amateur Packet Radio](https://tapr.org/)
* **NJIT** [Center for Solar-Terrestrial Research](https://research.njit.edu/cstr/)
* **MIT** [Haystack Observatory](https://www.haystack.mit.edu/)
* **Case Western Reserve University** [Case Western Reserve University](https://case.edu/)

---
### Step 1: [Ubuntu OS Installation](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/installation.md)
---
### Step 2: Hardware Build

### Step 3: [WSPRDaemon Configuration](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/configuration.md)
---
### Step 4: Hardware Build
---
### Step 5: Operation
---
### Upgrades, enhancements and Quality-of-Life improvements
---
### Links and Information Sources
