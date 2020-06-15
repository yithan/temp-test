## Introduction

Work has been undertaken to ensure that the existing DynaMIT-R works on
the Singapore Expressway Network. It uses a live feed of data received
from the LTA This section contains the DynaMIT-R code base and data
used. It also contains useful documentation.

The Singapore Expressway Network has been re-calibrated in October 2013.
This new recalibration includes new sensors and sensor locations - 650
in total. It also improves on the calibration of certain parameters.
Documentation on how this was done is provided below.

## Software

`Executables and parameter files for October 2013 calibration data set , i.e :`
`jRNE,DynaMIT R and P, network, supply parameters, free flow travel time, low value demand.dat, default socioEco, behavioral parameters.`
![<File:DynaMIT_exe_and_params.zip>](DynaMIT_exe_and_params.zip
"File:DynaMIT_exe_and_params.zip")

## Data: Singapore Expressway Network

**`Singapore``   ``Expressway``   ``Network:`**
`Data of the Singapore Expressway Network has been output in a variety of useful formats including SHP and CSV.  This data is provided in either:`
`WGS84: Coordinate system of GPS`
`SVY21: This is the Singapore Coordinate System and measure the number of metres North and East of a given datum.  It is easy to calculate distances between two points using this!`
`A shapefile containing all the Singapore Expressways is given below.  It is provided in two coordinate systems:`
`.`
`SVY21 - shp: `![<File:SEN_SVY21.zip>](SEN_SVY21.zip
"File:SEN_SVY21.zip")
`Singapore Expressway Network shapefile.  This is in the SVY21 coordinate system`
`.`
`SVY21 - shp: `![<File:SEN_SVY21_Individual_Expressways.zip>](SEN_SVY21_Individual_Expressways.zip
"File:SEN_SVY21_Individual_Expressways.zip")
`Singapore Expressway Network shapefile.  This is in the SVY21 coordinate system.  There is one shapefile for EACH expressway - i.e. 9 shapefiles`
`.`
`WGS84 - shp: `![<File:SEN_WGS84.zip>](SEN_WGS84.zip
"File:SEN_WGS84.zip")
`Singapore Expressway Network shapefile.  This is in the WGS84 coordinate system`
`.`
`WGS84 - SEN links CSV: `![<File:Links_SEN.txt>](Links_SEN.txt
"File:Links_SEN.txt")
`file of all links on the SEN in WGS84 coordinate system and CSV format.  The start and end point of each link is shown.  This includes slip roads for which some data is missing.`
` .`
`WGS84 - SEN expressway segment sequences: `![<File:ExpresswaySegmentSequences_20130816.txt>](ExpresswaySegmentSequences_20130816.txt
"File:ExpresswaySegmentSequences_20130816.txt")` or `![<File:ShapeFileSequences.zip>](ShapeFileSequences.zip
"File:ShapeFileSequences.zip")
`File containing the sequence of segments in each expresssway direction.  Uses WGS84 coordinate system and CSV format or shapeful.`
`.`
`Junctions on SEN - from Google Street View: `![<File:shapefile_junctions_sen.zip>](shapefile_junctions_sen.zip
"File:shapefile_junctions_sen.zip")
`File containing a series of 4 shapefiles showing the junctions on the expressway: all junctions, on-ramps, off-ramps, sequence of junctions on each direction of expressway.  Data in WGS84 format`

**`Singapore``   ``Road``   ``Network``   ``-``   ``urban``
 ``roads:`**
`The following file contains the shape file for the complete Singapore Road Network.  This is in WGS84 / UTM Zone 84 format (ESPG 32648).  This is NOT SVY21`
![<File:Singapore>`   ``Road``
 ``Network.zip`](Singapore_Road_Network.zip
"File:Singapore Road Network.zip")
`.`
`The following file contains the shape file for the complete Singapore Road Network.  This is in WGS84 format`
![<File:Singapore>`   ``Road``   ``Network``
 ``WGS84.zip`](Singapore_Road_Network_WGS84.zip
"File:Singapore Road Network WGS84.zip")
`.`
`The following file contains the CSV files for the complete Singapore Road Network.  There is a "nodes" file and a "links" file.  This is in WGS84 format`
![<File:WGS84_CSV.zip>](WGS84_CSV.zip "File:WGS84_CSV.zip")

### LTA road network data, January 2014

`The following file contains the LTA road data set of January 2014, including the new Marina Coastal Expressway, MCE: `![<File:ROAD_LTA_SEGMENT_START_END_NODE_DECEMBER_2013.zip>](ROAD_LTA_SEGMENT_START_END_NODE_DECEMBER_2013.zip
"File:ROAD_LTA_SEGMENT_START_END_NODE_DECEMBER_2013.zip")
`Shapefile of the LTA network is here: `![<File:LTA_map_shapefile_january_2014.zip>](LTA_map_shapefile_january_2014.zip
"File:LTA_map_shapefile_january_2014.zip")
`Mapping from LTA to Aimsun is here:  `![<File:AIMSUN_to_LTA.xlsx>](AIMSUN_to_LTA.xlsx
"File:AIMSUN_to_LTA.xlsx")

### Sensor Locations

`.`
`The following file contains the truth coordinates of sensors on the BKE, KJE, and PIE in SVY21 format: `![<File:Detector>`
 ``Location``
 ``(PIE,KJE,BKE).xlsx`](Detector_Location_\(PIE,KJE,BKE\).xlsx
"File:Detector Location (PIE,KJE,BKE).xlsx")
`.`
`These sensor locations have been mapped to Aimsun segments, with comments by Oren Lederman: `![<File:Detector_location_aimsun_validation.xlsx>](Detector_location_aimsun_validation.xlsx
"File:Detector_location_aimsun_validation.xlsx")

## Data: DynaMIT format

**`Network``   ``Data`**
`.`
`This contains the DynaMIT network.dat file`
![<File:network.zip>](network.zip "File:network.zip")

**`Calibration``   ``Data``   ``-``   ``26th``   ``November``
 ``2013`**
`.`
`This contains calibration data from July 2013 with 650 sensors:`
`.`
`1. DynaMIT Sensor.dat data: `![<File:sensor_dat_20131126.zip>](sensor_dat_20131126.zip
"File:sensor_dat_20131126.zip")
`2. Matlab CountVector Data: `![<File:CountVector_20131126.zip>](CountVector_20131126.zip
"File:CountVector_20131126.zip")
`3. Erroneous Sensor List: `![<File:July_650_ErrSensors.zip>](July_650_ErrSensors.zip
"File:July_650_ErrSensors.zip")

`Sensor files for October 2013 data set.`
`Contains speed data, flow data for calibration in dynaMIT and matlab format.`
![<File:Sensor_July2013.zip>](Sensor_July2013.zip
"File:Sensor_July2013.zip")
![<File:incidents_july_2013.zip>](incidents_july_2013.zip
"File:incidents_july_2013.zip")

## Singapore Expressway Demo

  -   - THIS WILL BE ADDED SHORTELY \*\*\*

`A guide to running the demo can be found below.  This was written by Melani Jayasuriya:`
![<File:DynaMIT_LiveDemoSetup.pdf>](DynaMIT_LiveDemoSetup.pdf
"File:DynaMIT_LiveDemoSetup.pdf")

## Calibrating the Singapore Expressway Network

This section describes how the Singapore Expressway Network was
calibrated.

**`supplyparam.dat`**
`See attached document: `![<File:determining_supply_parameters_20131108.docx>](determining_supply_parameters_20131108.docx
"File:determining_supply_parameters_20131108.docx")

## Golden Triangle: Test Network

The Golden Triangle refers to the sections of road marked by the BKE,
KJE, and PIE. It is around 10 times smaller than the main Singapore
Expressway Network so is ideal for testing new calibration algorithms.

### Current Version

`Version: 24th June 2014`
`Changes: 1. New sensor data from June 2014. 2. network.dat had wrong speeds`
`DynaMIT static and sensor files: `![`File:``
 ``GT_dynamit_initial_20140624.zip`](_GT_dynamit_initial_20140624.zip
"File: GT_dynamit_initial_20140624.zip")
`Unzip to get static, sensor, and incident files in a format compatable with the Calibration toolbox.  NB. the number of incident files has to match the number of sensor files used for calibration`
`.`
`Four demand files have been created:`
`a. 6 OD high-medium demand, 6 OD low demand.  The 6 ODs represent the ODs between the superloaders - i.e. the points on the PIE and SLE where the Golden Triangle was cut from the rest of the expressway`
`b. 154 OD high-medium demand, 154 OD low demand.  The 154 ODs represent ODs between the superloaders and ODs from each superloader to each loader.  There must be at least 6 sensors on all paths to be included`
`.`
`Shapefile of segments, nodes, sensors, loaders in WGS84: `![<File:map_golden_triangle_20140314.zip>](map_golden_triangle_20140314.zip
"File:map_golden_triangle_20140314.zip")
`Other lookup tables, i.e. sensor id to Aimsun id, Aimsun id to LTA id: `![<File:mapping_tables_20140507.zip>](mapping_tables_20140507.zip
"File:mapping_tables_20140507.zip")

### Old versions

`Version: 7th May 2014`
`Changes: 1. Corrected a small mistake in network.dat.`
`DynaMIT static files: `![<File:GT_static_data_20140507.zip>](GT_static_data_20140507.zip
"File:GT_static_data_20140507.zip")
`DynaMIT sensor.dat files: `![<File:GT_sensor_data_July_2013_20140314.zip>](GT_sensor_data_July_2013_20140314.zip
"File:GT_sensor_data_July_2013_20140314.zip")
`Shapefile of segments, nodes, sensors, loaders in WGS84: `![<File:map_golden_triangle_20140314.zip>](map_golden_triangle_20140314.zip
"File:map_golden_triangle_20140314.zip")
`Other lookup tables, i.e. sensor id to Aimsun id, Aimsun id to LTA id: `![<File:mapping_tables_20140507.zip>](mapping_tables_20140507.zip
"File:mapping_tables_20140507.zip")

`Version: 14th March 2014`
`Changes: 1. Corrected a small mistake in network.dat.   2. Minimum speed for all segments now 36kph.   3. Made all inconsistent sensors have a flow of -1`
`DynaMIT static files: `![<File:GT_static_data_20140314.zip>](GT_static_data_20140314.zip
"File:GT_static_data_20140314.zip")
`DynaMIT sensor.dat files: `![<File:GT_sensor_data_July_2013_20140314.zip>](GT_sensor_data_July_2013_20140314.zip
"File:GT_sensor_data_July_2013_20140314.zip")
`Shapefile of segments, nodes, sensors, loaders in WGS84: `![<File:map_golden_triangle_20140314.zip>](map_golden_triangle_20140314.zip
"File:map_golden_triangle_20140314.zip")

`Version: 27th January 2014`
`Changes: updated sensor locations`
`DynaMIT static files: `![<File:Golden_Triangle_DynaMIT_20140127.zip>](Golden_Triangle_DynaMIT_20140127.zip
"File:Golden_Triangle_DynaMIT_20140127.zip")
`DynaMIT sensor.dat files: `![<File:GT_Network_Sensor_July_2013_20140127.zip>](GT_Network_Sensor_July_2013_20140127.zip
"File:GT_Network_Sensor_July_2013_20140127.zip")
`Shapefile in WGS84: `![<File:Golden_Triangle_Network_Shapefile_20140115.zip>](Golden_Triangle_Network_Shapefile_20140115.zip
"File:Golden_Triangle_Network_Shapefile_20140115.zip")

`Version: 17th January 2014:`
`Problem - sensor locations are not wholly correct`
`DynaMIT static files: `![<File:Golden_Triangle_DynaMIT_20140117.zip>](Golden_Triangle_DynaMIT_20140117.zip
"File:Golden_Triangle_DynaMIT_20140117.zip")
`DynaMIT sensor.dat files: `![<File:GoldenTriangle_SensorData_20140115.zip>](GoldenTriangle_SensorData_20140115.zip
"File:GoldenTriangle_SensorData_20140115.zip")
`Shapefile in WGS84: `![<File:Golden_Triangle_Network_Shapefile_20140115.zip>](Golden_Triangle_Network_Shapefile_20140115.zip
"File:Golden_Triangle_Network_Shapefile_20140115.zip")

**`Version:``   ``15th``   ``January``   ``2014`**
`Problem - sensor locations are not wholly correct`
`DynaMIT static files: `![<File:Golden_Triangle_DynaMIT_20140114.zip>](Golden_Triangle_DynaMIT_20140114.zip
"File:Golden_Triangle_DynaMIT_20140114.zip")
`DynaMIT sensor.dat files: `![<File:GoldenTriangle_SensorData_20140115.zip>](GoldenTriangle_SensorData_20140115.zip
"File:GoldenTriangle_SensorData_20140115.zip")
`Shapefile in WGS84: `![<File:Golden_Triangle_Network_Shapefile_20140115.zip>](Golden_Triangle_Network_Shapefile_20140115.zip
"File:Golden_Triangle_Network_Shapefile_20140115.zip")

## Documents

### Real time data from the LTA

Real Time Data push informtion from the LTA. This is confidential and is
therefore stored in a password protected zip file. The password is
d\*\*\*\*\*t123 ;-) ![<File:DissemPushService>
v1.11.2.zip](DissemPushService_v1.11.2.zip
"File:DissemPushService v1.11.2.zip")

The approach to processing and cleaning LTA sensor data is described in
the following document:
![<File:LTA_data_DynaMIT_process_20140211.docx>](LTA_data_DynaMIT_process_20140211.docx
"File:LTA_data_DynaMIT_process_20140211.docx")

### Data cleaning process of real time flow and incident data

The approach to handling incident data is described in the following
document: ![<File:Incident> Feed to DynaMIT
20130405.docx](Incident_Feed_to_DynaMIT_20130405.docx
"File:Incident Feed to DynaMIT 20130405.docx")

One of the issues that has been faced is that the LTA provide flow data
for all links - even those without sensors on them. The following
document descibes the approach NTU took to identify links with sensors
on them: ![<File:Detection> of Sensor locations in
Expressways_byDistance.docx](Detection_of_Sensor_locations_in_Expressways_byDistance.docx
"File:Detection of Sensor locations in Expressways_byDistance.docx")

The NTU methodology for identifying errouneous sensor data is described
in the following document: ![<File:NTU> - spatial consistency for
assessing the accuracy of traffic data -
2013.pdf](NTU_-_spatial_consistency_for_assessing_the_accuracy_of_traffic_data_-_2013.pdf
"File:NTU - spatial consistency for assessing the accuracy of traffic data - 2013.pdf")

NTU have also written a literature review on cleaning erroneous sensor
data here:
![<File:TrafficData_QC_Survey_Draft_1.docx>](TrafficData_QC_Survey_Draft_1.docx
"File:TrafficData_QC_Survey_Draft_1.docx")

### Flow data from the LTA

Flow data used on the Singapore Expressway Network comes from camera
based data. This is discussed in detail in the following document: Mak
Chin Long (2002) "New Dual-Variable algorithms for detecting
lane-blocking incidents on expressways", PhD at Nanyang Technological
University ![<File:CEE-THESES_196.pdf>](CEE-THESES_196.pdf
"File:CEE-THESES_196.pdf")

## References

This section contains useful refernece material when working with the
Singapore Expressway Network

`Mak Chin Long (2002) "New Dual-Variabl Algorithms for detecting lane blocking incidents", PhD thesis, NTU`
`This PhD thesis uses Singapore LTA sensor data from expressways to detect incidents.  It describes the sensor data and issues in section 4`
![<File:CEE-THESES_196.pdf>](CEE-THESES_196.pdf
"File:CEE-THESES_196.pdf")