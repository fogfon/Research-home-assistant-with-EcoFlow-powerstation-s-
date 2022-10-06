# Research home assistant with EcoFlow powerstation(s)
## Testing, monitoring and controling EcoFlow Delta Max in combination with EcoFlow River 600, Raspberry PI400, TP-Link WR1043ND Freifunk and 400W solar power
### Abstract
Is it possible to run this setup stable, self-automated and self-regulated, off grid and without internet connection? <br>
In addition we have a close look at data security and privacy. <br>
We test efficiency and usability of different use cases e.g. water heating, air condition, cooling, office setup. 
This will be an ongoing report.<br>
##### Results with focus on Delta Max and AC usage
- Efficiency is up to 90% with loads ~2KWh, e.g. Water Heater
- Efficiency is ~50% with loads ~ 50Wh, e.g. low energy PC and low energy Display
- Efficiency is down to 20% with loads ~15Wh, e.g. fridge <br>

Self measurement of unit is very inexact (inaccurate). <br>
Fan is noisy. <br>
##### Security, privacy and control
EcoFlow App uses Oauth for mqtt connection, this looks very secure. <br>
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
2) Washing Machine up to 2.2 KW, total run 0.35 Kwh<br>
Good efficiency ~ 80%, only some minutes stress for battery
3) Workstation, monitor, router, between 80W and 400W very dynamic<br>
Fair efficiency ~ 60% - 80%
4) Refrigerator up to ~800 W for 1 or 2 seconds, 50W for 12 minutes, but only 12 Wh per hour<br>
Poor efficiency, DC Standby needs up to 50Wh
5) Computer 50W, continuous load<br>
Bad efficiency ~ 50%
6) Air Condition 800W<br>
We could not test yet, but we expect good efficiency

The powerful inverter is very efficient on high loads. Medium loads from 400Wh to 800Wh we find good efficiency. On lower loads, it is probably better to use the River 600. Some tests will follow. If you have enough solar power, the efficiency is not the most important.<br>
We found very inaccurate measuring of battery percentage, in Delta Max as in River 600.<br>
On Delta Max we made often battery calibration, switched off device, press and hold usb button, then press and hold Power on, hold both for 10s and you will see a battery percentage jump. Sometimes down, sometimes up, in both directions up to 20%.
We found this, because sometimes unit loads linear to 99% and then it stays there for minutes, 10 minutes and more.
When discharging percentage is staying very long time on 1% or, and this is DANGEROUS, when running a computer, it jumps from 10% to 0% within seconds.<br>
We thought about running the battery in between 20% and 80%, for lithium ion, we can expect more charge cycles, perhaps double, but, this means, every day one recalibration.<br>
Fan is starting when charging >= ~80W solar power (~20V), the DC/DC converter gets really hot, perhaps this is better with Solarpanels with higher Voltage.
When discharging Fan noise starts frequently >=~150W.

### Firmware/Hardware
We got a replacement device from EcoFlow because of our findings and an audibly electrical crackling nearby AC relay.
We can not test this like our old device, because of new firmware, unit arrived with 0.?.1, we had to update the firmware and we lost our statistics tool. After some charging and discharging in between 20% and 80%, we have done battery recalibration, a jump of 13%, from 33% to 20%. So, it looks like, this is not solved in latest firmware. Electrical crackling nearby AC relay still is audible, so it seems to be normal. <br>
In latest firmware they closed local port what killed this project, well, perhaps it is only injured. <br>
We must warn, do NOT buy EcoFlow Delta Max, when you want to control and monitor and automate it with home assistant or any other smart home solution.<br>
