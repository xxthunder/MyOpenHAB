# MyOpenHAB

## Parts list

![](images/parts.png)

* Raspberry Pi 4 B, 4x 1,5 GHz, 4 GB RAM, WLAN, BT
* Raspberry 4596 Pi - official power supply for Raspberry Pi 4 Model B, USB-C, 5.1V, 3A
* RPI CASE ALU08 (got it from [here](https://www.reichelt.de/de/de/gehaeuse-fuer-raspberry-pi-4-alu-schwarz-rpi-case-alu08-p272360.html?r=1))
* JSAUX USB 3.0 SATA Adapter (got it from [here](https://www.amazon.de/dp/B086W944YT/ref=cm_sw_r_awdo_navT_g_J4W8QZW49ZTRPVYGJE9D), found it on this [list](https://forum-raspberrypi.de/forum/thread/47876-magische-usb-sata-adapter-und-wo-sie-zu-finden-sind/))
* Some SATA SSD disk (e.g. 128 GBytes)

## Initial Commissioning

* Follow the [official description](https://www.raspberrypi.com/software/) to get Raspberry OS Lite onto a SD card.
* Put an empty file with name 'ssh' on the boot partition.
* Boot the Raspberry Pi.
* Login via ssh.
* use command 'sudo raspi-config' to configure the hostname to your needs.
* For robustness I choose a SSD SATA disk to boot from. To configure this do the following steps:
```bash
git clone https://github.com/billw2/rpi-clone.git
cd rpi-clone
sudo cp rpi-clone rpi-clone-setup /usr/local/sbin
sudo rpi-clone sda
sudo raspi-config
```
* Inside raspi-config:
   * 8 Update
   * 6 (Advanced Options) &rarr; A7(Bootloader Version) &rarr; E2(Default)
   * 6 (Advanced Options) &rarr; A6(BootOrder) &rarr; B2(USB Boot)
* reboot
* Pi should be running from sda1 (check with 'mount' or 'df -h')
* During the next shutdown phase you can remove the SD card.

## Ansible and Docker

My goal was to automate any further installation and configuration. Ansible seems to be the right tool for that job.
* Install Ansible:
```bash
sudo apt install ansible python3-docker
ansible-galaxy install geerlingguy.docker_arm geerlingguy.pip
ansible-playbook docker.yml
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

* https://www.rs-online.com/designspark/raspberry-pi-4-personal-datacentre-part-1-ansible-docker-and-nextcloud
* https://github.com/geerlingguy/ansible-role-docker_arm
* https://www.laub-home.de/wiki/Raspberry_Pi_mit_Raspbian_und_Docker