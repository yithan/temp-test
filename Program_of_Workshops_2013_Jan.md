## Claim

1.  Feel Free to change the page.
2.  Please do not share the contents with the public.

## Sensor Data

1.  Get one month (Aug, 2011) 338 sensors counts from Dhinesh.
      - sensor counts include flow, speed and density.
      - sensors are on Expressway, Singapore.
      - the exact sensor locations are unknown.
      - sensor interval is 15 minutes.
2.  In order to remove the effects of incidents, the one month sensors
    counts are aggregated (or averaged)
3.  We found that sensor flows are not consistent with each other, so we
    decided to remove inconsistent sensors.
      - The details are in the slide. ![<File:Sensor> Fusion and
        DynaMIT-R
        Calibration.pdf](Sensor_Fusion_and_DynaMIT-R_Calibration.pdf
        "File:Sensor Fusion and DynaMIT-R Calibration.pdf")
      - After running the sensor cleaning algorithms, around 210 sensors
        are left.

## Offline Calibration

1.  Lulu designed a new algorithm for off-line calibration. It is named
    W-SPSA. The details are in the paper.
2.  The first target is to calibrate OD Matrix. (373,646 time-dependent
    OD flows in one day)
      - The other parameters, like speed-density relationship and
        capacity, are coming from other projects.
      - The offline calibration period is from 00:15AM to 23:00PM.
      - The OD interval is 15 minutes. Offline calibration of 5 minutes
        is not as good as 15 minutes.
      - The weight matrix inside W-SPSA is generated using the
        free-flow-speed in the beginning, and then is generated using
        the assign matrix from DynaMIT-P.
      - The best calibrated RMSN in one day is around 0.158.
3.  The second target is to calibrate speed-density relationships. (for
    each segment)
      - Lulu modified the W-SPSA algorithm to calibrate speed-density
        relationship.
      - We found that the RMSN of speed is much better than the RMSN of
        flow. The best calibrated RMSN in one day is around 0.10.
      - We found a problem that the speed RMSN is always increasing as
        the time going.
4.  At that time, segment capacity is not calibrated.

## Online Calibration

1.  It is based on Costas's PhD Thesis
2.  It focus on online OD calibration. The OD interval is 15 minutes.
      - parameters in online calibration are calibrated using the month
        sensor data (Aug-2011).
      - Then, the prediction RMSN is calibrated based on sensor data on
        a new day. (Sep-4-2011)
3.  default parameters in online OD calibration
      - Since we have less confidence on sensor counts, the weight of
        sensors in varcov.dat file is set to be 0.25 by default. The
        weight of offline calibrated OD is set to be 1.0 by default.
      - The default depth of auto-regression in fmatrix.dat is 1 (random
        walk). The parameters in auto-regression is also set to be 1.0,
        by default.
4.  fmatrix.dat is calibrated. 6 is a reasonable choice of the depth of
    auto-regression based on the R^2 value.
5.  Based on our experience, when the depth of auto-regression changes
    from 0 to 1, there is one improvement in online prediction RMSN.
    while when the depth of auto-regression changes from 1 to 6, the
    improvement in online prediction RMSN is not obvious.
6.  weights of sensors and OD in varcov.dat are calibrated separately.
    The progress is in Costas's PhD Thesis.
7.  The files varcov.dat and fmatrix.dat are copied to Melani for online
    DynaMIT-R demonstration.
8.  Based on our experience, compared with offline OD calibration,
    Online OD calibrated is more sensitive to sensor errors.

## Others

1.  Steve proposes to use a new road network. After one week, the new
    network can not be combined efficiently. So, we decided to use the
    old network.
2.  Dhinesh proposes to use a new list of sensors. A preliminary offline
    calibration using new sensor counts gave bad offline calibration
    RMSN (around 0.35). So we decided to use the old 338 sensors.
3.  The other works from (no order) Steve, Francisco, Melani, Oren,
    Jenny, Randy, Edward are not covered in this page.