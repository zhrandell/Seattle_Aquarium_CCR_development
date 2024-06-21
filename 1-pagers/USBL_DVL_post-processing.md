# USBL_DVL_post-processing

## Background
ROV positioning---tracking the location of the ROV---is challenging, as typical GPS reception is not tenable underwater. 
We employ at WaterLinked USBL system that uses acoustic receivers beneath the vessel to triangulate the ROV's position, given the presence of an acoustic transmitter on the ROV. 
(And see [here](https://github.com/zhrandell/Seattle_Aquarium_CCR_development/blob/main/1-pagers/USBL_acoustic_logging.md) for more information about this USBL system). 

Unfortunately, the USBL system is rather noisy, i.e., it exhibits substantial fine-scale error (~ <2m), but occasionally larger jumps (>20m).
The strength of the USBL however its world frame - in general, it does a fairly good job at attributing the ROV to a set of latitude/longitude coordinates.

In contrast, the [DVL-A50](https://waterlinked.github.io/dvl/dvl-a50/) lacks a world frame, but provides very smooth metrics of displacement as the ROV moves across the seafloor.
It however is subject to drift, and the doppler effect DVLs utilize are notoriously poor at tracking yaw (ROV rotation about the z axis). 

See, for example, the image below, taken 6/21/2024 while the ROV flew directly above a 100m transect tape deployed by divers 
The ROV flew out along the tape - from the 0m end of the tape to the 100m, then back from the 100m -> 0m.
(thus, the two passes of the ROV's tracking should be more-or-less directly atop one another).  
1. the squiggly black line is from the USBL system with its near-ubiquitous fine-scale noise, and several larger erroneous jumps. 
2. the red line is from the DVL - its smooth path accurately tracks the *relative* movement of the ROV, though the yaw is off slightly off (the red line should overlay atop the black line). Furthermore, upon rotating the ROV around at the 100m end of the tape to return to the vessel, the DVL became confused and thought the ROV was heading in a different direction, hence the non-overlap between the two red lines. 

## The Problem
We want to plot our ROV surveys more accurately that either the USBL or DVL are capable of individually. 
We therefore want to post-process these data streams to calculate a revised trackline for any given ROV survey. 

## The Proposed Solution
There are likely a variety of analytical options available, including running a relatively simple EKF.

## Next Steps
All the necessary data from the USBL and DVL are contained in the ROV's TLOG. 
An example TLOG can be found here. 
Furthermore, Python code to access TLOGs can be found here. 

## Caveats

## Extra credit 

