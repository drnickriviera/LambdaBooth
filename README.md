
<p align="center">
  <img
    alt="Logo"
    src="https://github.com/leobel96/LambdaBooth/blob/master/images/logo.svg"
    width="500"
  />
</p>


LambdaBooth is an hardware and software photobooth that can make your parties even more funny.


## How it works
This photobooth works in this way: 
1. A person push a button 
2. 5 seconds timer starts
3. After the 5 seconds a photo is taken using a supported DSLR camera connected to the Raspberry
4. The background of the photo is changed with a random background taken from a list provided by the user using chromakey technique
5. The original and modified photos are saved in two folders chosen by the user.

## Bill Of Materials
To make the Lambdabooth you need:
- A DSLR camera, please refer to [this list](http://www.gphoto.org/proj/libgphoto2/support.php) to make sure your camera is supported. I've tested it with a Canon EOS 1100D
- A Raspberry Pi
- A cable to connect your camera to USB (please refer to your camera's manual)
- A micro USB Power Supply for Raspberry Pi
- A big momentary push button to take the photo such as [this one](https://it.aliexpress.com/store/product/16mm-BIG-head-Plastic-Emergency-Stop-switch-1NO1NC-LA16-11ZS-A/2030101_32755091219.html?spm=a2g0y.12010108.1000016.1.34c85ab5uKJrBb&isOrigTitle=true)
- A momentary button to switch off Raspberry Pi
- A 7 segment display for the countdown such as [this one](https://www.aliexpress.com/item/Free-Shipping-1pcs-Common-Anode-1-Bit-Digital-Tube-7-segment-2-3-inch-Red-LED/32282721171.html?spm=a2g0s.8937460.0.0.6cae2e0ef7D98c)
- A well lit green screen such as [this one](https://www.amazon.com/LimoStudio-AGG1338-Studio-Backdrop-Included/dp/B00KQ23GGW/ref=sr_1_8?s=photo&ie=UTF8&qid=1532250306&sr=1-8&keywords=green+screen&dpID=41yE%252BXGppLL&preST=_SY300_QL70_&dpSrc=srch)
- Material for the LambdaBooth's box. You can use wood, plastic,...
- Electric cables for connections

## Dependencies
1. Python 3 and pip3: If you have a recent version of Raspbian installed on your Raspberry Pi, they should already be installed
2. Gphoto2: It is necessary to control a DSLR camera using the Raspberry Pi. Installing it is as simple as: `sudo apt-get install gphoto2 libgphoto2*`
3. Opencv3: It is necessary for chromakeying. The installation is pretty long (it could require 4 hours on a first gen Raspberry Pi). To install it I have followed [this guide](https://www.life2coding.com/install-opencv-3-4-0-python-3-raspberry-pi-3/) from step 1 to step 11. There is also a [bash script](https://github.com/pageauc/opencv3-setup) that can simplify all the process and automate it but I've not tested it.

## Installation
1. Clone all the repository in your Raspberry Pi
2. Edit parameters in "LambdaBooth.py" according to your needs
3. Create a folder for original photos, a folder for backgrounds and a folder for edited photos paying attention to edit their paths in LambdaBooth.py
4. Make/seek backgrounds with the same dimensions of the original photo. The code tells you what is the right width and height
5. Add the possibility to shutdown the Raspberry Pi with the button following [this guide](https://github.com/raspberrypi/firmware/blob/master/boot/overlays/README#L619)
6. Make "LambdaBooth.py" autostart at boot adding it to crontab following [this guide](https://www.raspberrypi.org/forums/viewtopic.php?t=139774#p927101)
7. Connect the buttons according to your configuration and camera
8. Wire the display as shown [here]()

## Result example
I've taken a pretty hard green screen photo from google images to test the Chromakey feature. The result is pretty good:

![Original Image](/images/front.jpg)
![Background](/images/background.jpg)
![Result Image](/images/front_mod.jpg)

Probably, editing parameters in chromakey function, you can achieve better results. Also edit them if you use a blue screen instead of a green one.

## Troubleshooting
- After dependencies installation, I noticed errors when trying to import opencv module in Python. This is caused by other dependencies missing. In my case they were libatlas, libqt4 and libqt4-test. I've installed them in this way: `sudo apt-get install libatlas-base-dev libqt4 libqt4-test`. If you notice other errors caused by dependencies missing, please use Google to find a way to install them.
- Running gphoto2, I kept having error 'Could not claim the USB device'. This was caused by two processes which keep camera busy. To fix it I've followed [this guide](https://askubuntu.com/questions/993876/gphoto2-could-not-claim-the-usb-device). The problem was that, after reboot, the services keep autorun and I had to kill them after every boot. To kill them forever I used `sudo chmod -x /usr/lib/gvfs/gvfs-gphoto2-volume-monitor` and `sudo chmod -x /usr/lib/gvfs/gvfsd-gphoto2`.
- For every problem related to opencv, gphoto2 or the other libraries used, please refer to their support page. In particular: [gphoto2](https://github.com/gphoto/gphoto2) and [opencv](https://github.com/skvark/opencv-python).

## TODO
- Video Demonstration
- LambdaBooth.py file
- Display wiring
