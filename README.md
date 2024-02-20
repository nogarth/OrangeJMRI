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


disable hibanate

<code> sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target </code>

