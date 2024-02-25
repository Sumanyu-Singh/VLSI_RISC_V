# 4-Week Research Internship on VLSI and RISC-V using VSDSquadron Mini RISC-V Development Kit
In this project, we will be enhancing our learning about RISC-V open-source ISA and performing basic operations using VSDSquadron Mini RISC-V Board by doing practical application.
RISC-V is gaining traction across industries for its open-source nature, scalability, and efficiency, driving innovation in custom processor designs. It offers a modular and standardized framework, enabling diverse applications from embedded systems to high-performance computing. As industry support and development ecosystem expand, RISC-V continues to emerge as a compelling alternative to proprietary instruction set architectures.

----------
![board_in_hand](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/c9c3cb2c-9139-4c94-98ac-e9fa82e8aa48)

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
This repository is meant for documenting the tasks aggisned weekly.

* [TASK 1 - INSTALLING REQUIRED PACKAGES AND TOOLS REQUIRED](#task-1---installing-required-packages-and-tools-required)

* [TASK 2 - RISC-V ISA INSTRUCTION TYPES AND FORMAT](#task-2---risc-v-isa-instruction-types-and-format)
  
## TASK 1 - INSTALLING REQUIRED PACKAGES AND TOOLS REQUIRED
  
* Install RISC-V GNU Toolchain RISC-V based compiler)
  
* Install Yosys (Synthesis Tool)
  
* Install iverilog (Verilog Simulator)
 
* Install gtkwave (Simulation/Timing Waveform Viewer)
--------------------------------------------------------------------------------------------------------------------------------
* ### INSTALL RISC-V GNU TOOLCHAIN

````
sudo apt install git-all   # To install git and all related packages.
````
![git_all_install](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/34926d5c-3cce-4243-aa8c-5acd40f698de)

````
sudo apt-get install autoconf automake autotools-dev curl python3 python3-pip libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev ninja-build git cmake libglib2.0-dev
````
*make sure to install all the required dependencies*

![gnu_dependencies](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/bccbbd3c-cc59-4959-a187-0ef0e9abd1c2)

```
git clone https://github.com/riscv/riscv-gnu-toolchain --recursive
```
![gnu_toolchain_clone](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/2d917a34-48fe-4c0c-9fb8-5e14e102700c)

#### Creating opt dir

````
mkdir /opt/riscv
````
*try sudo incase of permission denial. In my case I have created a driectory named as below and then gave full permission of this directory


````
mkdir riscv   # in home directory
chmod -R 777 /home/sumanyu/riscv
````
#### Configure and make inside the risc-v-gnu-toolchain directory

````
./configure --prefix=/opt/riscv
```` 
But, I created different directory so I used below command
````
./configure --prefix=/home/sumanyu/riscv
 make
````
![config_make](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/4566c905-21e1-45eb-b49d-dbe6e88a89d2)

* ##### NOTE: It takes more time, so wait till it is finished
Also, do run below commands for installing build-essentials and avoiding error in gcc installation
````
sudo apt-get install build-essential
````
Add gcc path in $PATH variable or add in .bashrc file(in home directory), add at last line

````
gvim .bashrc
export PATH= "$PATH:/usr/bin/gcc"
````
* ### INSTALL YOSYS

````
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make
sudo apt-get install build-essential clang bison flex \libreadline-dev gawk tcl-dev libffi-dev git \ graphviz xdot pkg-config python3 libboost-system-dev\libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make 
sudo make install
````

![git_clone_yosys](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/6dab4fbf-b006-42cd-9c63-90cfc0f70e28)

![install_make_build_essen](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/9a0c4ab1-3163-430a-99c3-484be31298c0)

![make](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/3a222797-0639-4850-b55b-2005386bd82a)

![make_complete](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/5be5a6dc-2781-4655-9b43-749502cac4bd)

* ### INSTALL IVERILOG

```
sudo apt-get install iverilog
```
![iverilog](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/7190f933-241a-4d54-9f6d-0924f4549c82)

* ### INSTALL GTKWAVE
````
sudo apt-get install gtkwave
````
![gtkwave](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/04594765-eca1-4863-a55b-d66398ba4696)


## TASK 2 - RISC-V ISA INSTRUCTION TYPES AND FORMAT

[The RISC-V Instruction Set Manual](https://riscv.org/wp-content/uploads/2017/05/riscv-spec-v2.2.pdf)

The RISC-V ISA (Instruction Set Architecture) is a standardized set of instructions that define the behavior of a RISC-V processor. It offers different instruction formats for various types of operations, including arithmetic, logical, control transfer, and memory access. The ISA is designed to be modular, allowing for optional extensions to support specific application domains or customizations. With its open nature, the RISC-V ISA facilitates the development of compatible hardware and software ecosystems, driving innovation and flexibility in computing systems.





