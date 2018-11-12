# Catching the firmware

We are hackers, and we want to learn how easily could be make reverse enginerring over an esp8266.

First, we could catch the firmware that would be uploaded to the device just reading the log window

![disclosure](https://github.com/pastaCLS/heltec/blob/master/images/disclosure.png?raw=true)

when we read the first bytes of the file, we get:

![binary](../images/binary.png)

## que tiene el dispositivito este

un procesador esp8266ex, una flash de 4mb winbond donde storea el programa y un conversor ttl serial cp2102

![esp8266](../images/heltec-devices.png)

## Connecting the logic analizer

with the logic analyzer we could read lalalaa

![logic](../images/analisador1.jpg)

con zoom

![logic](../images/analisador2.jpg)

para conectarlo nos basamos en el datasheet

![datasheet](../images/winbond.png)
