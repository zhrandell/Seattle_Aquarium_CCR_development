# DVL_beam_splitter 

## Background
To capture video of a transect, the pilot tries to fly the ROV at a constant speed in a straight line 1m above the seafloor. 
The ROV has a WaterLinked [DVL-A50](https://waterlinked.github.io/dvl/dvl-a50/), which also acts as a rangefinder. 
The BlueOS DVL extension publishes the altitude in a MAVLink DISTANCE_SENSOR at ~8Hz. 
QGC can be configured to display the altitude to aid the pilot. QGC also logs this message for later analysis.

## The Problem
Rugged terrain poses difficult problems for both piloting and data analysis. 
In extreme cases the pilot may need to move the ROV up and over a 5m obstruction. 
It is difficult to keep the 1m distance to the seafloor during these maneuvers, as the leading edge of the ROV may be at a different altitude than the trailing edge. 
This affects the post-dive analysis.
The rangefinder reading in the DISTANCE_SENSOR messages is actually the average (we think) of the 4 distances reported by the 4 DVL beams. 
The DVL does show the 4 individual distances in the DVL UI (you have to dig a bit), but these distances aren't logged, so they can't be used in data analysis.

## The Proposed Solution
Build a BlueOS Extension that connects to the DVL, obtains the distances for each of the 4 beams, and publishes them as 4 additional DISTANCE_SENSOR messages.
Show all 5 distances in a simple extension UI so that the pilot can use the information to navigate.

## Next Steps
The WaterLinked BlueOS [DVL extension](https://github.com/bluerobotics/BlueOS-Water-Linked-DVL) provides an example of connecting to the DVL and sending MAVLink messages. Start by cloning this extension.

## Caveats
ArduSub only supports 1 rangefinder for each orientation, so the 4 additional messages should report different orientations.

## Extra Credit
Publish GLOBAL_VISION_POSITION_ESTIMATE messages with the output of the DVL AHRS. 
We can use this to compare the 2 different Attitude Heading Reference Systems: ArduSub's and the DVL's.
 

