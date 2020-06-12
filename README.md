# VELDT-info
VELDT Datasheets &amp; Documentation

## Table of Contents
1. [Pin Mapping](https://github.com/standardsemiconductor/VELDT-info#pin-mapping)
2. [Development Tools](https://github.com/standardsemiconductor/VELDT-info#development-tools)
   1. [Project IceStorm](https://github.com/standardsemiconductor/VELDT-info#project-icestorm)
      1. [Install Project IceStorm from Source on Ubuntu](https://github.com/standardsemiconductor/VELDT-info#install-project-icestorm-from-source-on-ubuntu)
      2. [Update Project IceStorm from Source on Ubuntu](https://github.com/standardsemiconductor/VELDT-info#update-project-icestorm-from-source-on-ubuntu)
      3. [Using Project IceStorm Flow](https://github.com/standardsemiconductor/VELDT-info#using-project-icestorm-flow)
   2. [Clash](https://github.com/standardsemiconductor/VELDT-info#clash)
      1. [Install Clash on Ubuntu](https://github.com/standardsemiconductor/VELDT-info#install-clash-on-ubuntu)
   3. [Mane](https://github.com/standardsemiconductor/VELDT-info#mane)
      1. [Install Mane from Source on Windows](https://github.com/standardsemiconductor/VELDT-info#install-mane-from-source-on-windows)
      
**Clicking on any header within this document will return to Table of Contents.**

## [Pin Mapping](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)
[PDF Version](https://github.com/standardsemiconductor/VELDT-info/blob/master/iCE40UltraUltraPlusSG48PinMigration.pdf)

[XLSX Excel Version](https://github.com/standardsemiconductor/VELDT-info/blob/master/iCE40UP-5k-Pinout.xlsx)
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

## [Development Tools](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)

### [Project IceStorm](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)
Visit the [Project IceStorm Homepage](http://www.clifford.at/icestorm) and the [Github Repository](https://github.com/cliffordwolf/icestorm) for more information. Note all Project Icestorm tools will be installed relative to `/usr/local/`

####  [Install Project IceStorm from Source on Ubuntu](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)
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

#### [Update Project IceStorm from Source on Ubuntu](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)
1. Update [IceStorm Tools](https://github.com/cliffordwolf/icestorm):
```console
foo@bar:~$ cd icestorm
foo@bar:~/icestorm$ git pull
foo@bar:~/icestorm$ make -j$(nproc)
foo@bar:~/icestorm$ sudo make install
```
2. Update [NextPNR](https://github.com/YosysHQ/nextpnr):
```console
foo@bar:~$ cd nextpnr
foo@bar:~/nextpnr$ git pull
foo@bar:~/nextpnr$ cmake -DARCH=ice40 -DCMAKE_INSTALL_PREFIX=/usr/local .
foo@bar:~/nextpnr$ make -j$(nproc)
foo@bar:~/nextpnr$ sudo make install
```
3. Update [Yosys](http://www.clifford.at/yosys):
```console
foo@bar:~$ cd yosys
foo@bar:~/yosys$ git pull
foo@bar:~/yosys$ make -j$(nproc)
foo@bar:~/yosys$ sudo make install
```

The update is complete.

#### [Using Project IceStorm Flow](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)

1. Synthesize Verilog Source Files:
```console
foo@bar:~/test$ ls
Baz.v Top.v
foo@bar:~/test$ yosys -p  "synth_ice40 -top Top -json Top.json -dsp -abc2" Top.v Baz.v
foo@bar:~/test$ ls
Baz.v Top.json Top.v
```
Step 1 assumes the top module is named "Top" and located in `Top.v`. `-json` writes the synthesized design to the specified JSON file. `-dsp` means Yosys will use iCE40 UltraPlus DSP cells for large arithmetic. Finally, the `-abc2` switch causes Yosys to run two passes of `abc` for slightly improved logic density. See the [Yosys Homepage](http://www.clifford.at/yosys/) and [Github Repository](https://github.com/YosysHQ/yosys) for more information. For up-to-date help and reference use `yosys -h` and `yosys -h synth_ice40`.

2. Place and Route Design:
```console
foo@bar:~/test$ nextpnr-ice40 --up5k --package sg48 --pcf Top.pcf --asc Top.asc --json Top.json
foo@bar:~/test$ ls
Baz.v Top.asc Top.json Top.v
```
For more information about NextPNR see the [Github Repository](https://github.com/YosysHQ/nextpnr), [Project IceStorm Homepage](http://www.clifford.at/icestorm) and `nextpnr-ice40 -h`.

3. Pack and Program Bitstream:
```console
foo@bar:~/test$ icepack Top.asc Top.bin
foo@bar:~/test$ ls
Baz.v Top.asc Top.bin Top.json Top.v
foo@bar:~/test$ iceprog Top.bin
```
### [Clash](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)
Visit the [Clash Homepage](https://clash-lang.org), [Github Repository](https://github.com/clash-lang/clash-compiler), and [Hackage Documentation](http://hackage.haskell.org/package/clash-prelude) for more information.

#### [Install Clash on Ubuntu](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)
1. Add [GHC PPA](https://launchpad.net/~hvr/+archive/ubuntu/ghc) and install prerequisites:
```console
foo@bar:~$ sudo add-apt-repository -y ppa:hvr/ghc
foo@bar:~$ sudo apt update
foo@bar:~$ sudo apt install -y cabal-install-xxx ghc-yyy
```
For users managing multiple GHC versions, note the [PPA description](https://launchpad.net/~hvr/+archive/ubuntu/ghc):
> The GHC packages install into `/opt/ghc/$VER/` so in order to use them, one way is to bring a particular GHC version into scope by placing the respective `/opt/ghc/$VER/bin` folder early in the PATH environment variable.
> There's also a `/opt/ghc/bin` (& `/opt/cabal/bin`) folder which contains version-suffixed symlinks to installed GHC versions for convenient use with cabal (e.g. "cabal new-build -w ghc-7.8.4"), as well as symlinks managed by update-alternatives(1) which can be configured via
> ```
> sudo update-alternatives --config opt-ghc
> sudo update-alternatives --config opt-cabal
> ```
> Note that `/opt/ghc/bin` also contains a default symlink for `cabal`, so it's enough to include `/opt/ghc/bin` in your PATH to get access to both `cabal` and `ghc`.

2. Update PATH:
```console
foo@bar:~$ echo "export PATH=\$PATH:/opt/ghc/bin" >> .bashrc
foo@bar:~$ . .bashrc
foo@bar:~$ which ghc && which cabal
/opt/ghc/bin/ghc
/opt/ghc/bin/cabal
foo@bar:~$ ghc --version && cabal --version
The Glorious Glasgow Haskell Compilation System, version yyy
cabal-install version xxx
compiled using version xxx of the Cabal library
```
3. Install Clash:
```console
foo@bar:~$ cabal update
foo@bar:~$ cabal install clash-ghc
foo@bar:~$ echo "export PATH=\$PATH:~/.cabal/bin" >> .bashrc
foo@bar:~$ . .bashrc
```

**Step 3 may fail due to Clash not supporting the latest GHC version.**

If this happens, try removing ghc `sudo apt remove ghc-yyy`, then installing an older GHC version `sudo apt install ghc-zzz`.

4. Verify Clash:
```console
foo@bar:~$ git clone https://github.com/standardsemiconductor/VELDT-blinker-clash.git
foo@bar:~$ cd VELDT-blinker-clash/
foo@bar:~/VELDT-blinker-clash$ cabal build
foo@bar:~/VELDT-blinker-clash$ cabal exec -- clash --verilog Blinker.hs
foo@bar:~/VELDT-blinker-clash$ ls verilog/Blinker/Blinker/
Blinker.manifest Blinker.v
```

### [Mane](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)

[Mane](https://github.com/standardsemiconductor/mane) is the open-source tool for loading bitstreams onto VELDT. It is maintained by Standard Semiconductor to ensure optimized performance with VELDT. Visit the [Github Repository](https://github.com/standardsemiconductor/mane) for more information. Please [open an issue](https://github.com/standardsemiconductor/mane/issues) if you have any problems, questions, or suggestions. 

#### [Install Mane from Source on Windows](https://github.com/standardsemiconductor/VELDT-info#table-of-contents)
**The following steps should be run as Administrator on Powershell.** (Right click, `Run as Administrator`)
1. [Install Chocolatey](https://chocolatey.org/install)
   
   **You may need to shut down and restart powershell prior to using `choco`.**
2. Install [Haskell](https://www.haskell.org/platform/windows.html):
   ```powershell
   C:\Users\foo> choco install haskell-dev
   C:\Users\foo> refreshenv
   C:\Users\foo> cabal update
   ```
3. Install [libusb](https://libusb.info):
   
   **You may need to shut down and restart powershell prior to using `mingw64-pkg`**
   ```powershell
   C:\Users\foo> mingw64-pkg install libusb
   ```
   1. Copy `C:\tools\msys64\mingw64\bin\libusb-1.0.dll` to `C:\Windows\System32\`.
   2. Open `C:\Users\foo\AppData\Roaming\cabal\config` in a text editor. Find the line containing `extra-include-dirs`, add `C:\tools\msys64\mingw64\include\libusb-1.0`.
   3. Find the line containing `extra-lib-dirs`, add `C:\tools\msys64\mingw64\bin`.
   
   **Make sure to delete the `--` and separate elements in the list with a comma.**
   ```
   ...
   extra-include-dirs: C:\tools\msys64\mingw64\include,
                       C:\tools\msys64\mingw64\include\libusb-1.0
   -- deterministic:
   -- cid:
   extra-lib-dirs: C:\tools\msys64\mingw64\bin
   ...
   ```
4. Update Drivers:
   
   Plug in VELDT, then install [Zadig](https://zadig.akeo.ie):
   ```powershell
   C:\Users\foo> choco install zadig
   C:\Users\foo> zadig
   ```
   In Zadig, select `Options` -> `List All Devices`. In the dropdown box select `USB <-> Serial Converter (Interface 0)`. On the `Driver` input, select the Up/Down arrows to choose `WinUSB` then click `Replace Driver` button. Close Zadig when the driver installation completes.
5. Install [Mane](https://github.com/standardsemiconductor/mane):
   
   **You may need to shut down and restart powershell prior to using `git`**
   ```powershell
   C:\Users\foo> choco install git
   C:\Users\foo> git clone https://github.com/standardsemiconductor/mane.git
   C:\Users\foo> cd .\mane\
   C:\Users\foo\mane> cabal install
   ```
6. Verify Mane:
   ```powershell
   C:\Users\foo\mane> mane .\example\Blinker.bin
   ```
