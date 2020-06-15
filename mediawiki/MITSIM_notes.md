## Supplementary user guide for Closed-Loop

### master.mitsim

    [Link Travel Times Input File]    = {
        "eqbm_linktime.dat" # Historical travel time
        "eqbm_linktime.dat" # Updated travel time
        0x0113  # SP flags }

First file specifies link times used by unguided drivers, and the second
is for guided drivers. The third parameter is SP flags, and each bit has
a special meaning:

  - 0x0001 : if bit is set, Mitsim would use time-dependent travel times
    from link time files specified, otherwise, it uses the averaged
    travel time to guide drivers.
  - 0x0002 : if bit is set, Mitsim would calculate shortest path
    periodically, controlled by a PathStepSize parameter, or whenever it
    receives guidance (in closed loop). This applies to dynamic shortest
    path route model only.
  - 0x0004 : if bit is set, similar to above, but it applies to route
    switching models only.
  - 0x0010 : if bit is set, Mitsim expects historic and closed-loop link
    time files to be turning sensitive and would use turning-sensitive
    information to guide drivers.
  - 0x0100 : if bit is set, make guided drivers unconditionally guided
    for all periods.

<!-- end list -->

    [Time To Unblock]                 = 86400
    [Max Allowed Dynamit Delay]       = 1
    [PathStepSize]                    = 86400

Explanations:

  - \[Time To Unblock\] is the time of day after which Mitsim will start
    waiting for guidance at the end of each OD interval.
  - \[Max Allowed Dynamit Delay\] is the time in seconds allowed for
    Mitsim to run into next OD interval before it starts waiting for
    closed-loop guidance. Note: its value should be strictly less than
    OD interval length.
  - \[PathStepSize\] is the frequency (length of the period) at which
    Mitsim updates path table using its own simulated travel times.
    Note: in closed-loop if we only want Mitsim to use DynaMIT's
    guidance, we need to set this value to a sufficiently large number
    such as 86400.

<!-- end list -->

    [ClosedLoopGuidance]    = "/home/user/Bin/DynaMIT/output/closedloopguidance.out"
    [ClosedLoopToll]        = "/home/user/Bin/DynaMIT/toll.dat"
    %[OpenLoopToll]         = "toll.dat"

Explanations:

  - \[ClosedLoopGuidance\] points to DynaMIT's guidance file (generated
    by DynaMIT periodically).
  - \[ClosedLoopToll\] points to DynaMIT's toll file (optimized by
    DynaMIT periodically).
  - Note: you can specify either one of above (or both) to establish the
    closed-loop, depending on your needs.
  - \[OpenLoopToll\] is the toll file used by Mitsim itself for open
    loop run. It's recommended to be switched off (just like the example
    above) in the closed-loop setup.
  - Note: if both toll files are specified, the open-loop toll table is
    loaded first, and starting with the second OD interval, whenever
    closed-loop toll is ready, the corresponding section of the toll
    table would be overwritten by the new values.

<!-- end list -->

    [Point Sensor Step Size]          = 300
    [Area Sensor Step Size]           = 300
    [Sensor Output Flags]             = { }

Explanations:

  - Sensor step size specifies the aggregation level of sensor
    measurements. It's recommended to set it the same as OD interval
    length for ease of processing.
  - Sensor flags seem to produce addtional output to the sensor.out
    file. It's recommended to set it empty for ease of processing.