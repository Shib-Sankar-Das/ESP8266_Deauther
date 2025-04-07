# ESP8266 Deauther
This firmware allows you to easily perform a variety of actions to test 802.11 networks using an ESP8266. It's also a great project for learning about WiFi, microcontrollers, Arduino, hacking and electronics/programming in general.

<p float="left">
  <img src="https://github.com/user-attachments/assets/c195f79b-655a-443f-8e1b-dfc4bab50059" width="45%" />
  <img src="https://github.com/user-attachments/assets/d8963b37-24a8-4d1c-934e-4ea5843a5195" width="45%" />
</p>

The deauthentication attack is the main feature, which can be used to disconnect devices from their WiFi network.
Although this denial-of-service attack is nothing new, a lot of devices are still vulnerable to it. Luckily this is slowly changing with more WiFi 6 enabled devices being used. But a lot of outdated WiFi devices remain in place, for example in cheap IoT hardware. With an ESP8266 Deauther, you can easily test this attack on your 2.4GHz WiFi network/devices and see whether it's successful or not. And if it is, you know you should upgrade your network.

## How it works
A deauthentication attack works by sending packets that tell the receiver they are disconnected. Deauth frames are a necessary part of the WiFi protocol. However, these packets are often unprotected. This means that any WiFi device can theoretically craft packets that disconnect nearby connections. All they need to know is the sender and receiver address, which can be observed by passivly scanning for WiFi devices.
To effectively prevent a deauthentication attack, both the client and access point must support protected management frames (PMF).

In 2009 the WiFi Alliance provided a fix for the problem (802.11w), but most devices didn't implement it. This is finally changing in 2021 with the introduction of WiFi 6! Although it's not a guarantee to be safe, I found that most WiFi 6 certified devices are immune to this attack. But remember that it requires both access point and client to support the new standard.

### WiFi Jammer
Many refer to this project as a WiFi jammer. This can be misleading because this firmware is not turning an ESP8266 into a radio or frequency jammer. Although radio jamming and deauthing are both denial of service attacks, deauthing only affects targeted WiFi devices. In contrast, jamming affects every wireless communication device of a specific frequency in its range.
It's really dangerous when you cannot know/control what you are disrupting and how. This is why jamming is illegal almost everywhere.

## Download
For flashing the firmware, choose Binaries and select your device.
If you want to open the project in Arduino IDE, choose Source Code **(esp8266_deauther_2.6.1_DSTIKE_USB_DEAUTHER_V2.bin)**.

## DIY Tutorial
How to build a Deauther yourself with off-the-shelf parts.
### Supported Devices
The most important things first:

- Any ESP8266-based development board can run the Deauther firmware
- ESP8285 is also supported (basically the same as ESP8266 but with internal flash)
- ESP32 is not supported as it's an entirely different chip
#### Recommended Boards
The sheer amount of different boards available can create uncertainty about which one to buy. So here we've compiled a small list of boards we can recommend. Feel free to use this list not only for the Deauther project but as a recommendation for good ESP8266 development boards in general.

##### NodeMCU (ESP8266)
The NodeMCU board is probably the most popular ESP8266 development board. It's cheap, widely available, uses the ESP12 module, and has pre-soldered header pins - which come in handy when using a breadboard.

The original NodeMCU (as seen in the picture above) uses a CP2102 USB serial chip. The NodeMCU V3 is slightly bigger and uses the CH340 chip. However, both versions work the same.

Do not buy an ESP32 version if you're planning to build a Deauther. You'll need an ESP8266!

### Installation (.bin)
1. Get a .bin file for your board from [deauther.com](https://deauther.com/docs/download/)
2. Open [esp.huhn.me](https://esp.huhn.me/) in Chrome, or another supported browser
3. Connect your ESP8266 board via USB
4. Click Connect and select the serial port of your ESP
5. Select your Deauther .bin file
6. Click Program

![espwebtool-6d469715aba3e64ebbc8faebebd19168](https://github.com/user-attachments/assets/428cd3c9-cdf2-469d-bfc2-6fadbcfd7f30)


#### Finding the correct port
If you don't know which serial port to select, click connect on [esp.huhn.me](https://esp.huhn.me/) and then plug in your board. Whatever port pops up in the list is what you're looking for.

You should check the cable and USB port if no new port pops up. Some USB cables are only for charging and cannot transmit data.

Or maybe you're missing the drivers for your device:

🔗 CH340/CH341 Drivers: [http://www.wch-ic.com/downloads/CH341SER_ZIP.html](https://www.wch-ic.com/downloads/CH341SER_ZIP.html)

🔗 CP210x Drivers: [https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers](https://www.silabs.com/developer-tools/usb-to-uart-bridge-vcp-drivers)

🔗 FTDI Drivers: [https://ftdichip.com/drivers/](https://ftdichip.com/drivers/)

#### Connection failed?
Make sure to set the baud rate to 115200 in the settings. Higher baud rates allow faster upload speeds but can also introduce connection issues.

If that doesn't help, check out this blog post about common ESP8266 and ESP32 errors: https://blog.spacehuhn.com/espcomm/

And if you run into other issues, try using a different flashing tool/method.

#### Alternative Tools
My ESP web tool is not the only software you can use to flash your ESP8266:

- [esptool](https://github.com/espressif/esptool)
- [ESP flash download tools](https://www.espressif.com/en/support/download/other-tools)
- [esptool-gui](https://github.com/Rodmg/esptool-gui)

And if you're looking for something Deauther-specific, check out n2d: [https://github.com/realmrvodka/n2d/](https://github.com/a4004/n2d)

#### Installation (Arduino IDE)

1. Extract the ESP8266 Deauther zip you downloaded
2. Go into the esp8266_deauther folder and open esp8266_deauther.ino with Arduino IDE
3. In Arduino IDE, go to File > Preferences and add this URL to the Additional Boards Manager URLs: **https://raw.githubusercontent.com/SpacehuhnTech/arduino/main/package_spacehuhn_index.json**
4. Now go to **Tools > Board > Boards Manager**, search deauther, and install Deauther ESP8266 Boards
5. Select your board at **Tools > Board** and be sure it is at Deauther ESP8266 Boards (and not at ESP8266 Modules)!
6. Plugin your Deauther and select its COM port at **Tools > Port**
7. Optional: To reset/override previous settings select **Tools > Erase Flash > All Flash Contents**
8. Press upload
Done 🎉

![arduino-tutorial-6f94987d729b12ae3959e35256e46840](https://github.com/user-attachments/assets/1db32de0-1536-42bf-9c99-912ba27e810c)

#### Upload Errors
##### "error: espcomm_open failed"

![espcomm-a5bd2bb6bb0ed01df2b4b2aa85805ae0](https://github.com/user-attachments/assets/5c9677a7-3037-4a84-a2a3-3da1f9bb91bd)

If you work with ESP32 or ESP8266 boards, regardless of the firmware you want to install, you will likely encounter this error sooner or later. The espcomm_open error is not a compiler error. It appears when you try to upload firmware, but [esptool](https://github.com/espressif/esptool) fails to establish a connection.

Besides *espcomm_open*, other common errors include *espcomm_sync* and *Timed out waiting for packet header*.

```
warning: espcomm_sync failed
error: espcomm_open failed
Failed to connect to ESP8266: Timed out waiting for packet header
serial.serialutil.SerialTimeoutException: Write timeout 
  does not exist or your board is not connected
```
Error messages [Esptool](https://github.com/espressif/esptool) is a python script made for flashing the ESP32 or ESP8266. It can be used directly through the command line or indirectly through an IDE like Arduino.

If it fails to open a connection to your development board, check these things:

- Make sure to have the correct serial (COM) port selected
- Install missing drivers
- Try another USB cable (some only provide power and transfer no data)
- Try a different USB port and avoid USB hubs, dongles, or adapters
- Make sure the serial connection isn't already in use by another program
- Hold down the flash button or connect GPIO-0 (D3) to GND
- If everything fails, try it on another computer

##### Select the correct port

![arduinoserialport-cf33a406265e1a4f05eab359c5f2bc2e](https://github.com/user-attachments/assets/f255be30-7482-44c5-a8ce-97c7eb1938d1)

Before you can flash firmware onto a development board, you must select a serial port (COM port).

In Arduino IDE, you select it by going to **Tools** and then **port**.

To figure out which serial port corresponds to your dev board, look at the list (without your board plugged in), then plug in your dev board and observe which new serial port appeared in the list.

If you don't see a new port appear when you plug in your board, or the menu is grayed out completely, then no new serial port was detected.
This can be caused by a missing driver or a defective USB cable. Continue reading in this case.

##### Drivers
**Bad news 😔:** There are multiple drivers, and we can't tell you which one you need. It depends on the hardware you have.

**Good news 😃:** There are only 3 different families of serial chips used on almost all development boards. So worst case, you install all of them.

Below is a list of those chips with links to their manufacturer's drivers' download page. The pictures shown are examples. All these chip families exist in different sizes (packages) and can look different on your development board.

###### CH340 & CH341

![ch340-2e6172cfc0b63a4deb3c0fb359a26db1](https://github.com/user-attachments/assets/a7a5f259-a043-4a0d-bba6-72802326f7be)

The [CH340/CH341](https://www.wch-ic.com/downloads/CH341SER_ZIP.html) is a very common USB to serial chip family, used often in cheap development boards thanks to its affordable pricing.


##### The USB connection

![usb-e9a3d6cd04774686591c21de536aa539](https://github.com/user-attachments/assets/ef3892e1-0403-4aae-a98e-ec56b5b4d143)

If you installed the drivers, but no new serial port is detected, it might be the cable itself. Some USB cables are made for charging only and can't transmit data. Try another cable.

Sometimes it can also be enough to use a different physical USB port.

Avoid USB hubs, dongles, or other adapters in between the connection that could cause problems.


##### Flash button

![flash-2948dc54f011cd94f784208b6bc484a6](https://github.com/user-attachments/assets/e0cdd7c8-61c1-4904-85a5-a88e9da4a836)

If your board is detected and you are sure to have selected the correct port, but uploading firmware still doesn't work, it might be because of the development board itself. The ESP has to be in flash mode to accept new firmware.

Most ESP32 and ESP8266 boards have an automatic reset and flash circuit. Meaning they can be restarted and put into flashing mode automatically. But sometimes, that circuit is defective or hasn't been implemented correctly.

To manually put the ESP32 or ESP8266 into flashing mode, you need to connect GPIO-0 (D3) to GND. Some boards have a dedicated button for that. Other boards don't - in which case you'd have to connect those 2 pins with a wire.

With the flash button pressed or GPIO-0 connected to GND, plug in your board or hit the reset button. Then start uploading the firmware. Sometimes, you need to keep the button pressed or the pins connected until the upload begins. This part is sometimes tricky and might require a bit of trial and error.

Then you must disconnect the pins and restart the board (unplug and plug it in again). It should then be back to the regular boot mode and run your newly flashed firmware.

### Web Interface

To access the web interface, your Deauther must be running, and you have to be connected to its WiFi network pwnd using the password deauther.

Then open your browser and visit 192.168.4.1. Make sure you're not connected to a VPN or anything else that could get in the way. You have to temporarily disable the mobile connection on some phones to make it work.

If you can't see a pwned network, ensure ESP8266 Deauther firmware was successfully installed. We made a tutorial for that, which you can find here.

#### Home / Warning Page

![home-39e35982d596044fa0d1abe658c3c0cb](https://github.com/user-attachments/assets/bb400cff-b842-4eba-b249-0170f46d4b7b)

The first thing you'll probably see when you open the web interface is a warning that you must confirm to continue.

We felt this was necessary when making it since many users would abuse our tool and spread misinformation about how it works.

#### Scan Page

![scan-990653ea79d4c5a116e8fec295650a37](https://github.com/user-attachments/assets/0e66e7f7-a932-41ca-8d65-810219a26490)

On the scan page, you can discover access points (WiFi networks) and stations (client devices) nearby. If the access point list is empty, click on SCAN APS.

A scan takes a few seconds (usually 2 - 5 seconds). Depending on your board, you might see a LED turning on when starting the scan. As soon as the scan is finished, it turns off, signaling you to click on RELOAD to see the scan results.

![scan2-b66189015d5425d3c9701de3b9f98d2a](https://github.com/user-attachments/assets/407d2c68-947d-4388-85f2-574689eff56a)

Once you have a list of the access points, you can select them for an attack. But make sure only to select your own networks. Attacking other people's networks on purpose is strictly prohibited!


You can select multiple targets, but it's recommended to select only a single one for stability and performance reasons.

You can also scan for stations to select a specific client rather than an entire network. While a station scan is running, the web interface will be unavailable. You have to wait until it's finished and then reconnect.

#### SSID Page

![ssid1-0accf03d80782e73f5bd963d324e1303](https://github.com/user-attachments/assets/e5b40f75-6c32-406f-9c98-7172ad8ef8b4)

This is where you can add, edit and remove SSIDs. An SSID (Service Set Identifier) is the name of a WiFi network. They are used in beacon and probe attacks.

![ssid2-5041ef114f06aa456e648f7bcfacfece](https://github.com/user-attachments/assets/25830f18-f7cd-4d75-8f15-11ca0200aa67)

#### Attack Page

![attack-87686eb3a5088fffc93ac834765aec3e](https://github.com/user-attachments/assets/d1829fcf-af44-408e-a858-cc6a4f9b9951)

On the attack page, you start and stop WiFi attacks such as Deauthentication, Beacon, and Probe.

You may lose connection to the web interface when initiating an attack, but if you only select one target, you may be able to reconnect to it without problems. Attacks stop after 5 minutes by default. This is intended behavior to prevent abuse.

The pkts/s info is not automatically refreshed to save resources. You have to manually click RELOAD.

#### Settings

![settings-9ab7f8b383706568f78feb6eafdcd0b2](https://github.com/user-attachments/assets/e935213d-874e-40cc-867e-00c4b5ba7fc2)

You can edit device settings here, such as the SSID and password of Deauther's network. But make sure to hit SAVE after changing something and click on RELOAD to refresh the site and check whether or not your changes were applied.

#### Errors

When using this tool, a thing to keep in mind is that the ESP8266 Deauther project was a proof of concept that became a popular tool for beginners to learn about WiFi hacking.

It's not a professional tool. It's free and open source. So please understand that:

The web interface is sometimes unstable and creates errors.
You will lose connection to the Deauther when starting a scan or an attack.
The attacks are meant for testing. They are not guaranteed to work. Learn more here.
The amount of networks and devices you are able to pick up and attack is limited by a variety of external factors, including but not limited to the transmit power of such a small device and its antenna.

