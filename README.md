# OrangeJMRI
setting up JMRI on an Orange Pi with LCD output and Access point for IP

# Prerequisits
First off download the minimal armbian for the OS (all my examples are built on Orange Pi 3 LTS)

https://www.armbian.com/orangepi3-lts/

Boot machine with HDMi and Keyboard connected and follow first time setup with your preferences.

![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/63bc7a5d-b240-41fb-b484-4350edec5cb2)

login via putty to your IP of the Orangepi

![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/f19452cc-bdec-4018-ba5e-deb9a4696735)

install armbian-config

<code> sudo apt update && sudo apt install armbian-config </code>

Press Y and Enter to proceed on installing

![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/ea1f1d32-62e1-4928-9e53-740f920e27d4)

![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/4752c497-eb1b-4fbd-b3f7-ae2105b301ce)

Load Armbian Config

<code> sudo armbian-config </code>

![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/607ae69c-755b-4d75-99ec-d048b2b29246)

change to Stable selecting System > Stable
then update all firmware System > Firmware

Reboot

Load Armbian Config

<code> sudo armbian-config </code>

now setup wireless for the USB Wireless

Select Network > WiFi

![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/811d2fda-83ec-44df-9301-cd1c88339218)

setup HotSpot

![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/51f1b348-bd8a-42e5-9d5b-a1aacb948497)

wlan0

exit and unmask hostapd

<code>sudo systemctl unmask hostapd.service
sudo systemctl enable hostapd.service
sudo reboot now</code>



disable hibanate

<code> sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target </code>

