### Description:

When I increase the estimation iteration from 1 -\> 3.

DynaMIT stops with a Error.

![Error_Iterations_Estimation.png](Error_Iterations_Estimation.png
"Error_Iterations_Estimation.png")

### Solution:

The reason is not on the code. BUT, on the sensor.dat.

(1) sensor.dat starts from 8:00.

(2) simulation starts from 7:00.

(3) when running with estimation iterations, need to load in sensor
data. BUT, cannot, so error.

I change the simulation period to (8:00-11:00), so turns ok.

### Additional Progress: