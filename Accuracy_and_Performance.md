DynaMIT-R is designed to support high-accuracy real-time short-term
traffic prediction with high-performance.

High accuracy means the difference between the predictions (flow, speed,
density, travel time, etc) and the surveillance data is small.

  - In order to guarantee high accuracy, we need:
    1.  Accurate Road Network,
    2.  Accurate Historical & Real-Time Traffic Data (currently, we
        focus on "sensor" counts) [Read More Sensor
        Data](Read_More_Sensor_Data "wikilink")
    3.  Accurate Calibration to configure large number of parameters in
        various models in DynaMIT-R
    4.  Accurate Estimation of Traffic condition in previous intervals.
        (The key is OD estimation)
    5.  Accurate Prediction of Traffic condition in future
        intervals.(The key is OD prediction)
    6.  Accurate Represent of Traffic Incidents in DynaMIT-R. (under
        research)

<!-- end list -->

  - In order to guarantee high performance, we need:
    1.  High performance machines
    2.  High speed network
    3.  Number of OD pairs and number of sensors
    4.  DynaMIT-R Parameters Setting
    5.  Load Balance Algorithm (if use many machines)
    6.  New (on-line) OD Estimation algorithm (current Matlab code is
        time costly)
    7.  Multi-thread. (if we need many cores)