RISC-V GNU Toolchain with the Klessydra Instruction Extensions
===================================================

This README provides instructions on how to install and build the RISC-V GNU-compiler Toolchain with the Klessydra instruction extensions. This extension enables the execution of vector operations in SIMD/MIMD fashion inside the [Klessydra Vector Coprocessing Unit (VCU)](https://github.com/klessydra/pulpino-klessydra). For more information on how to use these instructions, please refer to the [Klessydra Technical Manual](https://github.com/klessydra/pulpino-klessydra/blob/master/doc/Klessydra/Klessydra%20Technical%20Manual%20v11.1%20May%202020.pdf).

## Prerequisites
Several standard packages are needed to build the toolchain. On Ubuntu, you can install them executing the following commands:

    sudo apt install python2.7
    sudo apt install python-pip
    pip2 install pyyaml
    cd $(dirname $(which python2.7))
    sudo ln -s python2.7 python
    sudo apt-get install git cmake tcsh autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev

##  Installation
To install the RISC-V toolchain with Klessydra instruction extension, please follow the steps below:
   1. Clone this repository to your local machine:     
   
     git clone https://github.com/klessydra/riscv-gnu-toolchain
     
   2. Run the configure script replacing **"/path/to/install"** with the path where you want to install the toolchain: 
   
     ./configure --prefix=/path/to/install --with-arch=rv32ima --with-abi=ilp32  
     
   3. Build the toolchain:
     
     make
     
   4. Copy the riscv-gnu-toolchain/**make_link.sh** script into the **bin** directory of the installed toolchain:

     cp make_links.sh </path/to/install>/bin  
       
   5. Make the script executable:  
   
     chmod +x /path/to/install/bin/make_links.sh
     
   6. Run the script to create symbolic links:  

    ./path/to/install/bin/make_links.sh
         
## Usage
   To use the RISC-V toolchain with Klessydra instruction extension, simply add the **bin** installation directory to your PATH environment variable. For example, if you installed the toolchain to **/opt/riscv-klessydra**, add the following line to your **.bashrc** file in your home directory:
   
    export PATH=$PATH:/opt/riscv-klessydra/bin  
    
Now if you want to test for example the riscv gcc compiler in the toolchain, you can execute the following command "klessydra-unknown-elf-gcc -c file.c -o file.o"
