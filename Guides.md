
The official website of Ettus (https://kb.ettus.com/Building_and_Installing_the_USRP_Open-Source_Toolchain_(UHD_and_GNU_Radio)_on_Linux)
provide a relatively guide for the users to install the dependencies of GNU radio. But it still has many bugs you have to be careful to
avoid stucking on some step. 

Update and Install dependencies

On Ubuntu systems, run:
```
   sudo apt-get update
```
On Ubuntu 18.04 systems, run:
```
   sudo apt-get -y install git swig cmake doxygen build-essential libboost-all-dev libtool libusb-1.0-0 libusb-1.0-0-dev libudev-dev libncurses5-dev libfftw3-bin libfftw3-dev libfftw3-doc libcppunit-1.14-0 libcppunit-dev libcppunit-doc ncurses-bin cpufrequtils python-numpy python-numpy-doc python-numpy-dbg python-scipy python-docutils qt4-bin-dbg qt4-default qt4-doc libqt4-dev libqt4-dev-bin python-qt4 python-qt4-dbg python-qt4-dev python-qt4-doc python-qt4-doc libqwt6abi1 libfftw3-bin libfftw3-dev libfftw3-doc ncurses-bin libncurses5 libncurses5-dev libncurses5-dbg libfontconfig1-dev libxrender-dev libpulse-dev swig g++ automake autoconf libtool python-dev libfftw3-dev libcppunit-dev libboost-all-dev libusb-dev libusb-1.0-0-dev fort77 libsdl1.2-dev python-wxgtk3.0 git libqt4-dev python-numpy ccache python-opengl libgsl-dev python-cheetah python-mako python-lxml doxygen qt4-default qt4-dev-tools libusb-1.0-0-dev libqwtplot3d-qt5-dev pyqt4-dev-tools python-qwt5-qt4 cmake git wget libxi-dev gtk2-engines-pixbuf r-base-dev python-tk liborc-0.4-0 liborc-0.4-dev libasound2-dev python-gtk2 libzmq3-dev libzmq5 python-requests python-sphinx libcomedi-dev python-zmq libqwt-dev libqwt6abi1 python-six libgps-dev libgps23 gpsd gpsd-clients python-gps
```

Building and installing GNU Radio from source code
First, make a folder to hold the repository.
```
   cd $HOME
   mkdir workarea-gnuradio
   cd workarea-gnuradio
```   
Next, clone the repository.
```   
   git clone --recursive https://github.com/gnuradio/gnuradio
```   
Next, go into the repository and check out the desired GNU Radio version.
```   
   cd gnuradio
   git checkout v3.7.10.1
   git submodule update --init --recursive
```   
Next, create a build folder within the repository.
```   
   mkdir build
   cd build
```   
Next, invoke CMake to create the Makefiles.
```   
   cmake ../
```   
Next, run Make to build GNU Radio.
```   
   make
```   
Next, you can optionally run some basic tests to verify that the build process completed properly.
```   
   make test
```   
Next, install GNU Radio, using the default install prefix, which will install GNU Radio under the /usr/local/lib folder. 
You need to run this as root due to the permissions on that folder.
```
   sudo make install
```   
Finally, update the system's shared library cache.
```
   sudo ldconfig
```
At this point, GNU Radio should be installed and ready to use. You can quickly test this, with no USRP device attached, by running
the following quick tests.
```  
   gnuradio-config-info --version
   gnuradio-config-info --prefix
   gnuradio-config-info --enabled-component
```   
There is a simple flowgraph that you can run that does not require any USRP hardware. It's called the dialtone test, and it produces a PSTN dial tone on the computer's speakers. Running it verifies that all the libraries can be found, and that the GNU Radio run-time is working.
```
   python $HOME/workarea-gnuradio/gnuradio/gr-audio/examples/python/dial_tone.py
```   
You can try launching the GNU Radio Companion (GRC) tool, a visual tool for building and running GNU Radio flowgraphs.
```
   gnuradio-companion
```
Configuring USB
````   
   cd $HOME/workarea-uhd/uhd/host/utils
   sudo cp uhd-usrp.rules /etc/udev/rules.d/
   sudo udevadm control --reload-rules
   sudo udevadm trigger
````   
   





   
   
