# ESP8266 Built-in OLED – Heltec WiFi Kit 8

This text is based on [the robotzero blog](https://robotzero.one/heltec-wifi-kit-8/) but here we have the ubuntu version

![heltec device](https://github.com/pastaCLS/heltec/blob/master/images/heltec-device.jpg?raw=true)

A  set-up guide for the Heltec WiFi Kit 8 development board (an ESP8266 with built-in OLED display).
Follow the easy steps below to get up and running with this board using standard Arduino libraries.

This board is based on the ESP8266 chip and has onboard WiFi,  a 0.96inch 128 * 32 OLED display, lithium battery connector charging and a CP2014 USB to serial interface. It also works with the Arduino IDE!

## Setting Up the Arduino IDE for the ESP8266 Range

I made the setup in the following arduino's version:
![arduino version](https://github.com/pastaCLS/heltec/blob/master/images/version-arduino.jpg?raw=true)

and ubuntu:

![ubuntu version](https://github.com/pastaCLS/heltec/blob/master/images/version-ubuntu.jpg?raw=true)

In the IDE, open the File Menu->Preferences and in the field "Additional Board Manager URLs enter:

```
https://dl.espressif.com/dl/package_esp32_index.json, http://arduino.esp8266.com/stable/package_esp8266com_index.json
```


