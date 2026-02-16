# PHIL-MER-HamSCI-PSWS
The PHL-MER (Philadelphia-Mercer County, NJ) Group's HamSCI RX888WSPRDaemon SDR Personal Space Weather Station.

> **Note:** This will be an 'essential' PSWS build. It will not incorporate WSPR transmitter, VLF or Magnetometer modules
---

## HamSCI RX888 WSPRDaemon SDR Station

This repository documents the build of a **Personal Space Weather Station (PSWS)** node. This is a cooperative project involving a subgroup of Delaware Valley Radio Association (DVRA) members in association with **HamSCI**.

> **Note:** While the participants are DVRA members, this project is independent of and not in association with the DVRA.

### Project Overview

The goal of the PSWS project is to create a geographically distributed, multi-instrument system for ground-based space environment measurements. Data from this node is aggregated into a central database for space science research, specifically for analyzing phenomena like **Traveling Ionospheric Disturbances (TIDs)**.

This repository documents the PHIL-MER Group's process in the building, configuration, maintenance, operation and ongoing improvement of it's HamSCI PSWS located in maidenhead grid FN20lb.

### Technology Stack and Target Radio Sources

The essential **RX888WSPRDaemon SDR** node is a low-cost, high-precision receiver designed for scientific data collection:

* **SDR:** [RX888 Software Defined Radio](https://www.amazon.com/Receiver-Luminum-Industrial-Beautiful-1kHz%E2%80%9164Mhz/dp/B09FZW89L8)
* **Alternative Source:** [OpenSourceLabs](https://opensourcesdrlab.com/products/rx888-mkii-16bit-sdr-receiver-radio-ltc2208-adc-upgrade-rx888-1)
* **SDR Support:** [TAPR RX-888 Clock kit and thermal pad](https://tapr.org/product/rx888-clock-kit-and-thermal-pad/)
* **Filter-Preamp:** [Turn Island Systems Low pass filter and preamp](https://turnislandsystems.com/product/filter-preamp-v1/)
* **Computing:** HamSCI spec'd off-the-shelf Linux-based system - [Ubuntu 24.04 Server LTE](https://ubuntu.com/download/server).
* **Timing:** [Leo Bodnar GPS-Disciplined Oscillator GPSDO includes GPS patch antenna](https://www.leobodnar.com/shop/index.php?main_page=product_info&cPath=107&products_id=393&zenid=0c06e05cfbe1ec87514a52daab4ec452)
* **Integration:** High-quality SMA connection cables, hardware, low-noise power supply.
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


