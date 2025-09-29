# Drone
This document outlines the technologies pre-installed on the drone before the start of the research.

## What is it?
The drone that is used in the research is ModalAI's [Starling 2 Max](https://www.modalai.com/products/starling-2-max) with an extra [Sierra Wireless EM9291 5G](https://www.sierrawireless.com/iot-modules/5g-modules/em9291/) chip from Qualcomm on board.

It came with four batteries, the controller, a powersupply and the case.

## Specifications
### Starling 2 Max
The Starling 2 Max is VOXL 2-powered, NDAA-compliant development drone supercharged by VOXL SDK specifically designed for computer vision-based, long-range dead reckoning with a 500g payload capacity. Powered by Blue UAS Framework autopilot, VOXL 2, the Starling 2 Max weighs 500g and boasts an impressive 55 minutes of autonomous flight time.

**Note:** there are performance issues with GPS on the current iteration of this design, an updated GPS is in development.

 - 500g weight
 - 322mm airframe
 - 180mm propellers
 - 55+ minutes flight time
 - 500g additional payload capacity

#### Powered by VOXL 2:
 - VOXL 2 is powered by Qualcomm QRB5165: 8 cores up to 3.091GHz, 8GB LPDDR5 
 - Abundance of perception capabilities built into Starling 2 Max with dual Sony IMX412 and dual OnSemi AR0144 image sensors
 - Integrated flight controller on DSP with TDK ICM-42688 IMU and ICP-10111 Barometer
 - VOXL ESC Mini 4-in-1

#### Software Features: 
 - Advanced Autonomy
     - Visual Inertial Odometry to navigate in GPS denied environments
     - TFLite Neural Networks run object classification, detection, and other models
     - Open-source software: OpenCV, ROS 2, Docker, PX4 integrated flight controller
     - VOXL SDK
 - Built-in Connectivity Options
     - IP Datalink
         - Wi-Fi
         - Microhard
         - 4G
     - R/C
         - Ghost Atto
         - ELRS (Express LRS) R/C

For more information see the [product page](https://www.modalai.com/products/starling-2-max) on ModalAI's website.


### Sierra Wireless EM9291 5G
**Optimized 5G NR performance for applications requiring Gibabit speed, the EM9291 module is part of the EM Series offering global 5G connectivity.**

Designed in an M.2 form factor, the EM9291 is compatible with our EM9191 module for a simple upgrade path to get the latest standards compliance and bands, as well as the EM7690 module to help facilitate the migration and differentiation between 4G LTE and 5G.

This 5G NR Sub-6 GHz embedded module delivers up to 3.5Gbps downlink speed and 900Mbps uplink speed. With automatic 4G and 3G fallback networks and integrated GNSS receiver (GPS, GLONASS, BeiDou, and Galileo satellite systems supported), the EM9291 is applicable to a wide range of IoT applications such as industrial routers, home gateways, industrial and consumer laptops, rugged tablet PCs, video surveillance and digital signage.

#### 5G NR
 - **Category:** 5G NR Sub-6  
 - **Frequency Bands:** n1, n2, n3, n5, n7, n8, n12, n13, n14, n18, n20, n25, n26, n28, n29, n30, n38, n40, n41, n48, n66, n70, n71, n75, n76, n77, n78, n79 

#### 4G LTE
 - **Category:** Cat-20 
 - **Frequency Bands:** B1, B2, B3, B4, B5, B7, B8, B12, B13, B14, B18, B19, B20, B21, B25, B26, B28, B29, B30, B32, B34, B38, B39, B40, B41, B42, B43, B46, B48, B66, B71

#### Data Speed
 - **Peak Download Rate:** 3.5Gbps
 - **Peak Upload Rate:** 900Mbps 

#### Location Services
 - **Satellite Systems:**  Galileo, Glonass, GPS, Beidou (Bands: L1 and L5) 

#### Embedded Software
 - **Firmware:** Secure boot, Pre-certified firmware 
 - **System Drivers:** Windows® 10, Linux, Android RIL 

#### Interfaces
 - **USB:** USB 3.1 
 - **PCIe:** PCIe generation 3 (or 2), 1 lane

#### Hardware
 - **Dimensions:** 30x52x2.38mm 
 - **Temperature Range:** -30°C / +70°C, -40°C / +85°C 

#### Approvals
 - **Carrier:** AT&T (FirstNet), NTT Docomo, Softbank, T-Mobile, Telstra, Verizon 
 - **Regulatory:** FCC, GCF, IC, KCC, PTCRB, EU RED, JATE/Telec 

#### Embedded Sim
 - Onboard consumer eUICC (optional) 

 For more information see the [product page](https://www.sierrawireless.com/iot-modules/5g-modules/em9291/) on Sierra Wireless's website.

### VOXL 2
VOXL 2 is the next generation Blue UAS Framework integrated AI Companion Computer and Flight Controller powered by Qualcomm Flight™ RB5. VOXL 2 has a robust ecosystem of pre-integrated image sensor modules and modems.

#### VOXL 2 Features

 - 16 grams, 70x36mm SWAP-optimized design
 - Powered by Qualcomm® QRB5165: 8 cores up to 3.091 GHz, 8GB LPDDR5
 - 15 TOPS AI embedded Neural Processing Unit (NPU)
 - Integrated flight controller on DSP with TDK® ICM-42688 IMU and ICP-10111 Barometer
 - 5G, 4G/LTE, WiFi, Microhard add-on connectivity

#### Software Features

 - PX4, ArduPilot, ROS 1/2, Ubuntu 18.04.5 LTS, OpenCV 4.4, MAVROS, MAVSDK
 - Open Source Linux kernel, cross-compilers
 - Docker build environment for CPU, GPU (OpenCL) and DSP (Hexagon SDK) heterogeneous computer vision and deep learning processing


## System Information
```
--------------------------------------------------------------------------------
system-image: 1.8.02-M0054-14.1a-perf
kernel:       #1 SMP PREEMPT Mon Nov 11 22:47:44 UTC 2024 4.19.125
--------------------------------------------------------------------------------
hw platform:  M0054
mach.var:     1.0.1
--------------------------------------------------------------------------------
voxl-suite:   1.4.1
--------------------------------------------------------------------------------
Packages:
Repo:  http://voxl-packages.modalai.com/ ./dists/qrb5165/sdk-1.4/binary-arm64/
Last Updated: 2023-03-02 12:58:41
WARNING: repo file has changed since last update,
	packages may have originated from a different repo
List:
kernel-module-voxl-fsync-mod-4.19.125     1.0-r0
kernel-module-voxl-gpio-mod-4.19.125      1.0-r0
kernel-module-voxl-platform-mod-4.19.125  1.0-r0
libfc-sensor                              1.0.7
libmodal-cv                               0.5.16
libmodal-exposure                         0.1.3
libmodal-journal                          0.2.2
libmodal-json                             0.4.3
libmodal-pipe                             2.10.6
libqrb5165-io                             0.4.9
libvoxl-cci-direct                        0.2.5
libvoxl-cutils                            0.1.1
modalai-slpi                              1.1.19
mv-voxl                                   0.1-r0
qrb5165-bind                              0.1-r0
qrb5165-dfs-server                        0.2.0
qrb5165-imu-server                        1.1.2
qrb5165-rangefinder-server                0.1.4
qrb5165-slpi-test-sig                     01-r0
qrb5165-system-tweaks                     0.3.4
qrb5165-tflite                            2.8.0-2
voxl-bind-spektrum                        0.1.1
voxl-camera-calibration                   0.5.9
voxl-camera-server                        2.1.1
voxl-ceres-solver                         2:1.14.0-10
voxl-configurator                         0.9.7
voxl-cpu-monitor                          0.5.3
voxl-docker-support                       1.3.1
voxl-elrs                                 0.4.1
voxl-esc                                  1.5.1
voxl-feature-tracker                      0.5.2
voxl-flow-server                          0.3.6
voxl-fsync-mod                            1.0-r0
voxl-gphoto2-server                       0.0.10
voxl-gpio-mod                             1.0-r0
voxl-io-server                            0.0.4
voxl-jpeg-turbo                           2.1.3-5
voxl-lepton-server                        1.3.3
voxl-lepton-tracker                       0.0.4
voxl-libgphoto2                           0.0.4
voxl-libuvc                               1.0.7
voxl-logger                               0.4.9
voxl-mavcam-manager                       0.5.7
voxl-mavlink                              0.1.1
voxl-mavlink-server                       1.4.4
voxl-modem                                1.1.5
voxl-mongoose                             7.7.0-1
voxl-mpa-to-ros                           0.3.9
voxl-mpa-tools                            1.3.7
voxl-open-vins                            0.4.16
voxl-open-vins-server                     0.3.0
voxl-opencv                               4.5.5-2
voxl-osd                                  0.1.1
voxl-platform-mod                         1.0-r0
voxl-portal                               0.7.5
voxl-px4                                  1.14.0-2.0.94
voxl-px4-imu-server                       0.1.2
voxl-px4-params                           0.6.3
voxl-qvio-server                          1.1.1
voxl-remote-id                            0.0.9
voxl-reset-slpi                           0.0.1
voxl-state-estimator                      0.0.4
voxl-streamer                             0.7.5
voxl-suite                                1.4.1
voxl-tag-detector                         0.0.4
voxl-tflite-server                        0.3.9
voxl-utils                                1.4.4
voxl-uvc-server                           0.1.7
voxl-vision-hub                           1.8.17
voxl-vtx                                  1.1.8
voxl2-io                                  0.0.3
voxl2-system-image                        1.8.02-r0
voxl2-wlan                                1.0-r0
--------------------------------------------------------------------------------
```