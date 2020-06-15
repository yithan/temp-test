## Introduction

Dhinesh knows better on this topic

## Historical Sensor Data Collection

Dhinesh knows better on this topic

## Real-Time Sensor Data Collection

Melani knows better on this topic

## Sensor Cleaning Algorithm

### Motivation

We found many cases that the historical sensor data does not match with
the network topology."match" means the sensor counts should in most
cases, increase after an on-ramp, and decrease after on an off-ramp
(assume few incidents happened). Given an example, sensor 1 and sensor 2
are located in figure 1. There is one on-ramp between. But, in
historical sensor counts, sensor 2 always have lower value than sensor 1
(say: 80% is lower). It does not make sense and DynaMIT-R cannot
estimate traffic conditions matching such sensor counts.

The problem can be caused by 3 cases:

1.  On-ramp & Off-ramp are wrongly located in network.
2.  Sensor counts are wrongly located in network.
3.  Both (1) and (2).

In the work, I assume that the network topology (On-ramp & Off-ramp) is
correct. And then I removed some sensors, in order to remove the
miss-matching problem.It is not a perfect solution, because the best way
is to find the exact sensor location and the exact network topology. But
it is a back-up solution. I guess.

### Solution

The solution is composed by 3 steps:

If you want to know more about the algorithm, please download the
presentation: ![<File:Algorithm.pdf>](Algorithm.pdf
"File:Algorithm.pdf")

![Algorithm.png](Algorithm.png "Algorithm.png")

### Toolkit

You can download the Java code from:
![<File:OfflineSensorCleaningAlgorithm.zip>](OfflineSensorCleaningAlgorithm.zip
"File:OfflineSensorCleaningAlgorithm.zip")

The library you need to install before running the toolkit is:

1.  JDK 6.0 (check the Java version by command: java -version)

You can find 3 folders in the toolkit:

1.  inputs : you need put 6 files inside. (See the picture below)
2.  outputs : you can get the new network.dat and the new sensor.dat
    here.
3.  temp : you can get some other files, like: sensor_locations.dat.

Unzip the \*.zip and Use Java Command to execute it:

  - **java -jar OfflineSensorCleaningAlgorithm.jar**

Here, I give a example how to use the toolkit. (It is very simple)

![<File:Example.png>](Example.png "File:Example.png")

### Source Code

If you want to have more control, you have to download the source code.
I used Eclipse 3.6 as the IDE. The source code is available from:
![<File:SourceCode.zip>](SourceCode.zip "File:SourceCode.zip")