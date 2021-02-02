# Wiki
This wiki holds the knowledgebase for Project Neumann.

## RISC-V Tool Chain Setup

**Objective**

This section describes how to setup the RISC-V gcc compiler toolchain. The Pulp Platform supports a generic ELF/Newlib toolchain build mode.

**Installation of RISC-V Toolchain**

For installing the RISC-V gnu toolchain,the newlib-gnu need to be installed.

Steps to be followed:

**1**.Create a folder named RISCV-TOOLS INSTALLATION.Set up the installation path for the same in the `.bashrc` or `etc/environment` file.

- `RISCV=/home/vlsi/Desktop/RISCV-TOOLS-INSTALLATION`
- `PATH=/home/vlsi/Desktop/RISCV-TOOLS INSTALLATION:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games`
- `cd RISCV-TOOLS INSTALLATION`
- `git clone --recursive https://github.com/riscv/riscv-gnu-toolchain`

**2**.Standard pacakages are needed to be installed,
- `sudo apt-get install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev`

**3**.After cloning and installing the packages one should configure the particular build mode to be used.As the newlib gcc compiler is needed for the Pulp Platform.this is to be configured.
 `./configure --prefix=$RISCV`
RISCV is the path for RISCV-TOOLS INSTALLATION.

**4**.`make` (This is the step of installation of the toolchain)

### RISCV Tools

To run a simple C program using riscv-gnu-toolchain we need some packages to be installed namely,Spike and riscv-pk.

**1.Spike**
Clone this git repository `https://github.com/riscv/riscv-isa-sim`
-  cd riscv-isa-sim
-  sudo apt-get install device-tree-compiler
-  mkdir build
-  cd build
-  ../configure --prefix=$RISCV
-  make
-  make install

**2.riscv-pk**
The RISC-V pk(Proxy Kernel) is a lightweight application execution environment that can host
statically-linked RISC-V ELF binaries.
- git clone `https://github.com/riscv/riscv-pk.git`
- Set the environment variable in `.bashrc` or `etc/environment`.
-  cd riscv-pk 
- mkdir build
- cd build
- ../configure --prefix=$RISCV --host=riscv32-unknown-elf (newlib gcc)
- make
-  make install or use sudo make install

## PULP PLATFORM AND TOOLCHAIN SETUP

PULPino has the following requirements-

- 1.Modelsim 
- 2.Cmake >= version 2.80 
- 3.riscv-toolchain(riscv32-unknown-elf-gcc compiler) 
- 4.verilator

For setting up the pulp platform this has to be followed- 
- sudo apt-get install tcsh
- sudo apt-get install cmake (for cmake scripts)
- sudo apt-get install vim-gtk3 
- Set the `PATH` for the pulp-riscv toolchain to work in the environment file.
- git clone --recursive https://github.com/pulp-platform/pulp-riscv-gnu-toolchain
- Create a folder to store all the binaries of the pulpino cross compiler.(say,pulptoolchain)
- Set up the PATH for the pulp toolchain.
- ./configure --prefix= /home/ vlsi /Desktop/pulptoolchain --with-arch=rv32imc --with-cmodel=medlow --enable-multilib 
- make 
- The binaries are now installed in the folder named pulptoolchain.(riscv32-unknown-elf-gcc)
- Now the pulpino repository can be cloned with- git clone https://github.com/pulp-platform/pulpino


## Creating Cadence Work Area
Check the video https://youtu.be/zQdRLo1zv2M
- After loging in to a a Linux workstation in the Lab, bring up a fresh terminal.
- Type `siproj` and you should see a list of projects.
- Select project number **9** ie. `neumann/rev1`
- If there are no errors, your project area is created and ready to be used.
- Before using Cadence's Virtuoso, you need set environment variables for the tools.
- For that type the command `von` which is alias for the loading the appropriate module file.
- To change your directory to the project work area type `cdproj` and
- start Virtuoso by typing `virtuoso &`
