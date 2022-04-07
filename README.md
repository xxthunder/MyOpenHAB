# MyOpenHAB

## Parts list

* Raspberry Pi 4 B, 4x 1,5 GHz, 4 GB RAM, WLAN, BT
* Raspberry 4596 Pi - official power supply for Raspberry Pi 4 Model B, USB-C, 5.1V, 3A
* RPI CASE ALU08 (got it from [here](https://www.reichelt.de/de/de/gehaeuse-fuer-raspberry-pi-4-alu-schwarz-rpi-case-alu08-p272360.html?r=1))
* JSAUX USB 3.0 SATA Adapter (got it from [here](https://www.amazon.de/dp/B086W944YT/ref=cm_sw_r_awdo_navT_g_J4W8QZW49ZTRPVYGJE9D), found it on this [list](https://forum-raspberrypi.de/forum/thread/47876-magische-usb-sata-adapter-und-wo-sie-zu-finden-sind/))
* Some SATA SSD disk (e.g. 128 GBytes)
* TODO: Some pictures here, please.

## Initial Commissioning

* TODO: add all the sd card cloning stuff here.
* Install docker:
```bash
curl -sSL https://get.docker.com | sh
sudo docker run hello-world
```
* You should get a message about successful creation of a hello-world container.
