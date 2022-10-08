# Research home assistant with EcoFlow powerstation(s)
## Testing, monitoring and controling EcoFlow Delta Max in combination with EcoFlow River 600, Raspberry PI400, TP-Link WR1043ND Freifunk and 400W solar power
### Abstract
Is it possible to run this setup stable, self-automated and self-regulated, off grid and without internet connection? <br>
In addition we have a close look at data security and privacy. <br>
We test efficiency and usability of different use cases e.g. water heating, air condition, cooling, office setup. 
This will be an ongoing report.<br>
##### Results with focus on Delta Max and AC usage
- Efficiency is up to 90% with loads ~2KWh, e.g. Water Heater
- Efficiency is up to 85% with loads ~300W, e.g. Workstation
- Efficiency is ~50% with loads ~ 50Wh, e.g. low energy PC and low energy Display
- Efficiency is down to 20% with loads ~15Wh, e.g. fridge <br>

On lower loads, it is probably better to use the River 600. <br>
Self measurement of unit is very inexact (inaccurate). <br>
Fan is noisy. <br>
##### Security, privacy and control
EcoFlow App uses Oauth for mqtt connection, this looks very secure and has a lot of features. <br>
EcoFlow Servers are in China, anonymized connections via Tor are impossible, different VPN work, other not. <br>
Automation does not work without internet connection. <br>
EcoFlow offers an online api, you can ask support for keys, you will get 4 values with the curl command. <br>
Controlling via app is possible without internet connection, but Delta Max hotspot is without any security/password, anyone nearby with EcoFlow app might take over the device Hotspot is not permanent. <br>
##### Automation does not work at all with latest firmware <br>

### Setup
River 600 is connected to 100W Solarpanel or Delta Max DC output.
Delta Max is connected to 300W or 400W Solarpower.
Raspberry and Router( 12V Router via USB-PD Trigger Modul) are connected to River 600 usb ports.
River 600 AC output is connected to Delta Max AC input.
Car charger cable is connected from Delta Max output to River 600 input.

### Idea
River 600 will be waked up from sun and charged, usb ports on River 600 are always on when unit is on, so Raspberry and Router are starting automatically with sun rising-> Home assistant collects data, automation is ready.
Or River 600 runs continuously and will be charged by Delta Max via DC.
Delta Max  will be waked up from sun and charged.
AC connection gives us the possibility to wake up and control the Delta Max, for example when River 600 Battery is low.

### Testing and Findings
#### Use cases and Tests with Delta Max
1) 1.8KW 50l water heater, total 1.8KWh<br>
High efficiency ~ 87%, but we think, this stresses the battery
2) Workstation, calculating with fairly linear 300Wh over 6 hours<br>
Very good efficiency ~ 85%
3) Washing Machine up to 2.2 KW, total run 0.35 Kwh<br>
We have tested with solar input, battery information useless
4) Workstation, monitor, router, between 80W and 400W very dynamic<br>
Fair efficiency ~ 60% - 80%
5) Refrigerator up to ~800 W for 1 or 2 seconds, 50W for 12 minutes, but only 12 Wh per hour<br>
Poor efficiency, DC Standby needs up to 50Wh
6) Computer 50W, continuous load<br>
Bad efficiency ~ 50%
7) Air Condition 800W<br>
We could not test yet, but we expect good efficiency

The powerful inverter is very efficient on high loads. Medium loads ~300Wh we find very good efficiency.<br>
If you have enough solar power, the efficiency is not the most important.<br>
#### Inaccurate measuring of battery percentage:<br>
1) <a href="https://github.com/fogfon/Delta-Max-Tests-and-Graphs/blob/main/README.md#nearly-linear-ac-discharging-without-input-with-a-load-of-300w-until-battery-is-empty-after-that-linear-charging-like-expected" title="0.49%">When discharging Delta Max percentage is staying very long time on 0.49%</a><br>
2) <a href="https://github.com/fogfon/Delta-Max-Tests-and-Graphs/blob/main/README.md#linear-charging-and-discharging-then-solar-charging-and-at-the-end-battery-recalibration" title="Battery Jumps">At battery recalibration, we found battery percentage jumps up to 30% up or down.</a><br>
#### Recalibration: Switch off device, press and hold usb button, then press and hold Power on, hold both for ~10s and you will see a jump... 
We thought about running the battery in between 20% and 80%, for lithium ion, we can expect more charge cycles, perhaps double, but, this means, every day one recalibration.<br>
Fan is starting when charging >= ~80W solar power (~20V), the DC/DC converter gets really hot, perhaps this is better with Solarpanels with higher Voltage.
When discharging Fan noise starts frequently >=~150W.<br>

#### Tests with River 600
1) Solarcharging to 100%, then Solarcharging and different load first AC and then ~100W DC until battery is empty.<br>
<a href="https://github.com/fogfon/River-600-Tests-and-Graphs#solarcharging-to-100-then-solarcharging-and-different-load-first-ac-and-then-100w-dc-until-battery-is-empty" title="River-600-Tests-and-Graphs">Battery jumps on linear DC discharging from 27% to 0% in seconds and switch off.</a>


### Firmware/Hardware
We got a replacement device from EcoFlow because of our findings and an audibly electrical crackling nearby AC relay. Unit arrived with 0.?.1, we had to update the firmware and we lost control. In latest firmware they closed local port what killed this project, well, perhaps it is only injured. <br>
They might have closed the port because it was not secure. We have not researched this, perhaps everybody in local network could reach and control the device.
It would have been better to secure the port instead of closing it or let the user decide, we would wish us an option in the app. <br>
When you want to control and automate the Delta Max with home assistant or any other smart home solution, THIS IS NOT POSSIBLE ANYMORE!!!<br> 
Because of this, we can not monitor our testing at the moment. After some charging and discharging in between 20% and 80%, we have done battery recalibration, a jump of 13%, from 33% to 20%. After some loads and charging and recalibration, a jump from 40% to 61%. So, it looks like, this is not solved in latest firmware. Electrical crackling nearby AC relay still is audible, so it seems to be normal. <br>
