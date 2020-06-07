# VELDT-info
VELDT Datasheets &amp; Documentation

## Table of Contents
1. [Pin Mapping](https://github.com/standardsemiconductor/VELDT-info#pin-mapping)
2. [Development Tools](https://github.com/standardsemiconductor/VELDT-info#development-tools)
   1. [Project IceStorm](https://github.com/standardsemiconductor/VELDT-info#project-icestorm)

## Pin Mapping
[PDF](https://github.com/standardsemiconductor/VELDT-info/blob/master/iCE40UltraUltraPlusSG48PinMigration.pdf)
[XLSX](https://github.com/standardsemiconductor/VELDT-info/blob/master/iCE40UP-5k-Pinout.xlsx)
FNC|Pin Type|Bank|Differential Pair|ICE40UP-5K-SG48
---|--------|----|-----------------|---------------
IOB_0a|DPIO|2|TRUE_of_IOB_1b|46
IOB_2a|DPIO|2|TRUE_of_IOB_3b|47
IOB_3b_G6|DPIO/GBIN|2|COMP_of_IOB_2a|44
IOB_4a|DPIO|2|TRUE_of_IOB_5b|48
IOB_5b|DPIO|2|COMP_OF_IOB_4a|45
IOB_6a|DPIO|2|TRUE_of_IOB_7b|2
IOB_8a|PIO|2|TRUE_of_IOB_9b|4
IOB_9b|PIO|2|COMP_of_IOB_8a|3
creset_b|CONFIG|1||8
IOB_13b|PIO|1||6
CDONE|CONFIG|1||7
IOB_16a|PIO|1||9
IOB_18a|PIO|1||10
IOB_20a|PIO|1||11
IOB_22a|PIO|1|TRUE_of_IOB_23b|12
IOB_23b|PIO|1|COMP_of_IOB_22a|21
IOB_24a|PIO|1||13
IOB_25b_G3|PIO/GBIN|1||20
IOB_29b|PIO|1||19
IOB_31b|DPIO|1|COMP_of_IOB_30a|18
IOB_32a_SPI_WO|PIO/CONFIG_SPI|1||14
IOB_33b_SPI_WI|PIO/CONFIG_SPI|1||17
IOB_34a_SPI_WCK|PIO/CONFIG_SPI|1||15
IOB_35b_SPI_WS|PIO/CONFIG_SPI|1||16
IOT_36b|PIO|0|COMP_of_IOT_37a|25
IOT_37a|PIO|0|TRUE_of_IOT_36b|23
IOT_38b|PIO|0|COMP_of_IOT_39a|27
IOT_39a|PIO|0|TRUE_of_IOT_38b|26
IOT_41a|PIO|0||28
IOT_42b|PIO|0|COMP_of_IOT_43a|31
IOT_43a|PIO|0|TRUE_of_IOT_42b|32
IOT_44b|PIO|0|COMP_of_IOT_45a|34
IOT_45a_G1|PIO/GBIN|0|TRUE_of_IOT_44b|37
IOT_46b_G0|PIO/GBIN|0||35
IOT_48b|PIO|0|COMP_of_IOT_49a|36
IOT_49a|PIO|0|TRUE_of_IOT_48b|43
IOT_50b|PIO|0|COMP_of_IOT_51a|38
IOT_51a|PIO|0|TRUE_of_IOT_50b|42
RGB2|LED|0||41
RGB1|LED|0||40
RGB0|LED|0||39
VCC|VCC|VCC||5
VCC|VCC|VCC||30
VCCIO_0|VCCIO|0||33
VCCIO_2|VCCIO|2||1
SPI_VCCIO_1|VCCIO|1||22
VCCPLL|VCCPLL|VCCPLL||29
VPP_2V5|VPP|VPP||24

## Development Tools

### Project IceStorm
Visit the [Project IceStorm Homepage](http://www.clifford.at/icestorm) and the [Github Repository](https://github.com/cliffordwolf/icestorm) for more information. Note all Project Icestorm tools will be installed relative to `/usr/local/`

####  Install Project IceStorm from Source on Ubuntu
1. Install Prerequisites:
```console
foo@bar:~$ sudo apt install build-essential clang bison flex libreadline-dev gawk tcl-dev libffi-dev git graphviz xdot pkg-config python python3 libftdi-dev qt5-default python3-dev libboost-all-dev cmake libeigen3-dev
```
2. Install [IceStorm Tools](https://github.com/cliffordwolf/icestorm) (icepack, icebox, iceprog, icetime, chip databases, etc.):
```console
foo@bar:~$ git clone https://github.com/cliffordwolf/icestorm.git icestorm
foo@bar:~$ cd icestorm
foo@bar:~/icestorm$ make -j$(nproc)
foo@bar:~/icestorm$ sudo make install
```
3. Install [NextPNR](https://github.com/YosysHQ/nextpnr) (place-and-route tool):
```console
foo@bar:~$ git clone https://github.com/YosysHQ/nextpnr nextpnr
foo@bar:~$ cd nextpnr
foo@bar:~/nextpnr$ cmake -DARCH=ice40 -DCMAKE_INSTALL_PREFIX=/usr/local .
foo@bar:~/nextpnr$ make -j$(nproc)
foo@bar:~/nextpnr$ sudo make install
```
4. Install [Yosys](http://www.clifford.at/yosys) (Verilog synthesis):
```console
foo@bar:~$ git clone https://github.com/cliffordwolf/yosys.git yosys
foo@bar:~$ cd yosys
foo@bar:~/yosys$ make -j$(nproc)
foo@bar:~/yosys$ sudo make install
```
5. Update [udev](https://wiki.debian.org/udev) rules:

Create a file `/etc/udev/rules.d/53-lattice-ftdi.rules` with the following line:
```
ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6010", MODE="0660", GROUP="plugdev", TAG+="uaccess"
```
This will allow uploading bitstreams as unprivileged user.

The installation is complete.

#### Update Project IceStorm from Source on Ubuntu
1. Update [IceStorm Tools](https://github.com/cliffordwolf/icestorm)
```console
foo@bar:~$ cd icestorm
foo@bar:~/icestorm$ git pull
foo@bar:~/icestorm$ make -j$(nproc)
foo@bar:~/icestorm$ sudo make install
```
2. Update [NextPNR](https://github.com/YosysHQ/nextpnr)
```console
foo@bar:~$ cd nextpnr
foo@bar:~/nextpnr$ git pull
foo@bar:~/nextpnr$ cmake -DARCH=ice40 -DCMAKE_INSTALL_PREFIX=/usr/local .
foo@bar:~/nextpnr$ make -j$(nproc)
foo@bar:~/nextpnr$ sudo make install
```
3. Update [Yosys](http://www.clifford.at/yosys)
```console
foo@bar:~$ cd yosys
foo@bar:~/yosys$ git pull
foo@bar:~/yosys$ make -j$(nproc)
foo@bar:~/yosys$ sudo make install
```

The update is complete.