# MyOpenHAB

## Parts list

![](images/parts.png)

* Raspberry Pi 4 B, 4x 1,5 GHz, 4 GB RAM, WLAN, BT
* Raspberry 4596 Pi - official power supply for Raspberry Pi 4 Model B, USB-C, 5.1V, 3A
* RPI CASE ALU08 (got it from [here](https://www.reichelt.de/de/de/gehaeuse-fuer-raspberry-pi-4-alu-schwarz-rpi-case-alu08-p272360.html?r=1))
* JSAUX USB 3.0 SATA Adapter (got it from [here](https://www.amazon.de/dp/B086W944YT/ref=cm_sw_r_awdo_navT_g_J4W8QZW49ZTRPVYGJE9D), found it on this [list](https://forum-raspberrypi.de/forum/thread/47876-magische-usb-sata-adapter-und-wo-sie-zu-finden-sind/))
* Some SATA SSD disk (e.g. 128 GBytes)

## Initial Commissioning

* Follow the [official description](https://www.raspberrypi.com/software/) to get Raspberry OS Lite onto an SD card and configure it according to your needs (user account, ssh, WiFi, etc.)
* Boot the Raspberry Pi and login.
* For robustness I choose a SSD SATA disk with an USB 3.0 adapter to boot from. Therefore the following steps are necessary:
   * Start raspi-config: 
   ```bash
   sudo raspi-config
   ```
   * Inside raspi-config:
      * 8 Update
      * 6 (Advanced Options) &rarr; A7(Bootloader Version) &rarr; E2(Default)
      * 6 (Advanced Options) &rarr; A6(BootOrder) &rarr; B2(USB Boot)
* Get Raspberry OS Lite onto the SSD.
* Connect SSD and reboot.
* Pi should be running from sda1 (check with 'mount' or 'df -h')
* During the next shutdown phase you can remove the SD card.

## Ansible and Docker

My goal was to automate any further installation and configuration. Ansible seems to be the right tool for that job.
* Install Ansible on your control host. I use the Pi itself for this, so I need these packages:
```bash
sudo apt update
sudo apt upgrade
sudo apt install ansible git python3-docker build-essential cargo python3-pip
sudo reboot
```
* Run playbooks of this repo:
```
git clone https://github.com/xxthunder/MyOpenHAB.git
ansible-playbook main.yml --extra-vars "piuser=$USER"
```
* Reboot:
```bash
sudo reboot
```
* Check Docker:
```bash
docker ps
docker run hello-world
```
* You should get a message about successful creation of a hello-world container.

## Sources, References and Ideas

* https://community.openhab.org/t/ansible-revisited/105754
* https://github.com/fex01/ansible-openhabserver
* https://www.laub-home.de/wiki/Raspberry_Pi_mit_Raspbian_und_Docker
