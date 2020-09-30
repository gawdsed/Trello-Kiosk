30 Sept 2020: Edited from Zuehlke for Raspbian Buster support and new atlassian login script

# Trello-Kiosk

This script enables you to display a Trello dashboard with a RaspberryPi after startup. Currently, it supports Raspbian Jessie.

## Pre-requisites
At first, you can improve the performance of the RaspberryPi by overclocking its core and expanding the space on the SD-Card. Open the configuration of the RaspberryPi by executing the following command.

```
sudo raspi-config
```

Select the option to increase your space on the SD-Card. I would recommend to overclock the Pi to medium level (900Mhz).

## Remove unnecessary software.
If your SD-Card is only 4GB you can perform following steps in order to free up around 1GB.

**Wolfram will free 460MB.**
```
sudo apt-get purge wolfram-engine -y
```

**Libreoffice will free 253MB.**
```
sudo apt-get purge libreoffice* -y
```

**BlueJ Java IDE will free 123MB.**
```
sudo apt-get purge bluej* -y
```

**Greenfoot will free 10.2MB.**
```
sudo apt-get purge greenfoot* -y
```

**Clean apt-get cache.**
```
sudo apt-get clean
```

**Check your free space on your SD-Card.**
```
df -h
```

**Remove empty icons from the menu bar. This might free 157MB.**
```
sudo apt-get autoremove
```

## Update your RaspberryPi Raspian OS
This command will update your software of your OS.
```
sudo apt-get update && sudo apt-get upgrade -y
```

# Install the Epiphany web browser
The following command you will install the Epiphany web browser and tools for the kiosk mode and automation of key inputs.
```
sudo apt-get install epiphany-browser x11-xserver-utils xautomation unclutter -y
```

# Configure autostart
Edit the autostart file 
```
raspbian Jessie:
sudo vi ~/.config/lxsession/LXDE-pi/autostart

raspbian Buster:
sudo vi /etc/xdg/lxsession/LXDE-pi/autostart
```

Add these lines to the autostart file. For the last line, replace your relative path to your Trello dashboard and the user as well as its password.

This is the relative path after the trello domain to your dashboard.
> [TRELLO_BOARD_RELATIVE_PATH]=/b/xXXxxXXx/dashboard-name

This is your username for Trello.
> [USER]=foo.bar[at]email.com

This is your password for your user on Trello.
> [PASSWORD]=********

```
@xset s off
@xset -dpms
@xset s noblank
@/home/pi/Trello-Kiosk/trello-kiosk.sh [TRELLO_BOARD_RELATIVE_PATH] [USER] [PASSWORD] > /dev/null 2>&1
```

# Checkout GitHub repository
Clone the repository to the home folder of your *pi* user **/home/pi**.
> git clone https://github.com/Zuehlke/Trello-Kiosk.git

**Change the permissions.**
> sudo chmod 755 /home/pi/Trello-Kiosk/trello-kiosk.sh

Reboot your RaspberryPi. It should show your Trello dashboard when it started after around one minute.
