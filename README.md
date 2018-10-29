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
Open the Boards Manager from Tools > Board:xxxxx menu

![board manager](https://github.com/pastaCLS/heltec/blob/master/images/board-manager.png?raw=true)

Find esp8266 by ESP8266 Community in the list and click Install

The ESP8266 Hardware Libraries are now installed and you can test your new board with a simple Sketch.

## Testing the WiFi is Functioning

In the Arduino IDE, in the Tools > Board menu choose NodeMCU 1.0 (ESP-12E Module)

![nodemcu](https://github.com/pastaCLS/heltec/blob/master/images/nodemcu.png?raw=true)

Select the port

![port](https://github.com/pastaCLS/heltec/blob/master/images/port.png?raw=true)

You can now upload Sketches to the board. A good test is use the example WiFiScan sketch.

Open File->Examples->ESP8266WiFi->WifiScan and upload the sketch.

![burning sample](https://github.com/pastaCLS/heltec/blob/master/images/burning-sample.png?raw=true)

If you open the Serial Monitor (Tools > Serial Monitor) you will be able to see any WiFi access points in range. Check the baud rate is the same as in the sketch – probably 115200.

![wifi scan](https://github.com/pastaCLS/heltec/blob/master/images/wifiscan.png?raw=true)

## Displaying data on the WiFi Kit 8 OLED
U8g2 could be installed using de Arduino IDE library Manager. Open Sketch->Include Library->Manage Libraries and search for and the install U8g2

![u8g2](https://github.com/pastaCLS/heltec/blob/master/images/u8g2.png?raw=true)

and paste the following code:

```c
#include <U8g2lib.h>

//U8g2 Contructor
U8G2_SSD1306_128X32_UNIVISION_F_HW_I2C u8g2(U8G2_R0, /* reset=*/ 16, /* clock=*/ 5, /* data=*/ 4);
// Alternative board version. Uncomment if above doesn't work.
// U8G2_SSD1306_128X32_UNIVISION_F_HW_I2C u8g2(U8G2_R0, /* reset=*/ 4, /* clock=*/ 14, /* data=*/ 2);

u8g2_uint_t offset;     // current offset for the scrolling text
u8g2_uint_t width;      // pixel width of the scrolling text (must be lesser than 128 unless U8G2_16BIT is defined
const char *text = "GATO "; // scroll this text from right to left


void setup(void) {
  u8g2.begin();

  u8g2.setFont(u8g2_font_logisoso32_tf); // set the target font to calculate the pixel width
  width = u8g2.getUTF8Width(text);    // calculate the pixel width of the text

  u8g2.setFontMode(0);    // enable transparent mode, which is faster
}


void loop(void) {
  u8g2_uint_t x;

  u8g2.firstPage();
  do {

    // draw the scrolling text at current offset
    x = offset;
    u8g2.setFont(u8g2_font_logisoso32_tf);   // set the target font
    do {                // repeated drawing of the scrolling text...
      u8g2.drawUTF8(x, 32, text);     // draw the scolling text
      x += width;           // add the pixel width of the scrolling text
    } while ( x < u8g2.getDisplayWidth() );   // draw again until the complete display is filled

    u8g2.setFont(u8g2_font_logisoso32_tf);   // draw the current pixel width
    u8g2.setCursor(0, 64);
    u8g2.print(width);          // this value must be lesser than 128 unless U8G2_16BIT is set

  } while ( u8g2.nextPage() );

  offset -= 1;            // scroll by one pixel
  if ( (u8g2_uint_t)offset < (u8g2_uint_t) - width )
    offset = 0;             // start over again
}

```

