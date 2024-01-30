# LunaHub
Astronomy power and USB hub, in development.

![image](https://github.com/GeneralSyb/LunaHub/assets/56089117/2a5c14ec-9b13-4b98-96c2-a40b7dd93848)
![image](https://github.com/GeneralSyb/LunaHub/assets/56089117/222b00e3-edba-43f9-b170-9d51daf71fc6)
![image](https://github.com/GeneralSyb/LunaHub/assets/56089117/a1d555ad-fb2f-4683-9b4a-7e533d3e462b)
![image](https://github.com/GeneralSyb/LunaHub/assets/56089117/85a2e01e-bca4-4cce-be38-a9549744a915)

For now just work in progress design files for the USB hub PCB. On top of this will come the power supply PCB that has a number of buck converters to power the USB hub and a handfull of barrel jacks. I chose to keep these two boards seperate so that I don't need to worry too much about keeping one PCB small and so that I can build and test them indepentendly. To provide power to the USB hub the PSU board has a 1.1V and a 3.3V buck converter which can supply enough current to power all the electronics. The example design from TI for the TUSB8041 USB 3.1 hub IC show the usage of load switches which are controller by the IC to switch the maximum current as requested by the connected device. However to save on cost and to allow "dumb" devices to draw a lot of current, I didn't do this and connected the USB 5V power pins directly to the buck converters on the PSU board. Of course with a poly fuse chosen to allow a maximum current of 1.5A per port.

I chose to use the TUSB8041 hub IC because it was cheap, provides a lot of automatic features and seemed easy enough to use in a DIY USB hub, given my experience (which honestly isn't a whole lot).
For configuration of the IC there are a number for pins that are pulled either high or low with a resistor, and the rest is done by programming the I2C EEPROM IC. This storage chip can be programmed by removing the jumpers and connecting GND, 3.3V, SDA and SCL to an external microcontroller. The minimum amount of EEPROM storage required by the TUSB8041 is 2kB, so the 4kB EEPROM IC that I chose should be plenty.

All the differential pair lines and vias should have an impedance of 90 Ohms with a tolerance of 5% and the superspeed lines have their length matched as best as possible. The highspeed lines are mostly the same, except for the upstream port where the placement of the pins on the connector made the length matching really hard. This has been calculated using the Saturn PCB toolkit with a dielectric constant of 4.1 and a prepreg thickness on the 0.0994mm. (more details about the JLC04161H-3313 stackup can be found on [JLCPCB's](https://jlcpcb.com/impedance) website)
