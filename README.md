# 4-Week Research Internship on VLSI and RISC-V using VSDSquadron Mini RISC-V Development Kit
In this project, we will be enhancing our learning about RISC-V open-source ISA and performing basic operations using VSDSquadron Mini RISC-V Board by doing practical application.
RISC-V is gaining traction across industries for its open-source nature, scalability, and efficiency, driving innovation in custom processor designs. It offers a modular and standardized framework, enabling diverse applications from embedded systems to high-performance computing. As industry support and development ecosystem expand, RISC-V continues to emerge as a compelling alternative to proprietary instruction set architectures.

----------
## BOARD TECHNICAL SPECIFICATIONS:

| Board Name : VSDSquadron Mini   SKU : VSDSQM    Microcontroller : CH32V003F4U6 chip with 32-bit RISC-V core based on RV32EC instruction set |
| --------------------------------------------------------------------------------------------------------------------------------------
| USB Connector : USB 2.0 Type-C |                                                                                                                                         
| Built-in LED Pin :                                                           1X onboard user led (PD6) |                                                                    
| Digital I/O pins :                                                           15 |                                                                                         
| Analog I/O pins :                                                           10-bit ADC, PD0-PD7, PA1, PA2, PC4 |                                                         
| PWM pins :                                                                 14X |                                                                                       
| External interrupts :                                                       8 external interrupt edge detectors, but it only maps one external interrupt to 18 I/O ports |
| USART :                                                                     1x, PD6(RX), PD5(TX) |                                                                       
| I2C :                                                                       1x, PC1(SDA), PC2(SCL) |                                                                      
| SPI :                                                                      1x, PC5(SCK), PC1(NSS), PC6(MOSI), PC7(MISO)  |                                               
| Programmer/debugger :                                                       Onboard RISC-V programmer/debugger, USB to TTL serial port support |                          
| I/O voltage        :                                                       3.3 V  |                                                                                      
| Input voltage (nominal) :                                                   5 V |                                                                                         
| Source Current per I/O Pin :                                                8 mA  |                                                                                       
| Sink Current per I/O Pin  :                                                 8 mA   |                                                                                      
| Processor :                                                                24 MHz  |                                                                                     
| SRAM  :                                                                   2kb onchip volatile sram     16kb external program memory |                                  

--------------------------------------------------------------------------                                            
This repo is meant for documenting the tasks aggisned weekly.

<details>
    <summary> TASK 1 - INSTALLING REQUIRED PACKAGES AND TOOLS REQUIRED</summary>
  
1) Install RISC-V GNU Toolchain
  
2) Install Yosys (Synthesis Tool)
  
3) Install iverilog (Verilog Simulator)
 
4) Install gtkwave (Simulation/Timing Waveform Viewer)
   
### 1) INSTALL RISC-V GNU TOOLCHAIN
````
sudo apt install git-all   # To install git and all related packages.
````
![git_all_install](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/34926d5c-3cce-4243-aa8c-5acd40f698de)

````
sudo apt-get install autoconf automake autotools-dev curl python3 python3-pip libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev ninja-build git cmake libglib2.0-dev
````
*make sure to install the dependencies*

![gnu_dependencies](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/bccbbd3c-cc59-4959-a187-0ef0e9abd1c2)

```
git clone https://github.com/riscv/riscv-gnu-toolchain
```
![gnu_toolchain_clone](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/2d917a34-48fe-4c0c-9fb8-5e14e102700c)

## Create a opt dir
```mkdir /opt/riscv```  *try sudo incase of permission denial*
In my case I created a driectory ```mkdir riscv``` and ``` chmod 777 home/nawras/riscv ```
## Config and make inside the risc-v gnu toolchain dir 
```./configure --prefix=/opt/riscv```  
In my case ```./configure --prefix=/home/nawras/riscv```  
Then
```make``` **(Have patience)**
### Troubleshooting
**ERROR 1**: "gcc not found"
try ```sudo apt-get install build-essential```
see if gcc is in /usr/bin/
**ERROR 2**: "no acceptable c compiler found in $PATH"
Open the .bashrc by any editors like vim,emacs,nano,gedit ```nano ~/.bashrc``` 
Add the below line at the end of .bashrc and save it
```export PATH="$PATH:/usr/bin/gcc```
**ERROR 3**: Even after installing gcc g++ sometimes it shows 'gcc' command not found ,though it suggest to ```sudo apt install gcc``` which again will cause the same error. I figured this by ```ls```'ing the /usr/bin directory to find the gcc g++ cc to be in red text with black background indicates broken link or missing file.
Better purge it at **YOUR OWN RISK** and reinstall it again.
```sudo apt-get purge gcc```
or **REINSTALL** ```sudo apt-get install --reinstall gcc``` (didn't work for me)
### INSTALLING IVERILOG GTKWAVE & YOSYS
### YOSYS
```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys 
sudo apt-get install build-essential clang bison flex \libreadline-dev gawk tcl-dev libffi-dev git \ graphviz xdot pkg-config python3 libboost-system-dev\libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make 
sudo make install
```
