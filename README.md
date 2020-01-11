# My Raspberry Pi-setup

This repository contains the basic setup description for my Raspberry Pi's. 

## Download the image

Go to the Raspberry Pi org website  https://www.raspberrypi.org/downloads/raspbian/ and you will find a variety of available images, even Third Party images. Select the one that is fitting best to your project. 

I used the Raspian and the Raspberry Pi Desktop images. 

To deploy the image on the SD-Card I am using the `balenaetcher` application, but there are plenty of tools available to deploy the image.

## Mandatory steps to keep your Pi safe and ready to use

If you are using the Raspian image then you will be guided through the setup and it covers the major part of the listed steps below. 

### Update and Upgrade the system image

I prefer to use the batch job listed below to update, upgrade and restart my Pi, but I although list the single steps of the procedure. 

* Batch job:

   `sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get autoremove -y && sudo reboot`

* Step by step procedure
   1. sudo apt-get update
   2. sudo apt-get upgrade -y
   3. sudo apt-get autoremove -y
   4. sudo reboot

### Set the country, language and timezone

Use the command `sudo dpkg-reconfigure tzdata` 

Depending on your selection the installation of the required language might take some minutes. 

### Change the default password for the `pi`user account 

The default password is `raspberry`and well known in the Pi community and hacker community and highly recommended to change prior going live!

### Select the Wifi network  

You have to click with the left mouse button on the right main menu the wifi icon and select your WiFi network. 

### Restart 

Restart your Raspberry to activate your configuration and changes

## Configure the required interfaces as SSH and VNC

* GUI
   * Select the Raspberry icon in the upper main menu , go to `Preferences` and select `Raspberry Pi Configuration`
   * Select the tab `Interfaces` and enable the required interface

### Activate SSH

* Via Console
   * in the terminal session enter the command `sudo raspi-config` , 
   * select the entry `Interface Options` 
   * select the Entry `SSH` 
   * to enable SSH and follow the information displayed
   
### Activate VNC

* Via Console
   * in the terminal session enter the command `sudo raspi-config` , 
   * select the entry `Interface Options` 
   * select the entry `VNC`
   * to enable VNC and follow the information displayed
   * On the command line perform following steps
    * `sudo vncpasswd -service `, enter the service password
    * create in the directory `/etc/vnc/config.d`the file `common.custom` and add  the line `Authentication=VncAuth` 
    * run `sudo systemctl restart vncserver-x11-serviced`
   * Now you can use the integrated `vnc connect from RealVNC`, if you want to use tightvnc see the section further below.

## Resize root partition

* Via Console
   * in the terminal session enter the command `sudo raspi-config` , 
   * select the entry `Advanced Options` 
   * select the entry `Expand filesystem`
   * follow the information displayed, you have to reboot the Raspberry that the change will be activated.

## Install additonal tools

**Text Editor VIM**
1. sudo apt-get update
2. sudo apt-get install vim -y

**Browser**

The browser `iceweasel` has been depricated and you need to install the `firefox-esr` version. 

1. sudo apt-get update
2. sudo apt-get install firefox-esr

**Tight VNC server as an option to the integrated vnc connect by RealVNC**
* sudo apt-get install tightvncserver
* tightvncserver (initialisation)
    * Would you like to enter a view-only password (y/n)?
    * sample to start: vncserver :0 -geometry 1280x720 -depth 24 -dpi 96
* Activate if not already done prior the initial configuration phase
    * classic menu: sudo raspi-config  - Interfaces
    * standard menu: 
    * Main Menu -> Preferences -> Raspberry Pi Configuration
    * Tab Interfaces
    * Enable VNC
* Integrate into your profile shell script 

## FHEM installation

* update the system: `sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get autoremove -y && sudo reboot`
* Ensure that you have `resized the root partition!` , see section above. 
* Install the prerequisites for FHEM:
`sudo apt-get -f install && sudo apt-get install perl libdevice-serialport-perl libio-socket-ssl-perl libwww-perl libxml-simple-perl libjson-perl sqlite3 libdbd-sqlite3-perl libtext-diff-perl -y`

* Now download and install the latest FHEM version:
Find out the latest FHEM version here https://fhem.de/fhem.html#Download . In the sample below is 5.9 the current version.

`sudo wget http://fhem.de/fhem-5.9.deb && sudo dpkg -i fhem-5.9.deb` 

* If the installation was successful remove the install packages `sudo rm fhem-5.9.deb`
* Set the required access rights for FHEM:
   * cd /opt
   * sudo chmod -R a+w fhem
   * sudo usermod -a -G tty pi && sudo usermod -a -G tty fhem
   * sudo adduser fhem gpio
   * sudo reboot
   
* Now you can use the FHEM web interface at i.e.  `http:192.168.178.84:8083`. Be aware that the IP-address of your Raspberry depends on your network setup!

## The following section is under construction!!

**GIT installation**

* sudo apt-get install git
Github
already installed
* git init 
* optional touch README.md
* git add *  or git add —all
* git commit -a
* git remote add origin https://github.com/kapahnke-iot/<repository-name>.git
* git push -u origin master
    * username
    * password
for a an update first pull the remote master to your local directory
* git pull

https://help.github.com/articles/about-readmes/

http://kbroman.org/github_tutorial/pages/init.html

http://kbroman.org/github_tutorial/pages/routine.html


* sudo apt-get install -y make build-essential libssl-dev zlib1g-dev libbz2-dev \ libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \ xz-utils tk-dev

Command line history
* Ctrl+R is usually the best way, as descriptor said.


X Remote Desktop
* sudo apt get install xrdp
* to access the Raspberry Pi outside your network install the DNS: https://tutorials-raspberrypi.de/webserver-installation-teil-6-dns-server-via-no-ip/





SSH
* classic menu: sudo raspi-config - Interfaces
* standard menu: 
    * Main Menu -> Preferences -> Raspberry Pi Configuration
    * Tab Interfaces
    * Enable SSH
￼
Password
* classic menu: sudo raspi-config - Change User Password 
* standard menu: 
    * Main Menu -> Preferences -> Raspberry Pi Configuration
    * Tab System
    * Password Change Password


audio bluetooth
* vim alsa-base.conf
* sudo chmod -v 777 alsa-base.conf
* shutdown -r

nodejs 
* uname -m  if the responds starts with armv7 than that’s the version we need.
* go to https://nodejs.org/en/download and choose the version we need
* wget  https:// …. or download per ftp … 
* tar …. 
* cd node…
* sudo cp -R * /usr/local/ 
* node -v
* npm -v  

