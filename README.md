# OrangeJMRI
setting up JMRI on an Orange Pi with LCD output and Access point for IP

# Prerequisits
First off download the minimal armbian for the OS (all my examples are built on Orange Pi 3 LTS)

https://www.armbian.com/orangepi3-lts/

Boot machine with HDMi and Keyboard connected and follow first time setup with your preferences.

![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/63bc7a5d-b240-41fb-b484-4350edec5cb2)


![image](https://github.com/nogarth/OrangeJMRI/assets/1279577/8d7eca18-1bb9-4d02-ada4-f6c8e554b10a)


disable hibanate

<code> sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target </code>

