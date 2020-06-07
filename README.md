# VELDT-info
VELDT Datasheets &amp; Documentation

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