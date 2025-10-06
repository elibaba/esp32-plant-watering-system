# esp32-plant-watering-system
A simple esphome based plant watering system

# Background
I have several plants in my porch that require constant watering, and I got tired from doing this manually, so here comes esphome to the rescue!

This uses a pretty simple setup:

* ESP32-Vroom with GPIO33 controlling a 1-gang relay
* A 12V submerged water pump, currently inside a 10L water bucket, but can be of course in any container you wish (ideally with a lid)
* A 12VDC power supply to power the pump and the ESP32
* A buck converter to step down 12V DC to 5V DC in order to power the ESP32 
* A hall flow meter to sense the water flow rate
* A garden watering hardware kit from Aliexpress
* A mains plug + wire to connect to the 12V power supply
* A breadboard to house the ESP32 and the voltage converter

# Switches
* The Esphome config exploses the following the the HA frontend:
  * watering_system_pump : a switch to turn the pump on/off
  * watering_system_reset_daily_water_usage  : a switch to reset the daily amount, in case I need that

# Sensors
* watering_system_water_flow_rate : Flow rate in L/Min, also can be used to detect if there no water in the bucket (e.g rate below 0.1 for 30 seconds or more)
* watering_system_daily_water_usage : Total amount of liters per day, resets at midnight

# Wiring
* Connect the mains plug wire to the AC inputs of the power supply.
* Connect the earth and black leads of the pump into earch and Minus (-) of the power supply.
* Connct the red wire from the pump to the NC contact of the relay.
* Connect another red wire from the Plus (+) output of the power supply to the COM contact of the relay. Now if the relay is turned on, 12V power flows from COM to NC (normally closed) and powers the pump.
* Connect another pair of black/red leads from the 12V outputs of the power supply into the inputs of the buck voltage converter.
* Connect a pair of leads from the 5V outputs of the voltage converter into the VIN (can be called also 5V) and GND pins of the ESP32, this now powers the ESP32.
* Connect the relay ground to the ESP32 ground
* Connect the relay VIN to the ESP32 V+
* Connect your ESP32 chosen control pin (mine is GPIO33) to the relay control pin
* Connect the flow meter poitive and negative wires similarly, while connecting it's yellow pulse sensor wire to a different GPIO pin for sensing (I am using GPIO32)
* Connect the tubing, drippers and inline the flow meter in the main tube, not to far from the pump.
* Submerge the pump in a bucket of water.
* Add the esp32 to your home assistant and configure a card if you with (see card.yaml)
* Configure automations for watering at your favourite intervals and for stopping the pump if the rate is too low for some time, which might indicate the bucket is empty of water. I have a notification sent to me in the case. You can also integrate with weather sensors and stop watering if it rains, or if the soil is too damp (with appropriate soil sensors).
* Profit and watch your beutiful plants grow with automating wateting!





