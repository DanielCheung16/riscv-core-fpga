# FPGA Implementation of a RISC-V 32I Five-Stage Pipelined CPU
 
### Table of Contents

- [FPGA Implementation of a RISC-V 32I Five-Stage Pipelined CPU](#fpga-implementation-of-a-risc-v-32i-five-stage-pipelined-cpu)
    - [Table of Contents](#table-of-contents)
    - [Platform](#platform)
    - [Installation Steps](#installation-steps)
    - [File Directory Description](#file-directory-description)
    - [System Block Diagram](#system-block-diagram)
    - [Instruction Set Architecture](#instruction-set-architecture)
    - [Version Control](#version-control)


### Platform
FPGA: Genesys2  
Vivado: 18.3  
ModelSim: SE-64 10.5

**Note**: The current Vivado and ModelSim co-simulation configuration path is the path on the author's computer. Users need to configure it by themselves.  
Tutorials for Vivado and ModelSim co-simulation:  
[vivado18.3 and modelsim integration - CSDN Blog](https://blog.csdn.net/baidu_25816669/article/details/135588889)  
[ModelSim installation and ModelSim + Vivado co-simulation tutorial - devindd - Blog Garden](https://www.cnblogs.com/devindd/articles/16837346.html)  

### Installation Steps


### File Directory Description
```
.
├── CPU2.srcs
│   ├── constrs_1
│   │   └── new
│   ├── sim_1
│   │   └── new
│   └── sources_1
│       ├── imports
│       │   ├── HDMI
│       │   ├── new
│       │   └── vsrc
│       ├── ip
│       │   ├── bmem_ip
│       │   ├── clk_pll
│       │   ├── clk_pll2
│       │   ├── imem_ip
│       │   ├── ps2_fifo_0
│       │   ├── vga_ctrl_0
│       │   └── vga_gen_0
│       └── new
├── Init
└── waves
```

The three folders to mainly focus on are **CPU2.srcs**, **Init**, and **waves**. `CPU2.srcs` contains the constraint files *constrs_1*, the testbench *sim_1*, and the source code *sources_1*. `Init` contains the bare-metal programs used to initialize imem and dmem, as well as the initialization files for video memory and video memory control. `waves` contains templates for loading waveforms.  

**Note 1**: After modifying the `.coe` files in `Init`, you need to enter the following command in the Vivado command line: `generate_target simulation [get_ips  <your_ip_name>]`, so as to update the netlist of the IP core. This is because Vivado does not regenerate the IP core when the `.coe` file is modified, which causes the old initialization data to still be used during simulation.  
**Note 2**: For how to use `waves`, refer to [USE_WAVE.md](./USE_WAVE.md)


### System Block Diagram
![System Block Diagram](./pictures/Whole_System.png)  
- The CPU code is generated from Chisel into Verilog and is located in `CPU2.srcs/sources_1/imports/vsrc`
- The HDMI module code is located in `CPU2.srcs/sources_1/imports/HDMI`
- The other peripheral code is located in `CPU2.srcs/sources_1/new`  

**Note**: Due to the limitations of the experimental hardware devices, the keyboard here is implemented in the form of buttons (corresponding to `CPU2.srcs/sources_1/new/virtual_ky.sv`). However, the author also built a PS/2 keyboard mode (corresponding to `CPU2.srcs/sources_1/new/ky.sv`). If you want to use a PS/2 keyboard, you need to use git to return to the initial version and add constraints and conversion modules so that Genesys2 supports the corresponding function.

### Instruction Set Architecture
Please read the [Chinese RISC-V Instruction Set Architecture Manual](http://riscvbook.com/chinese/RISC-V-Reader-Chinese-v2p1.pdf).  
For interrupts, please read the [Privileged Instruction section](https://www.scs.stanford.edu/~zyedidia/docs/riscv/riscv-privileged.pdf).

### Version Control
This project uses Git for version management. You can check the currently available versions in the repository.







