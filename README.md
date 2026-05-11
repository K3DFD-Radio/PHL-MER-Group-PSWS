## K3DFD HamSCi RX888 WSPRDaemon SDR Personal Space Weather Station  

---
<img width="1707" height="960" alt="image" src="https://github.com/user-attachments/assets/ab836dde-0132-4e4b-95d8-efa7d719f4fc" />

### Project Overview  
The goal of the PSWS project is to create a geographically distributed, multi-instrument system for ground-based space environment measurements. Data from this node is aggregated into a central HamSCI database for space science research, specifically for analyzing phenomena like **Traveling Ionospheric Disturbances (TIDs)**. Technically, it is a Wide spectrum receiving system that reports data in multiple formats:  WSPR/FST4w and Doppler shift monitoring in the Digital RF _DRF_ format.  This data is useful for studying the behavior of the ionosphere.  

[WSPRDeamon](https://wsprdaemon.readthedocs.io/en/master/index.html) by Rob Robinette AI6VN, incorporating Phil Karn's [ka9q-radio](https://ka9q-radio.org) is a Linux-based service designed to operate as a reliable, autonomous appliance for amateur radio operators and researchers. Its primary function is to decode WSPR and FST4W spots from one or more Software-Defined Radios (SDRs) and reliably upload them to public databases like [wsprnet.org](https://wsprnet.org) and [wspr.rocks](https://wspr.rocks). The project emphasizes high reliability, advanced features, and scientific data collection, going beyond the capabilities of applications like WSJT-X.  

This repository documents the build of a Personal Space Weather Station (PSWS) node by located in maidenhead grid FN20lb at the QTH of [K3DFD](https://www.qrz.com/db/K3DFD) in the Fox Chase section of Philadelphia, Pa. This build will not incorporate WSPRsonde, VLF receiver or Magnetometer.   

HamSCI's research & collaboration is coordinated by Dr. Nathaniel Frissell W2NAF at the University of Scranton W3USR and supports a global network of "Citizen Science" monitors. Key partners include: TAPR [Tucson Amateur Packet Radio](https://tapr.org/) - NJIT [Center for Solar-Terrestrial Research](https://research.njit.edu/cstr/) - MIT - [Haystack Observatory](https://www.haystack.mit.edu/) - Case Western Reserve University [Case Western Reserve University](https://case.edu/) et.al.  

### Building the RX888 WSPRDaemon SDR Station
[Hardware Build](https://github.com/K3DFD-Radio/K3DFD-PSWS/blob/main/hardware.md)  
[Official HamSCI System Installation & Configuration](https://github.com/HamSCI/PSWS_Documentation/wiki/HF-wsprdaemon-Receiver)  
[Use of the PSWS & WSPRDaemon](https://github.com/K3DFD-Radio/K3DFD-PSWS/blob/main/operation.md)  
[Links and Information Sources](https://github.com/K3DFD-Radio/K3DFD-PSWS/blob/main/sources_links.md)    

---

### System Block Diagram
<img width="1143" height="796" alt="image" src="https://github.com/user-attachments/assets/f20a7ee4-881c-4ba0-92e2-a33dcc595e65" />  

|  Item  |  Source  | Information  &  Support |
|------|--------|--------|
| RX888 MkII SDR | [OpenSourceLabs](https://opensourcesdrlab.com/products/rx888-mkii-16bit-sdr-receiver-radio-ltc2208-adc-upgrade-rx888-1) | [Instructions](https://github.com/ik1xpv/ExtIO_sddc) [Linux Drivers](https://github.com/cozycactus/SoapyRX888) |
| GPS Clock | [Leo Bodner LBE-1420](https://www.leobodnar.com/shop/index.php?main_page=product_info&cPath=107&products_id=393&zenid=0c06e05cfbe1ec87514a52daab4ec452)  | * |
| Filter-Preamp | [Turn Island Systems Low pass filter and preamp](https://turnislandsystems.com/product/filter-preamp-v1/) | [12VDC Linear Power Supply](https://www.jameco.com/z/DDU120100Z7972-Jameco-ReliaPro-AC-to-DC-Wall-Adapter-Transformer-12-Volt-1-Amp-12-Watt_100870.html) |
| GPS Clock+Thermal kit | [TAPR RX-888 Clock kit and thermal pad](https://tapr.org/product/rx888-clock-kit-and-thermal-pad/) | [Instructions](https://turnislandsystems.com/wp-content/uploads/2024/05/RX888-Kit-2.pdf) |
| Computer | [Beelink](https://www.amazon.com/Beelink-SER5-Computer-Graphics-Support/dp/B0D6G965B)  | [Ubuntu 24.04 Server LTE](https://ubuntu.com/download/server) |
| Integration | [High-quality SMA connection cables](https://www.dxengineering.com/parts/cew-316ds001-2), [hardware](https://www.amazon.com/Saddle-Mounts-Tapping-Organizer-Holders/dp/B09B97326Z) | * |
| Case Cooling Fan | [Noctua NF-A4x10 FLX, Premium Quiet Fan](https://www.amazon.com/Noctua-Cooling-Blades-Bearing-NF-A4x10/dp/B009NQLT0M?pd_rd_w=gbwG0&content-id=amzn1.sym.5b28a964-6fd3-4c72-8c58-6450e7d02f5f&pf_rd_p=5b28a964-6fd3-4c72-8c58-6450e7d02f5f&pf_rd_r=0G5C06AR9745D0GVFQWF&pd_rd_wg=Msobs&pd_rd_r=c0dfe18b-ecbe-4a4c-9c6e-7b25a077237f&pd_rd_i=B009NQLT0M&psc=1&ref_=pd_basp_d_rpt_ba_s_1_t) |
| Antenna | [DX Engineering Short Element Active Antenna DXE-RSEAV-1](https://www.dxengineering.com/parts/dxe-rseav-1) | [12VDC Linear Power Supply](https://www.jameco.com/z/DDU120100Z7972-Jameco-ReliaPro-AC-to-DC-Wall-Adapter-Transformer-12-Volt-1-Amp-12-Watt_100870.html)

<ins>Radio Sources</ins>  
|[WWV](https://www.nist.gov/pml/time-and-frequency-division/time-distribution/radio-station-wwv) | [CHU](https://nrc.canada.ca/en/certifications-evaluations-standards/canadas-official-time/nrc-shortwave-station-broadcasts-chu) | [WSPR](https://wspr.rocks/)  | [FST4W](https://www.wsprdaemon.org/fst4w) |

### Operation & Data Connectivity
[PSWS Operation, Control and Data Analysis](https://github.com/K3DFD-Radio/K3DFD-PSWS/blob/main/operation.md)  
