RIOT on the 6Flo
===================


This is a example workflow for using RIOT-OS with the <i class="icon-cog"></i>**6flo module** .
The 6flo features a Atmel ATSAMR21E ARM Cortex-M0+ CPU (Atmel SAMD21) with integrated 2.4 GHz transceiver.

For more information or to buy a module, see the 6flo tindie store:
[https://www.tindie.com/stores/6Flo/](https://www.tindie.com/stores/6Flo/)


----------
#Toolchain for RIOT



##Getting started
RIOT has a special directory for board related files and for platform related files.
The board files for samr21-xpro is more or less compatible with the 6flo.

To get your board up and running as quickly as possible follow the steps below.



### Install tools
To run RIOT on the 6flo you will need to install a few things.

#### 1. GCC ARM Embedded

You need this to cross compile software for ARM CPU's. There are pre-build binaries for all major OS'es.
[https://launchpad.net/gcc-arm-embedded](https://launchpad.net/gcc-arm-embedded)

Make sure the bin directory (containing the executables) is in your __PATH__.

###### Linux
Alternatively one can do this by downloading and installing:
`sudo apt-get remove binutils-arm-none-eabi gcc-arm-none-eabi &&`
`sudo add-apt-repository ppa:terry.guo/gcc-arm-embedded &&
 sudo apt-get update &&
     sudo apt-get install gcc-arm-none-eabi `
    
#### 2. Make environment

Most developers will already have make installed. But if not you need to install this.

###### OSX
Install the Command Line Tools you can find them here:
[https://developer.apple.com/opensource/](https://developer.apple.com/opensource/)

###### Linux
`sudo apt-get install build-essential`

###### Windows
Install the make package from GNUWin32 you can find it here:
[http://gnuwin32.sourceforge.net/packages/make.htm](http://gnuwin32.sourceforge.net/packages/make.htm)

#### 3. RIOT Packages

The following packages are needed to build the necessary tools and the RIOT application:
`sudo apt-get install git pkg-config autoconf \
	  libudev-dev libusb-1.0-0-dev libtool unzip   valgrind`
    

#### 4. OpenOCD (optional)

OpenOCD can be used for pogramming binaries into your target.
Its open source and available for all major OS'es. As of version 0.8.0 the target SAMR21E18 is supported. The latest source code can be downloaded from:
[http://sourceforge.net/projects/openocd/files/latest/download?source=files](http://sourceforge.net/projects/openocd/files/latest/download?source=files)

Build instuctions are included in the download.

RIOT now adds support for both the samr21"G" and E versions: it's linker file is "samr21x18a.ld".

The `RIOT-master/boards/samr21-xpro` contains a special build target for uploading the application to the target using openocd. For flashing the samr21E it should be changed into this:
 ` set CHIPNAME at91samr21e18`
` set ENDIAN little `
` source [find target/at91samdXX.cfg]`

To use this target openocd must be in your __PATH__.

### Get the code

The easiest way to get sources is to install Git on your machine and clone the repository.
`git clone https://github.com/RIOT-OS/RIOT.git`

Alternatively you can download the sources from GitHub as a ZIP-file.


### Build and Run the demo

Now it's time to build the first example program.

Change to the directory containing the hello-world demo.
`cd RIOT-master/examples/hello-world`

Flash the binary to the board:
`make board=samr21-xpro flash`

To upload the demo you have to have a JTAG debugger connected to the 6flo and upload the source manually or by using Open OCD  (which is default for RIOT-OS).

Open a serial connection in another terminal:
`sudo make board=samr-xpro term`

You should see a *"Hello world"* message.

### Running CoAP on the 6Flo
Change to the directory containing the CoAP server demo.
`cd RIOT-master/examples/microcoap_server`

For building a test Coap Server (the device should be connected to a 6LowPAN Border Router) run:
`make board=samr21-xpro flash`

For quick testing on a native environment (it will save time by not downloading to the board) use: 
`make board=native term`

You can find further instructions for running an example microCoAP server demo here:
[https://github.com/RIOT-OS/RIOT/tree/master/examples/microcoap_server](https://github.com/RIOT-OS/RIOT/tree/master/examples/microcoap_server)








