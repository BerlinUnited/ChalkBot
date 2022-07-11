Configuration Raspberry Pi 
============

# SSH Connection

## Configuration using command line:

To open the configuration tool on a Raspberry Pi, enter the following command line in the command prompt:

```bash
$ sudo raspi config
```
Scroll up and down using tab-key and arrows, navigate *SSH* then *YES*, then *OK* then 
click *Finish*.

## Configuration using desktop:

Go to menu *Preferences*, choosing *Raspberry Pi configuration*. Then the corresponding GUI opens with setting options, you should select SSH via interface options and release the corresponding option.

![Raspberry Pi Configuration Tool](img/chalkbot_raspi/2022-06-18_21-03-52.png)
*Images were taken from [www.raspberrypi.org](https://www.raspberrypi.org/)*

## Configuration using systemctl:

```bash
$ sudo systemctl enable ssh
```
```bash
$ sudo systemctl start ssh
```


!!! note annotate "IP-address of Rapsberry Pi" 
    
    You'll need to write down your Raspberry Pi's IP address to connect to it later. The ifconfig command displays information about the current network status, including the IP address, or you can use hostname -I to display the IP addresses associated with the device.

For connection with the *Raspberry Pi* you need to type in the following:
```bash
$ sudo pi@<IP>
```