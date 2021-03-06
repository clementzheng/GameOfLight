# GameOfLight
Game of Light Installation


## Requirements
- 36 stations
- each station 1m in lenght covered in leds
- 5 sections of lamp to create a 'species'
- automatic identification of each lamp 'species'

## Main Power Supply
- 12,24V power supply recommended with a buck converter (for leds and mcu) or linear regulator (if for just mcu) at each location
- typical computer psu will have several 12V rails
- if there is 5m of leds with 30 leds/meter wrapped around a tube, then that is 150 leds. 150 leds at 60mA is 9A running at around 3V. This is around 27-30W assuming an efficient local conversion of power, which is likely embedded within the addressable chip.
- 36 stations of 30W is a total max draw of 1080W. So a 800W-1000W-1200W power supply should be fine.

## Local Power Regulation
- Switch mode power supply for high current (https://www.aliexpress.com/item/DC-CC-12A-300W-Step-Down-Buck-Converter-7-32V-To-0-8-28V-Power-module/32247251105.html)
- Linear regulator for low current needs (eg. if using 12V main power supply and 12V leds)

## Power Delivery
- ribbon cable (40 pin), using most pins for power and ground
- RJ45? probably can't handle the max current needs for 6 stations with 12V supply (15A)
- RJ11? probably can't handle the max current needs for 6 stations with 12V supply (15A)

## LEDs
- addressable color leds
- could use 1 2m strip folded over
- could use 1 5m strip wrapped around a pole (this will provide more light)
- WS2811 with 3 color leds on each section, each led is rgb, but in clusters of 3. This is fine for our applications. Also these are 12V, which is better for current draw. $8-10 per 5m strip: (https://www.aliexpress.com/item/best-price-5m-DC12V-ws2811ic-5050-RGB-SMD-individually-addressable-ws2811-led-pixels-strip/32385533484.html)

## Control
- recommended individual controller for each station; otherwise refresh rate is likely to be very slow
- attiny85 possible? may not have enough pins; but might
- atmega328p?
- arduino pro mini clone ($1-2)

## Recognition
- manual input (what a drag)
- infrared linear quadrature encoder or similar to recognize the lamp 'species' as a barcode when the lamp shade is slide over the rod
-- this would argue for a separate controller on each station

## Communication
- if using multiple controllers, one on each station, using a multidrop bus (https://en.wikipedia.org/wiki/Multidrop_bus) rather than a shift/ring topology
- I2C can go about 20ft without additional driver or buffers (http://forum.arduino.cc/index.php?topic=57604.0)
- RS-232 can go about 50ft (https://www.lammertbies.nl/comm/info/RS-232_specs.html)
- RS-485 can go about 4000ft (http://www.bb-elec.com/Learning-Center/All-White-Papers/Serial/Basics-of-the-RS-485-Standard.aspx)
-- RS-485 to ttl converter using the MAX485CSA (https://www.aliexpress.com/item/MAX485-Module-RS-485-TTL-to-RS485-MAX485CSA-Converter-Module-For-Arduino-Integrated-Circuits-Products/32667981058.html)
--- $0.38
-- needs twisted pair wire
