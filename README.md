# PHIL-MER-HamSCI-PSWS
The PHL-MER (Philadelphia-Mercer County, NJ) PSWS Group's HamSCI RX888WSPRDaemon SDR Personal Space Weather Station.

---

### Project Overview  
The goal of the PSWS project is to create a geographically distributed, multi-instrument system for ground-based space environment measurements. Data from this node is aggregated into a central HamSCI database for space science research, specifically for analyzing phenomena like **Traveling Ionospheric Disturbances (TIDs)**. Technically, it is a Wide spectrum receiving system that reports data in multiple formats:  WSPR/FST4w and Doppler shift monitoring in the Digital RF _DRF_ format.  This data is useful for studying the behavior of the ionosphere.  

WSPRDeamon (incorporating ka9q-radio) is a Linux-based service designed to operate as a reliable, autonomous appliance for amateur radio operators and researchers. Its primary function is to decode WSPR and FST4W spots from one or more Software-Defined Radios (SDRs) and reliably upload them to public databases like wsprnet.org. The project emphasizes high reliability, advanced features, and scientific data collection, going far beyond the capabilities of standard tools like WSJT-X. It is the 'engine' behind the Personal Space Weather System and has been developed by Rob Robinette at [WSPRDaemon](https://wsprdaemon.readthedocs.io/en/master/index.html).  

This project's research & collaboration is coordinated by the University of Scranton and supports a global network of "Citizen Science" monitors. Key partners include: TAPR [Tucson Amateur Packet Radio](https://tapr.org/) - NJIT [Center for Solar-Terrestrial Research](https://research.njit.edu/cstr/) - MIT - [Haystack Observatory](https://www.haystack.mit.edu/) - Case Western Reserve University [Case Western Reserve University](https://case.edu/) et.al.

### Building our RX888 WSPRDaemon SDR Station for HamSCI
This repository documents the build of a Personal Space Weather Station (PSWS) node. This is a cooperative project involving a subgroup of Delaware Valley Radio Association [(DVRA)](https://www.w2zq.com/) members in association with HamSCI. Note that while the participants are DVRA members, this project is independent of and not in association with the DVRA. This repository documents the PHIL-MER PSWS Group's process of building, configuring, operating and improving it's HamSCI PSWS, located in maidenhead grid FN20lb at the QTH of [K3DFD](https://www.qrz.com/db/K3DFD) in the Fox Chase section of Philadelphia, Pa. Our build will not incorporate WSPRsonde, VLF receiver or Magnetometer.

The official HamSCI WSPRDaemon PSWS build instructions are [here:](https://github.com/HamSCI/PSWS_Documentation/wiki/HF-wsprdaemon-Receiver)

### System Components
<img width="1254" height="712" alt="PSWS drawio" src="https://github.com/user-attachments/assets/d4185718-2765-41ba-ad02-023ebcf7a1e1" />     

| Item | Source | Drivers, Information, Support |
|------|--------|--------|
| RX888 MkII SDR | [OpenSourceLabs](https://opensourcesdrlab.com/products/rx888-mkii-16bit-sdr-receiver-radio-ltc2208-adc-upgrade-rx888-1) | [Instructions](https://github.com/ik1xpv/ExtIO_sddc) [Win10-11 Drivers](https://irp-cdn.multiscreensite.com/46d0be53/files/uploaded/Cypress%20FX3%20Win10.zip) [Linux Drivers](https://github.com/cozycactus/SoapyRX888) |
| GPS Clock | [Leo Bodner LBE-1420](https://www.leobodnar.com/shop/index.php?main_page=product_info&cPath=107&products_id=393&zenid=0c06e05cfbe1ec87514a52daab4ec452)  | * |
| Filter-Preamp | [Turn Island Systems Low pass filter and preamp](https://turnislandsystems.com/product/filter-preamp-v1/) | [12VDC Linear Power Supply](https://www.jameco.com/z/DDU120100Z7972-Jameco-ReliaPro-AC-to-DC-Wall-Adapter-Transformer-12-Volt-1-Amp-12-Watt_100870.html) |
| GPS Clock+Thermal kit | [TAPR RX-888 Clock kit and thermal pad](https://tapr.org/product/rx888-clock-kit-and-thermal-pad/) | [Instructions](https://turnislandsystems.com/wp-content/uploads/2024/05/RX888-Kit-2.pdf) |
| Computer | [Beelink or spec'd PC](https://www.amazon.com/Beelink-SER5-Computer-Graphics-Support/dp/B0D6G965B)  | [Ubuntu 24.04 Server LTE](https://ubuntu.com/download/server) |
| Integration | [High-quality SMA connection cables](https://www.dxengineering.com/parts/cew-316ds001-2), [hardware](https://www.amazon.com/Saddle-Mounts-Tapping-Organizer-Holders/dp/B09B97326Z) | * |
| Case Cooling Fan | [Sunon 40mm](https://www.jameco.com/z/HA40101V4-0000-999-Sunon-12-Volt-40mm-DC-Brushless-Fan_2167630.html) |
| Antenna | Dipole, Longwire or [DX Engineering Active](https://www.dxengineering.com/parts/dxe-rseav-1) |

<ins>Target Radio Sources</ins>  
| [WWV](https://www.nist.gov/pml/time-and-frequency-division/time-distribution/radio-station-wwv) | [CHU](https://nrc.canada.ca/en/certifications-evaluations-standards/canadas-official-time/nrc-shortwave-station-broadcasts-chu) | [WSPR](https://wspr.rocks/)  | [FST4W](https://www.wsprdaemon.org/fst4w) |

<ins>Internet Connectivity</ins>  
Data backhaul to HamSCI/WSPRnet  

<ins>Research & Collaboration</ins>  
Coordinated by the University of Scranton, this project supports a global network of "Citizen Science" monitors. Key partners include:  
TAPR [Tucson Amateur Packet Radio](https://tapr.org/)  
NJIT [Center for Solar-Terrestrial Research](https://research.njit.edu/cstr/)  
MIT [Haystack Observatory](https://www.haystack.mit.edu/)  
Case Western Reserve University [Case Western Reserve University](https://case.edu/)  

## Step-by-Step Instructions  
Step 1: [Ubuntu OS Installation](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/installation.md)  
Step 2: [Hardware Build](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/hardware.md)  
Step 3: [WSPRDaemon Configuration](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/configuration.md)  
Step 4: [Data Integration with HamSCI](https://github.com/K3DFD-Radio/PHL-MER-Group-PSWS/blob/main/data.md)  
Upgrades, enhancements and Quality-of-Life improvements  
Links and Information Sources  
