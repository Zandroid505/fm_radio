These installation steps were performed and tested on a Raspberry Pi 5 running Ubuntu Server 24.10.
## HackRF
### Step 1
Install HackRF software:
``` bash
sudo apt install hackrf
```
*This includes HackRF Tools and the low-level library (libhackrf) that enables software on the computer on your computer to operate with HackRF*
### Step 2
Confirm that HackRF can be detected by your computer:
``` bash
hackrf_info
```
You should have output similar to what's shown below:
``` bash
hackrf_info version: 2024.02.1
libhackrf version: 2024.02.1 (0.9)
Found HackRF
Index: 0
Serial number: 0000000000000000088869dc3052b51b
Board ID Number: 2 (HackRF One)
Firmware Version: 2024.02.1 (API:1.08)
Part ID Number: 0xa000cb3c 0x004b4f6c
Hardware Revision: r6
Hardware appears to have been manufactured by Great Scott Gadgets.
Hardware supported by installed firmware:
    HackRF One
```
## Soapy SDR
### Step 1
Install dependencies:
``` bash
sudo apt install cmake g++ libpython3-dev python3-numpy swig
```
### Step 2
Get the source code:
``` bash
git clone https://github.com/pothosware/SoapySDR.git
cd SoapySDR
```
### Step 3
Build & Install:
``` bash
mkdir build
cd build
cmake ..
make -j`nproc`
sudo make install -j`nproc`
sudo ldconfig
```
Test that it was built and installed correctly:
``` bash
SoapySDRUtil --info
```
You should have output similar to what's shown below:
``` bash
######################################################
##     Soapy SDR -- the SDR abstraction library     ##
######################################################

Lib Version: v0.8.1-g6e99da18
API Version: v0.8.200
ABI Version: v0.8-3
Install root: /usr/local
Search path:  /usr/local/lib/SoapySDR/modules0.8-3 (missing)
No modules found!
Available factories... No factories found!
Available converters...
 -  CF32 -> [CF32, CS16, CS8, CU16, CU8]
 -  CS16 -> [CF32, CS16, CS8, CU16, CU8]
 -  CS32 -> [CS32]
 -   CS8 -> [CF32, CS16, CS8, CU16, CU8]
 -  CU16 -> [CF32, CS16, CS8]
 -   CU8 -> [CF32, CS16, CS8]
 -   F32 -> [F32, S16, S8, U16, U8]
 -   S16 -> [F32, S16, S8, U16, U8]
 -   S32 -> [S32]
 -    S8 -> [F32, S16, S8, U16, U8]
 -   U16 -> [F32, S16, S8]
 -    U8 -> [F32, S16, S8]
```
## (Soapy SDR) Plugin for HackRF
### Step 1
Install dependencies:
``` bash 
sudo apt install libhackrf-dev
```
### Step 2
Get the source code (NOTE: Don't clone this in the `SoapSDR/` directory):
``` bash
git clone https://github.com/pothosware/SoapyHackRF.git
```
### Step 3
Build & Install:
``` bash
cd SoapyHackRF
mkdir build
cd build
cmake ..
make
sudo make install
```
### Step 4
Plug in your HackRF One into your computer, and run the following to confirm the installation:
``` bash
SoapySDRUtil --probe="driver=hackrf"
```
You should have output similar to what's shown below:
``` bash
######################################################
##     Soapy SDR -- the SDR abstraction library     ##
######################################################

Probe device driver=hackrf
[INFO] Opening HackRF One #0 88869dc3052b51b...

----------------------------------------------------
-- Device identification
----------------------------------------------------
  driver=HackRF
  hardware=HackRF One
  clock source=internal
  part id=a000cb3c004b4f6c
  serial=0000000000000000088869dc3052b51b
  version=2024.02.1

----------------------------------------------------
-- Peripheral summary
----------------------------------------------------
  Channels: 1 Rx, 1 Tx
  Timestamps: NO
  Other Settings:
     * Antenna Bias - Antenna port power control.
       [key=bias_tx, default=false, type=bool]

----------------------------------------------------
-- RX Channel 0
----------------------------------------------------
  Full-duplex: NO
  Supports AGC: NO
  Stream formats: CS8, CS16, CF32, CF64
  Native format: CS8 [full-scale=128]
  Stream args:
     * Buffer Count - Number of buffers per read.
       [key=buffers, units=buffers, default=15, type=int]
  Antennas: TX/RX
  Full gain range: [0, 116] dB
    LNA gain range: [0, 40, 8] dB
    AMP gain range: [0, 14, 14] dB
    VGA gain range: [0, 62, 2] dB
  Full freq range: [0, 7250] MHz
    RF freq range: [0, 7250] MHz
  Sample rates: 1, 2, 3, 4, 5, ..., 16, 17, 18, 19, 20 MSps
  Filter bandwidths: 1.75, 2.5, 3.5, 5, 5.5, ..., 14, 15, 20, 24, 28 MHz

----------------------------------------------------
-- TX Channel 0
----------------------------------------------------
  Full-duplex: NO
  Supports AGC: NO
  Stream formats: CS8, CS16, CF32, CF64
  Native format: CS8 [full-scale=128]
  Stream args:
     * Buffer Count - Number of buffers per read.
       [key=buffers, units=buffers, default=15, type=int]
  Antennas: TX/RX
  Full gain range: [0, 61] dB
    VGA gain range: [0, 47, 1] dB
    AMP gain range: [0, 14, 14] dB
  Full freq range: [0, 7250] MHz
    RF freq range: [0, 7250] MHz
  Sample rates: 1, 2, 3, 4, 5, ..., 16, 17, 18, 19, 20 MSps
  Filter bandwidths: 1.75, 2.5, 3.5, 5, 5.5, ..., 14, 15, 20, 24, 28 MHz
```
## GNURadio
### Step 1
Install GNURadio:
``` bash
sudo apt install gnuradio
```
## Sources
[HackRF](https://hackrf.readthedocs.io/en/latest/index.html)

[SoapySDR](https://github.com/pothosware/SoapySDR/wiki/BuildGuide)

[(Soapy SDR) Plugin for HackRF](https://github.com/pothosware/SoapyHackRF/wiki)
