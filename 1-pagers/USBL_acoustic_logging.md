# USBL_acoustic_logging

## Background
Acoustic GPS systems rely upon (*1*) acoustic transmissions underwater and (*2*) a topside component on the vessel that obtains a GPS and compass heading. 
The integration of (*1*) & (*2*) generates GPS estimates of the ROV position underwater.

Unfortunately, [we found](https://discuss.bluerobotics.com/t/positioning-error-present-with-waterlinked-ugps-system/14317) WaterLinked’s Underwater GPS ([UGPS](https://waterlinked.github.io/underwater-gps/introduction/)) topside GPS and compass exhibited substantial error which propagated to our ROV positioning estimates. 
Clyde tapped into the Seattle Aquarium’s vessel to feed the Lowrance GPS and compass information to the UGPS, though [it was determined](https://www.dropbox.com/scl/fi/f9l4wlr08syb6tb8rv125/Test-results_YDEN-and-UGPS.pdf?rlkey=5kpjsey9cp8r2nfyzou0sjq8m&dl=0) the vessel’s GPS also exhibited error which was likely smoothed within a proprietary, closed off system. 
We therefore obtained Advanced Navigation’s [GNSS Compass](https://www.advancednavigation.com/inertial-navigation-systems/satellite-compass/gnss-compass/), and via Clyde’s [wl_ugps_external_extension](https://github.com/clydemcqueen/wl_ugps_external_extension), we feed GPS and compass information from the GNSS compass to the UGPS system.  

## The Problem
While the topside instability with the UGPS has been resolved, there are still instances where we want to scrutinize the underwater acoustics in more detail. 
The UGPS relies upon [x4 acoustic receivers](https://waterlinked.github.io/underwater-gps/locators/locator-d1/), though those x4 individual signals are not logged; 
only the final integrated output from (*1*) & (*2*) above are logged. 
Having the raw acoustic information would enable a better understanding of how our ROV survey parameters such as altitude above seafloor, distance from vessel, seafloor composition, etc., all affect the efficacy (and noise) of the acoustic system. 
We know there are limitations to acoustic systems (e.g., acoustic shadows), and having the raw acoustics would enable us to better understand these limitations in relation to our modes of ROV operation. 

## The Proposed Solution
Build a [BlueOS Extension](https://github.com/bluerobotics/BlueOS-Extensions-Repository) to harvest and automatically log the raw acoustic information from the UGPS extension. 
Python code to do precisely this already exists from Clyde in the form of [wl_ugps_acoustic_analysis](https://github.com/clydemcqueen/wl_ugps_acoustic_analysis), thus this project would serve as an excellent introduction to the BlueOS Extension format, and see example extensions linked [here](https://github.com/bluerobotics/BlueOS-examples) and [here](https://github.com/clydemcqueen/wl_ugps_external_extension). 
The logger should poll the WL API on the G2 box (see the existing Python script) and then write to a csv file. 
The pilot will need to use the BlueOS file browser to retrieve the csv file before turning off the power (see the BlueOS file browser [linked here](https://blueos.cloud/docs/blueos/1.0/advanced-usage/#file-browser)) 	

## Next Steps
Expand off of [wl_ugps_acoustic_analysis](https://github.com/clydemcqueen/wl_ugps_acoustic_analysis) and incorporate it into a BlueOS extension the Seattle Aquarium team can test in the field or at Pier 59. 

## Caveats
Clyde has indicated there is “a way to persist files from a BlueOS extension”, but that is largely unknown to him at this time. 
A good first task is to make sure that this is possible. 


