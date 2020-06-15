This page presents some useful toolkits for DynaMIT project, some of
which are useful for the the preparation of DynaMIT input files, and
others are for visualisation or debugging purposes, such as SensorGUI or
PrintPathTopo. Some tools have been existed since the DynaMIT 1.0 phase,
and they were enriched during the 2.0 project. There's an older page
describing tools in DynaMIT 1.0 [here](Tools "wikilink").

## SensorGUI

Features:

  - visualise network and sensor location from "network.dat"
  - check network topology by clicking on a node to highlight the links
    connected to it
  - visualise demand from "demand.dat" (whose average value greater than
    a threshold)
  - visualise incidents from incident csv file (format based on LTA
    incident database)

### User guide

The source code of SensorGUI is under *SourceCode/Tools/SensorGUI* of
code repository. It's a Qt-based application. To build it, simple type
"make" while under this directory, and application is named
"DynaMIT_Sensor_GUI". Usage:

  - Use "Menu -\> File -\> Open Network" to open a network file for
    viewing.
  - Use "Menu -\> Demand -\> Open Demand" to open a demand file for
    visualisation.
  - Use button "Loadin Incident" to load a incident file for
    visualisation.

Sample files including "network.dat", "demand.dat", "incident.csv":
![<File:sample.zip>](sample.zip "File:sample.zip").