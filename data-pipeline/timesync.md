# Pipeline Time

## Summary

There are several clocks running on the ROV system, and timestamps are recorded several ways in the different logs.
These need to be synchronized.

## Clocks

### ArduSub Time

Internally, ArduSub has a 64-bit microsecond clock that starts when ArduSub starts.
This clock is used throughout the code for all functions, including scheduling, EKF calculations and logging.

Many (all?) of the Dataflash log messages in a BIN file contain a 64-bit `TimeUS` field that records the time when the
log message was written. For post-processing, this is the most accurate source of time.

Several MAVLink messages include a 32-bit `time_boot_ms` (millisecond) field that contains the value of the ArduSub
clock when the message was sent. When this message is received by QGroundControl or another system, it can be compared
to the laptop time, though it also includes the transmission time, so it can't be used directly.

ArduSub can send a `SYSTEM_TIME` MAVLink message with both `time_boot_ms` and `time_unix_usec` fields.
In theory this can be used to accurately synchronize clocks.

> TODO ArduSub gets the UNIX time from a GPS, or in our case, from the GPS_INPUT message from the USBL.
> Where does this time come from?

This clock resets to 0 when ArduSub reboots.
A new BIN file is created for each boot, so time is monotonic within a BIN file.
If a dive spans multiple BIN files then we will need to synchronize across all of them.

### Laptop Time

The laptop gets its time from a network timeserver whenever it is connected to the internet.
The laptop has a real-time clock, so it maintains the correct time even when it is not connected.

QGroundControl writes the laptop time in the tlog file for each MAVLink message received.
The units are microseconds from the UNIX epoch (64-bits), rounded to the nearest millisecond.
This is available in pymavlink in the following code snippet:

~~~
timestamp = getattr(msg, '_timestamp', 0.0)  # float, seconds
~~~

### Raspberry Pi (BlueOS) Time

The Raspberry Pi has no real-time clock, so if it is booted up away from the internet it will not have the correct time.
The Pi cleverly remembers the last-known time, so timestamps are monotonic, but time appears to fast-forward when
the Pi connects to a network timeserver.

> TODO Can we ignore the Raspberry Pi clock? If we use cockpit we will have to rely on the tlog files generated by
> mavlink-router, which presumably contain timestamps from the Raspberry Pi clock.

### GoPro Time(s)

TODO

## Synchronization Procedures

TODO