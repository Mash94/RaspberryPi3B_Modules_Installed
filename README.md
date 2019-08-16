# Raspberry Pi 3B - Raspbian Buster
I'm newbie on Raspberry and fork this repo for save all modules that I have used on Raspberry and they work.

## VNC via Ethernet
### Connecting your Raspberry Pi to your Laptop Display
Server on Raspberry
Cliente on PC

Connect Raspberry to PC via Ethernet
Find the IP address of your Raspberry Pi, vias SSH. 
```
ifconfig
```
```
169.254.7.221
```
Go to the Network and Sharing Center on your laptop.
Set IP on Ethernet adaptor for example.
```
169.254.7.221
```

## 3.5” RPi Display(MPI3501):
Driver install:
```
sudo rm -rf LCD-show
git clone https://github.com/goodtft/LCD-show.git
chmod -R 755 LCD-show
cd LCD-show/
```
Change Image HDMI to 3.5"
```
cd LCD-show/
sudo ./LCD35-show
```

Change Image LCD to HDMI
```
cd LCD-show/
sudo ./LCD-hdmi
```
If the driver is already installed, execute the following command
```
cd LCD-show/
sudo ./rotate.sh 90
```


## WIFI
Install if necessary through
```
sudo apt-get install wpasupplicant
```
After that, open wpa_supplicant file:
```
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```
```
network={
    ssid="HomeOneSSID"
    psk="passwordOne"
    priority=1
    id_str="homeOne"
}

network={
    ssid="HomeTwoSSID"
    psk="passwordTwo"
    priority=2
    id_str="homeTwo"
}
```
By last update wifi networks setting
```
sudo wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/wpa_supplicant.conf -D wext
sudo dhclient wlan0
```


## Matplot 
```
sudo apt-get install python-matplotlib
```

## Faster OpenCV
Leverage all your CPUs power in OpenCV by using **TBB**, **Neon** and **VFPV3** libraries.

Since I've already compiled this on my own Raspberry Pi I made it available on GitHub.

Save countless of compile time by just installing these debs. Enjoy!

### What is this?
* A pre-compiled **OpenCV 4.1.0** for **Raspberry Pi** optimized for deep learning / computer vision applications (**NEON**, **VFPV3**, **TBB** turned on).
* Bindings for **Python 2** and **Python 3** are also included.
* For detailed build informations click [here](build_information.txt).
* Created with OpenCV cpack targets.
* Tested on **Raspberry Pi 3** using **Raspbian Buster (Debian 10)** (for Raspbian Stretch click [here](https://github.com/dlime/Faster_OpenCV_4_Raspberry_Pi/releases/tag/stretch_410)).

### How much faster?
Performance tests have been made in this [great blog article](https://www.pyimagesearch.com/2017/10/09/optimizing-opencv-on-the-raspberry-pi/) which led to an approximate **30%** increase in speed and of over **48%** when applied strictly to DNN module.

Another performance test is available [here](https://www.theimpossiblecode.com/blog/faster-opencv-smiles-tbb/) which also led to about **30%** increase in speed.

### How to use it?
Install OpenCV library prerequisites on your Raspberry Pi.
```
sudo apt-get update && sudo apt-get upgrade -y
    sudo apt-get update --fix-missing
sudo apt-get install -y libjpeg-dev libpng-dev libtiff-dev libgtk-3-dev
sudo apt-get install -y libavcodec-extra libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install -y	libxvidcore-dev libx264-dev libjasper1 libjasper-dev
sudo apt-get install -y	libatlas-base-dev gfortran libeigen3-dev libtbb-dev
```

Install **numpy** based on your target Python version:
```
sudo apt-get install -y python3-dev python3-numpy
```
or:
```
sudo apt-get install -y python-dev python-numpy
```

#### How to install?
Clone the repo into your Raspberry Pi and install all debs:
```
git clone https://github.com/Mash94/RaspberryPi3B_Modules_Installed.git
cd RaspberryPi3B_Modules_Installed/debs
sudo dpkg -i OpenCV*.deb
sudo ldconfig
```

#### How to test?

##### C++
Test the installation by going to tests cpp test folder, build it and launch the executable:
```
cd RaspberryPi3B_Modules_Installed/tests/cpp_opencv_test
mkdir build && cd build
cmake ..
make -j`cat /proc/cpuinfo | grep -c 'processor'`
./cpp_opencv_test
```

##### Python
Test the installation by going to tests folder and launch the test.py file:
```
cd RaspberryPi3B_Modules_Installed/tests/python_opencv_test
python test.py
```

You shouldn't see any error messages in console and an image with tetris blocks with contours drawed should appear.

#### How to uninstall?
Run the following command in your Raspberry Pi terminal:
```
sudo apt purge opencv-*
```
