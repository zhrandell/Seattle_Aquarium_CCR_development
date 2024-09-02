# ArduSub Localization Fixit

## The Problem
There are quite a few hardware and software problems that can prevent good localization, and finding and fixing these
problems requires quite a bit of knowledge or experience. Even if the pilot has sufficient knowledge and experience it 
can be time-consuming and error-prone to dig through a series of screens to isolate and resolve the problems.

Problems to watch for:
* GPS_INPUT messages are not flowing (extension is not installed, ROV is still above water, etc.)
* VISION_POSITION_DELTA messages are not flowing (extension is not installed, acoustics are turned off, etc.)
* Drive extensions are old, so GPS_INPUT and VISION_POSITION_DELTA messages may contain errors
* EKF_STATUS_REPORT reports that there is no origin
* The EKF is not configured correctly (EK3_SRCn_* parameters are not set correctly, etc.)

## The Proposed Solution
Build a BlueOS Extension that watches messages flowing on the MAVLink network, looks for problems, alerts the pilot,
and offers fixes where appropriate. The fixes may include changing ArduSub parameters.

The extension can also display interesting information during normal operation, perhaps including:
* A map showing the location of the ROV, the origin, the vessel
* EKF status and scaled innovations, e.g., is there a good horizontal position information

MAVLink messages to monitor:
* GPS_INPUT from the USBL
* VISION_POSITION_DELTA from the DVL
* EKF_STATUS_REPORT from ArduSub

Parameters to examine and possibly modify:
* EK3_SRCn_*
* Others?

## Next Steps

Look at [Surftrak Fixit](https://github.com/clydemcqueen/surftrak_fixit/).
This extension uses mavlink2rest to listen to all messages, get and set parameters, and so forth.

## Caveats

There is a [known issue where mavlink2rest will not route messages between websockets](https://github.com/mavlink/mavlink2rest/issues/93).

