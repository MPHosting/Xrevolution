XREVOLUTION

BUILD FOR WINDOWS ON UBUNTU

First, install the general dependencies:

sudo apt-get install build-essential libtool autotools-dev automake pkg-config bsdmainutils curl

A host toolchain (build-essential) is necessary because some dependency packages (such as protobuf) need to build host utilities that are used in the build process.
Building for 64-bit Windows

To build executables for Windows 64-bit, install the following dependencies:

sudo apt-get install g++-mingw-w64-x86-64 mingw-w64-x86-64-dev

Then build using:

cd depends
make HOST=x86_64-w64-mingw32
cd ..
./autogen.sh # not required when building from tarball
CONFIG_SITE=$PWD/depends/x86_64-w64-mingw32/share/config.site ./configure --prefix=/
make

Building for 32-bit Windows

To build executables for Windows 32-bit, install the following dependencies:

sudo apt-get install g++-mingw-w64-i686 mingw-w64-i686-dev 

Then build using:

cd depends
make HOST=i686-w64-mingw32
cd ..
./autogen.sh # not required when building from tarball
CONFIG_SITE=$PWD/depends/i686-w64-mingw32/share/config.site ./configure --prefix=/
make


BUILD UBUNTU

Dependency Build Instructions: Ubuntu & Debian

Build requirements:

sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils

Options when installing required Boost library files:

    On at least Ubuntu 14.04+ and Debian 7+ there are generic names for the individual boost development packages, so the following can be used to only install necessary parts of boost:

     sudo apt-get install libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-program-options-dev libboost-test-dev libboost-thread-dev

    If that doesn't work, you can install all boost development packages with:

     sudo apt-get install libboost-all-dev

BerkeleyDB is required for the wallet.

For Ubuntu only: db4.8 packages are available here. You can add the repository and install using the following commands:

sudo apt-get install software-properties-common
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libdb4.8-dev libdb4.8++-dev

Ubuntu and Debian have their own libdb-dev and libdb++-dev packages, but these will install BerkeleyDB 5.1 or later, which break binary wallet compatibility with the distributed executables which are based on BerkeleyDB 4.8. If you do not care about wallet compatibility, pass --with-incompatible-bdb to configure.

See the section "Disable-wallet mode" to build Xrevolution Core without wallet.

Optional (see --with-miniupnpc and --enable-upnp-default):

sudo apt-get install libminiupnpc-dev

ZMQ dependencies (provides ZMQ API 4.x):

sudo apt-get install libzmq3-dev

Dependencies for the GUI: Ubuntu & Debian

If you want to build Xrevolution-Qt, make sure that the required packages for Qt development are installed. Either Qt 5 or Qt 4 are necessary to build the GUI. If both Qt 4 and Qt 5 are installed, Qt 5 will be used. Pass --with-gui=qt4 to configure to choose Qt4. To build without GUI pass --without-gui.

To build with Qt 5 (recommended) you need the following:

sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler

Alternatively, to build with Qt 4 you need the following:

sudo apt-get install libqt4-dev libprotobuf-dev protobuf-compiler

libqrencode (optional) can be installed with:

sudo apt-get install libqrencode-dev

Once these are installed, they will be found by configure and a xrevolution-qt executable will be built by default.

Download xrevolution source code
----------------------------
```
cd ~
git clone https://github.com/xrevolution-dev/Xrevolution.git
```

Download and compile Berkley DB 4.8
-----------------------------------
```
cd ~
mkdir Xrevolution/db4/

wget 'http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz'
tar -xzvf db-4.8.30.NC.tar.gz
cd db-4.8.30.NC/build_unix/
../dist/configure --enable-cxx --disable-shared --with-pic --prefix=/home/theusername/Xrevolution/db4/
make install
```

Compile Xrevolution with Berkley DB 4.8
-----------------------------------
```
cd ~/Xrevolution/
./autogen.sh
./configure LDFLAGS="-L/home/theusername/Xrevolution/db4/lib/" CPPFLAGS="-I/home/theusername/Xrevolution/db4/include/"
make -s -j5
```

Run Xrevolution Daemon/QT/Client
----------------------------
```
./src/xrevd
./src/xrev-qt
./src/xrev-cli
