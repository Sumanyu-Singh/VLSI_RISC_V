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

* [TASK 3 - COMPILING C CODE AND VIEW RISC-V OBJDMP](#task-3---compiling-c-code-and-view-risc-v-objdmp)

* [TASK 4 - OPTIMIZATION OF C CODE IN GCC AND SPIKE INTRODUCTION](#task-4---optimization-of-c-code-in-gcc-and-spike-introduction)

* [TASK 5 - TESTING THE RV32I CORE](#task-5---testing-the-rv32i-core)

* [TASK 6 - GATE LEVEL SIMULATION (GLS)](#task-6---gate-level-simulation-gls)
  
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
**make sure to install all the required dependencies**

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

The **RISC-V ISA (Instruction Set Architecture)** is a standardized set of instructions that define the behavior of a RISC-V processor. It offers different instruction formats for various types of operations, including arithmetic, logical, control transfer, and memory access. The ISA is designed to be modular, allowing for optional extensions to support specific application domains or customizations. With its open nature, the RISC-V ISA facilitates the development of compatible hardware and software ecosystems, driving innovation and flexibility in computing systems.

**Levels of Representation/Interpretation of RISC-V Instruction**

![levels_of_representation](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/9a7bc193-c7ca-4428-86cc-d83d14d1428e)

The RISC-V instruction format consists of 32-bit instructions divided into several fields:

**1. Opcode (op):** Specifies the operation to be performed.

**2. rd:** Destination register where the result will be stored.

**3. rs1 and rs2:** Source registers containing operand values.

**4. Immediate (imm):** Immediate value for operations involving constants or offsets.

**5. Function code (funct3 and funct7):** Additional operation specifier, used for certain instructions.

![riscv_instruction_formats](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/24ad76cb-aabc-49bc-bb1f-fb0aecf28206)

In RISC-V, there are several types of instructions, each designed to perform specific operations:

**1. R-type:** Register-type instructions operate on data stored in registers. Examples include arithmetic (add, subtract), logical (AND, OR, XOR), and shift instructions.

**2. I-type:** Immediate-type instructions perform operations using an immediate value (constant) and a register operand. These instructions are used for arithmetic, logical, and data transfer operations with immediate values.

**3. S-type:** Store-type instructions store data from a register into memory. They typically use an immediate offset to specify the memory location.

**4. B-type:** Branch-type instructions perform conditional branching based on a comparison result. They compare two registers and branch to a target address if the condition is met.

**5. U-type:** Unconditional-type instructions include instructions for setting register values with an immediate value.

**6. J-type:** Jump-type instructions perform unconditional jumps to a target address.

**7. RV32I/RV64I/RV128I:** These are base integer instruction set extensions of RISC-V, offering different integer register widths (32-bit, 64-bit, 128-bit).

**Below is the sample list of commands alongwith codes for RISC-V Intsructions,**

![instruction_examples](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/969dd4d3-e133-4648-933b-fe363171a9ac)

Additionally, RISC-V supports various optional extensions, such as M (integer multiplication and division), F (single-precision floating-point), D (double-precision floating-point), and many more, each introducing additional instruction types tailored for specific functionalities.

## TASK 3 - COMPILING C CODE AND VIEW RISC-V OBJDMP

I have written a C code for finding factorial of a given number(n). Factorial code in C language is as below (factn.c),

````
#include<stdio.h>  
int main()    
{    
 int i,fact=1,number;    
 printf("Enter a number: ");    
  scanf("%d",&number);    
    for(i=1;i<=number;i++){    
      fact=fact*i;    
  }    
  printf("Factorial of %d is: %d",number,fact);    
return 0;  
}
````
I have used number= 8, to calculate factorial of 8. Compiling C code using RISC-V gcc complier,

````
riscv64-unknown-elf-gcc -o1 -o fact8.o fact8.c
````

![fact8_code_compile](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/7d89060b-e74e-4d09-a959-1c2c4398235a)


After compiling, we can see assembply code generated using RISC-V Objdmp as below,

````
riscv64-unknown-elf-objdump -d fact8.o | less
````

![fact8_objdmp](https://github.com/Sumanyu-Singh/VLSI_RISC_V/assets/100671647/c7592c88-e2a2-444f-ad19-529310802181)

## TASK 4 - OPTIMIZATION OF C CODE IN GCC AND SPIKE INTRODUCTION

Optimization in GCC is essential for improving the performance, efficiency, and/or size of compiled code. By enabling optimization flags like `-O1`, `-O2`, or `-O3`, GCC applies various transformations and analyses to produce faster or smaller executables. Optimization helps maximize resource utilization, minimize execution time, and enhance overall program performance, making it a crucial step in the software development process.

The `-Ofast` optimization flag in GCC enables aggressive optimizations, including disregarding strict IEEE compliance for floating-point operations. It can significantly improve execution speed but may produce results that deviate from standard floating-point behavior. Use with caution when precision is not critical, such as in numerical simulations or performance-critical applications.

For details refer: [Optimize-Options in GCC](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html)
**Assembly Language(ASM) of factorial of a number:**:

````
riscv64-unknown-elf-gcc -o1 -o fact8.o fact8.c
riscv64-unknown-elf-objdump -d fact8.o | less
````

```````
00000000000101a0 <main>:
   101a0:       1101                    addi    sp,sp,-32
   101a2:       ec06                    sd      ra,24(sp)
   101a4:       e822                    sd      s0,16(sp)
   101a6:       1000                    addi    s0,sp,32
   101a8:       4785                    li      a5,1
   101aa:       fef42423                sw      a5,-24(s0)
   101ae:       47a1                    li      a5,8
   101b0:       fef42223                sw      a5,-28(s0)
   101b4:       4785                    li      a5,1
   101b6:       fef42623                sw      a5,-20(s0)
   101ba:       a839                    j       101d8 <main+0x38>
   101bc:       fe842783                lw      a5,-24(s0)
   101c0:       873e                    mv      a4,a5
   101c2:       fec42783                lw      a5,-20(s0)
   101c6:       02f707bb                mulw    a5,a4,a5
   101ca:       fef42423                sw      a5,-24(s0)
   101ce:       fec42783                lw      a5,-20(s0)
   101d2:       2785                    addiw   a5,a5,1
   101d4:       fef42623                sw      a5,-20(s0)
   101d8:       fec42783                lw      a5,-20(s0)
   101dc:       873e                    mv      a4,a5
   101de:       fe442783                lw      a5,-28(s0)
   101e2:       2701                    sext.w  a4,a4
   101e4:       2781                    sext.w  a5,a5
   101e6:       fce7dbe3                bge     a5,a4,101bc <main+0x1c>
   101ea:       fe842703                lw      a4,-24(s0)
   101ee:       fe442783                lw      a5,-28(s0)
   101f2:       863a                    mv      a2,a4
   101f4:       85be                    mv      a1,a5
   101f6:       67e5                    lui     a5,0x19
   101f8:       ec078513                addi    a0,a5,-320 # 18ec0 <__clzdi2+0x3e>
   101fc:       320000ef                jal     1051c <printf>
   10200:       4781                    li      a5,0
   10202:       853e                    mv      a0,a5
   10204:       60e2                    ld      ra,24(sp)
   10206:       6442                    ld      s0,16(sp)
   10208:       6105                    addi    sp,sp,32
   1020a:       8082                    ret

```````

````
riscv64-unknown-elf-gcc -Ofast -o fact8.o fact8.c
riscv64-unknown-elf-objdump -d fact8.o | less
````
````
0000000000010104 <main>:
   10104:       6629                    lui     a2,0xa
   10106:       6565                    lui     a0,0x19
   10108:       1141                    addi    sp,sp,-16
   1010a:       d8060613                addi    a2,a2,-640 # 9d80 <exit-0x6368>
   1010e:       45a1                    li      a1,8
   10110:       e7050513                addi    a0,a0,-400 # 18e70 <__clzdi2+0x3c>
   10114:       e406                    sd      ra,8(sp)
   10116:       3b8000ef                jal     104ce <printf>
   1011a:       60a2                    ld      ra,8(sp)
   1011c:       4501                    li      a0,0
   1011e:       0141                    addi    sp,sp,16
   10120:       8082                    ret

0000000000010122 <register_fini>:
   10122:       00000793                li      a5,0
   10126:       c791                    beqz    a5,10132 <register_fini+0x10>
   10128:       6551                    lui     a0,0x14
   1012a:       6b250513                addi    a0,a0,1714 # 146b2 <__libc_fini_array>
   1012e:       7f60006f                j       10924 <atexit>
   10132:       8082                    ret

0000000000010134 <_start>:
   10134:       0000b197                auipc   gp,0xb
   10138:       e8c18193                addi    gp,gp,-372 # 1afc0 <__global_locale>
   1013c:       23818513                addi    a0,gp,568 # 1b1f8 <__stdio_exit_handler>
   10140:       0000b617                auipc   a2,0xb
   10144:       68060613                addi    a2,a2,1664 # 1b7c0 <__BSS_END__>
   10148:       8e09                    sub     a2,a2,a0
   1014a:       4581                    li      a1,0
   1014c:       65c000ef                jal     107a8 <memset>
   10150:       00000517                auipc   a0,0x0
   10154:       7d450513                addi    a0,a0,2004 # 10924 <atexit>
   10158:       c519                    beqz    a0,10166 <_start+0x32>
   1015a:       00004517                auipc   a0,0x4
   1015e:       55850513                addi    a0,a0,1368 # 146b2 <__libc_fini_array>
   10162:       7c2000ef                jal     10924 <atexit>
   10166:       5d8000ef                jal     1073e <__libc_init_array>
   1016a:       4502                    lw      a0,0(sp)
   1016c:       002c                    addi    a1,sp,8
   1016e:       4601                    li      a2,0
   10170:       f95ff0ef                jal     10104 <main>
   10174:       bf95                    j       100e8 <exit>
````

**INNSTALLING SPIKE**
For details refer: [Spike RISC-V ISA Simulator](https://github.com/riscv-software-src/riscv-isa-sim)
## TASK 5 - TESTING THE RV32I CORE
## TASK 6 - GATE LEVEL SIMULATION (GLS)
