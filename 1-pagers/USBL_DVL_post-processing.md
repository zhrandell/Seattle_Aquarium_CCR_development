# *draft*_USBL_DVL_post-processing

## Background
ROV positioning -- tracking the location of the ROV -- is a substantial challenge, as GPS reception is not tenable underwater. 
We employ a WaterLinked USBL system that uses acoustic receivers beneath the vessel to triangulate the ROV's position, given the presence of an acoustic transmitter on the ROV. 
(see [here](https://github.com/zhrandell/Seattle_Aquarium_CCR_development/blob/main/1-pagers/USBL_acoustic_logging.md) for more information/links about this USBL system). 

Unfortunately, the USBL system is rather noisy, i.e., it exhibits substantial fine-scale error (~ <2m), and occasional larger jumps (>20m).
The strength of the USBL however is its world frame -- in general, it does a fairly good job at attributing the ROV to a (noisy) set of latitude/longitude coordinates.

In contrast, the [DVL-A50](https://waterlinked.github.io/dvl/dvl-a50/) lacks a world frame, but provides very smooth metrics of ROV displacement as it moves across the seafloor.
The DVL however is subject to drift, and the doppler effect DVLs utilize are notoriously poor at tracking yaw (ROV rotation about the z-axis). 

See, for example, the image below, taken 6/21/2024 while the ROV flew directly above a 100m transect tape deployed by divers. 
The ROV flew out along the tape - from the 0m end of the tape (the more northerly end) to the 100m (to the south south-east), then back from the 100m -> 0m.
Thus, the two passes of the ROV's tracking should be more-or-less directly atop one another. 

The squiggly black line is from the USBL system with its decent location tracking, but near-ubiquitous fine-scale noise (and several larger erroneous jumps).

The red line is from the DVL - its smooth path accurately tracks the *relative* movement of the ROV, though the yaw is slightly off (the red line should overlay atop the black line). 
Furthermore, upon rotating the ROV around at the 100m end of the transect tape to return to the vessel, the DVL became confused and thought the ROV was heading in a different direction, hence the non-overlap between the two red lines. 

![DVL_USBL](https://github.com/zhrandell/Seattle_Aquarium_CCR_development/assets/49246458/e71ef7ac-deb5-468d-bf2d-4a8a59efaee8)

## The Problem
We want to plot our ROV surveys after-the-fact more accurately than either the USBL or DVL are capable of individually. 
We therefore want to post-process these data streams to calculate a revised trackline for any given ROV survey. 

## The Proposed Solution
There are likely a variety of analytical options available, including running a relatively simple EKF.

## Next Steps
All the necessary data from the USBL and DVL are contained in the ROV's TLOG. 
An example TLOG can be found [here](https://www.dropbox.com/scl/fo/4t5c2jr2la2w4hdx15zzx/AIpZHlauJyygAiNhgufH6mU?rlkey=6mcu34evuvo19no5vebd5yqar&dl=0). 
Furthermore, Python code to access TLOGs can be found [here](https://github.com/clydemcqueen/ardusub_log_tools). 

## Caveats

## Extra credit 

