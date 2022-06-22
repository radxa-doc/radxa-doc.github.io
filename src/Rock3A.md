# Getting Started with ROCK 3A 
This guide is designed for ROCK 3A enthusiast. The purpose is to learn about ROCK 3A as well as how to prepare and set up for basic use.
When you get a board, you need to know what model it is and which hardware version it is.
The information is printed in the top side of the board.
We will introduce the board information as much as possible.
# What you need

## Necessary 
* ROCK 3A main board

* One of the Storage media below:
  * microSD, larger than 8GB
  * eMMC module, larger than 8GB

* Power supply
  * The ROCK 3 is powered by Type-C port and has a wide range of input voltage, from 9V to 21V. ROCK 3 supports USB Type-C PD 2.0 with 9V/2A, 12V/2A, 15V/2A and 20V/2A. Besides, the Pi supports QC 3.0/2.0  with 9V/2A and 12V/1.5A.
  * The Type-C cable you using needs to support data communication. We call it USB Type-C charging data cable.

* USB Keyboard and Mouse
  * With four USB-A connectors, ROCK 3 can be equipped with a full sized keyboard and mouse.

* Monitor and HDMI Cable
  * ROCK 3 is equipped with a full sized HDMI connector. HDMI capable monitor is recommended.
  * HDMI EDID display data is used to determine the best display resolution. On monitors and TVs that support 1080p (or 4K) this resolution will be selected. If 1080p is not supported the next available resolution reported by EDID will be used. This selected mode will work with MOST but not all monitors/TVs.

* USB to TTL serial cable
  * ROCK 3 exports a dedicated serial console for CPU, which can access the low level debug message.

* USB Male A to Male A cable
  * If you want write image on ROCK 3 from USB OTG port or use fastboot/adb commands you need an USB Male A to Male A cable to connect ROCK 3 and PC.

## Optional 
* microSD Card Reader
  * For flashing the image into microSD Card 

* USB type A to type A cable
  * This is needed for fastboot/adb commands.

*  USB to TTL serial cable
  * This is needed for serial console.

*  Ethernet cable
  * ROCK 3 supports Internet access via WIFI or Ethernet.
  * An Ethernet cable is used to connect your ROCK 3 to a local network and  the Internet.

* Camera Module
  * ROCK 3 supports  camera function.

* LCD Module
  * ROCK 3 supports LCD display function.

* Audio cable
  * Audio can be played through speaker or headphones using a standard 3.5mm jack.

* [ WiFi/BT Cards](https://wiki.radxa.com/Rock3/hardware/wifi)

# Starting the board for the first time

ROCK 3A can be started with eMMC Module or μSD Card. Now, you are presented with three options when installing your new operating system onto your ROCK 3A. 

# Prepare 
* When starting system with eMMC Module  
(Option a) Insert the eMMC Module into ROCK Pi eMMC USB Reader. Then plug the ROCK Pi eMMC USB Reader into host PC.  
(Option b) Insert eMMC Module into eMMC to μSD card converter board. Insert the converter board into μSD Card Reader. Then plug the Card Reader into host PC.

* When starting system with μSD Card
(Option c) Insert the μSD Card into μSD Card Reader. Then plug the Card Reader into host PC.

## Image flash tool

* Download the flash tool, etcher, from [downloads](https://wiki.radxa.com/Rock3/downloads). Choose the right version for your host operation system. Here we operate on host Ubuntu 16.04.

* Do update your etcher to latest edition according to etcher's instruction after you launch it. Otherwise, your pc might malfunction during flashing.
## Network setup
###  Ethernet
ROCK 3A is equipped with one 1G Ethernet port.
You can use a network cable (one end connected to the external network port or route) to connect your ROCK 3 to the network.
The ROCK 3 will automatically configure the network for your surfing on the Internet.

#### To test the Ethernet, we need to follow the steps:

* Switch to super user mode by command
`$ sudo su`

* Check whether the Ethernet is normal by command, ifconfig, which would show us a network card, eth0, and the Ethernet IP address. Also, use tool, ping, to connect to a normal domain. 
```
 $ ifconfig
 $ ping www.baidu.com
 ```

* If failed to connect to a normal domain. , try 
 `$ sudo dhclient eth0`

 ### WIFI
 ROCK 3 Model A doesn't come with on board WiFi/BT. Currently the following WiFi Cards are tested and supported by the ROCK 3 Model A.
 | Model                      | Chip       | WiFi              | BT  | Others       |
 | -------------------------- | ---------- | ----------------- | --- | ------------ |
 | ROCK Pi Wireless Module A1 | BCM43436B0 | 2.4G, 36Mbps      | 4.2 |              |
 | ROCK Pi Wireless Module A2 | BCM43456   | 2.4G&5G, 200Mbps  | 5.0 |              |
 | ROCK Pi Wireless Module A3 | BCM43598   | 2.4G&5G, >400Mbps | 5.0 | Support RSDB |
 | ROCK Pi Wireless Module A6 | BCM43752   | 2.4G&5G, WiFi 6   | 5.0 |              |
 | Realtek RTL8723BE          | RTL8723BE  | 2.4G              | 4.0 |              |
 | Realtek RTL8822CE          | RTL8822CE  | 2.4G&5G           | 5.0 |              |
 | Intel 0MHK36               | Intel 3165 | 2.4G&5G           | 4.2 |              |
 | Intel 7265NGW              | Intel 7265 | 2.4G&5G           | 4.2 |              |

* More Intel WiFi cards are supported in theory as long as the kernel versions requirements < 4.19 for vendor kernel. The WiFi firmware should be put under '''/lib/firmware''' manually. Check [Intel website](https://www.intel.com/content/www/us/en/support/articles/000005511/wireless.html ) for the WiFi card model and download fw.
* Check whether your sbc support WIFI either through Hardware or command line. Rock 3A doesn't have wifi module.

#### To test the WIFI performance, we need to follow the steps: 

* Switch to super user mode
` $ sudo su`

* Open the WIFI
` $ nmcli r wifi on`

* Scan WIFI
` $ nmcli dev wifi`

* Connect to WIFI network
`$ nmcli dev wifi connect "wifi_name" password "wifi_password"`

* Test WIFI perpormance by tool iperf3.
***
### Now you can check your Network state

*Look at network configure:
`$ sudo ifconfig`

*Test network:
`$ping -c 5 www.google.com`