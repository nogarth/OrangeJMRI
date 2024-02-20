# OrangeJMRI
setting up JMRI on an Orange Pi with LCD output and Access point for IP

# Prerequisits
First off download the minimal armbian for the OS (all my examples are built on Orange Pi 3 LTS)



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

Install XFont used by TightVNC server

<code>sudo apt-get install xfonts-base</code>

Install TightVNC server

<code>sudo apt-get install tightvncserver</code>

Setup this user for VNC server,

<code>vncserver :1</code>

We need to assign a password. No need to specify a view-only password.

Use the command to confirm the server is running and the default options applied

<code>ps -ef | grep Xtightvnc</code>

VNC Client can now connect to this server, display :1 refers to port 5901. Hence the connection string is <IP Address>:5901.

However, there is no windows shown up, as Armbian distribution does not include any X-window manager. Now we install Xfce, a light weight X-window desktop.


<code>sudo apt-get -y install xorg lightdm xfce4 tango-icon-theme gnome-icon-theme dbus-x11</code>
 
Restart VNC server

<code>vncserver -kill :1
vncserver :1</code>
 
Now the client will show up Xfce desktop over TightVNC.
 
To make TightVNC autostart on OrangePi startup, use systemctl control. Create a new script,

<code>sudo nano /usr/local/bin/tightvncserver</code>
 
The content of this script

<code>#!/bin/bash
PATH="$PATH:/usr/bin/"
DISPLAY="1"
DEPTH="16"
GEOMETRY="1024x768"
OPTIONS="-depth ${DEPTH} -geometry ${GEOMETRY} :${DISPLAY}"

case "$1" in
start)
/usr/bin/vncserver ${OPTIONS}
;;

stop)
/usr/bin/vncserver -kill :${DISPLAY}
;;

restart)
$0 stop
$0 start
;;
esac
exit 0 </code>

Make this script executable,
<code>sudo chmod +x /usr/local/bin/tightvncserver</code>
 
Setup systemd script
<code>sudo nano /lib/systemd/system/tightvncserver.service</code>
 
With this content

<code>
[Unit]
Description=Manage tightVNC Server

[Service]
Type=forking
ExecStart=/usr/local/bin/tightvncserver start
ExecStop=/usr/local/bin/tightvncserver stop
ExecReload=/usr/local/bin/tightvncserver restart
User=orangepi

[Install]
WantedBy=multi-user.target 
</code>

Restart Systemd service and enable tightvncserver,

<code>sudo systemctl daemon-reload
sudo systemctl enable tightvncserver.service</code>
  
Now we have 4 commands to start, stop, restart, and status over tightvncserver,

<code>
sudo systemctl start tightvncserver.service
sudo systemctl stop tightvncserver.service
sudo systemctl restart tightvncserver.service
sudo systemctl status tightvncserver.service
</code>
 
Reboot Orangepi. Now the connection is ready as OrangePi started.

<code>sudo reboot</code>

setup the Hotspot

<code>sudo nmcli device wifi hotspot ifname wlan0 ssid JMRIPI password "jmripi01"</code>

install NetworkMonitor Tray for GUI

<code>sudo apt install nm-tray>/code>




disable hibanate

<code> sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target </code>

