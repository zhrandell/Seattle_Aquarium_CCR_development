# GNSS_compass_logging

## Background
We now use Advanced Navigation's [GNSS Compass](https://www.advancednavigation.com/inertial-navigation-systems/satellite-compass/gnss-compass/) to provide topside GPS and compass heading information to the WaterLinked Underwater GPS system (UGPS).  

## The Problem
Clyde’s [wl_ugps_external_extension](https://github.com/clydemcqueen/wl_ugps_external_extension) does a fantastic job of feeding GPS and compass information from the GNSS Compass to the UGPS G2 box. 
However, no information from the GNSS Compass is retained. 
At a minimum, we would like to log the GNSS Compass’ *GPS position* (the vessel’s position) as well as the *compass heading* of the vessel. 
This will enable us to better understand the relative level of noise in those data (likely low), and on a more practical note, those topside data will enable us to consistently anchor at the same locations year-after-year when repeating these surveys. 

A step further, we also desire to log the *pitch* and *roll* values from the GNSS Compass. 
We have reason to suspect that greater vessel movement (pitching and rolling in the wind, or in response to swell) may associate with higher levels of noise in the GPS position estimates, as the acoustic receivers move around in the water relative to the ROV. 
Therefore, these values may be of interest in the future, and at a minimum, high pitch and roll values could serve as a proxy for instances where the acoustics need to be down-weighted relative to, e.g., the DVL. 

## The Proposed Solution
Modify Clyde’s wl_ugps_external_extension to additionally enable the logging of GPS, compass, pitch and roll values. 
This would be an excellent introduction to BlueOS Extensions, as one would not need to create an extension from scratch, but rather one could edit an existing extension. 
The extension currently listens for NMEA 0183 GGA and HDT messages; this will need to be extended to listen for TSS1 messages to log pitch and roll. 
Furthermore, TSS1 messages are turned off by default, so we will need to access the compass GUI to enable them. 

## Next Steps
Familiarize oneself with Clyde’s [wl_ugps_external_extension](https://github.com/clydemcqueen/wl_ugps_external_extension) as well as the GNSS Compass messages (see, e.g., [here](https://docs.advancednavigation.com/gnss-compass/Introduction.htm)).   
Once Clyde’s extension has been edited, we can set up the GNSS Compass at the Aquarium and conduct a ROV flight off of Pier 59 to test everything. 

## Caveats
The pilot will need to use the [BlueOS file browser](https://blueos.cloud/docs/blueos/1.0/advanced-usage/) to retrieve the csv file before turning off the power.	

 

