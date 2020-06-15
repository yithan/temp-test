Some general information about DynaMIT Offline Calibration in 2012.

  - Network: Singapore Expressway
  - OD Interval: 15 mins
  - Raw Data: Sensor Flows in Step, 2011
  - OD Pairs: 4106
  - Period: 00:15:00 - 23:00:00
  - best RMSN: 0.16

In some conditions, you may want to re-create the same off-line
calibration process. Here is a tutoriual to show you how to do it.

### Data Download

You need to download the folder below: (Note the folder contains also
all the calibrated results and internal files, like Sim\*.dat and
link_tt.dat)

<https://drive.google.com/file/d/0B6HnyAz4xRpiOHh2c2poM0Z1UjQ/edit?usp=sharing>

### DynaMIT Sourcecode Download and Compile

There is an already-compiled DynaMIT-P (executable file) in the folder
you downloaded. The DynaMIT-P was compiled on Ubuntu 12.04 (32 bit). If
you can direcly execute it. You can skip this step.

Otherwise, Go to here: [Tutorial](Tutorial "wikilink"), compile DynaMIT
and copy DynaMIT-P to the calibration folder (inside the folder
"DynaMIT")

### Install Octave

Octave is similiar to Matlab. you can download using the command:

  - sudo apt-get install octave

After installing octave, you can run matlab code using:

  - octave MATLAB_CODE.m

### Start Calibration

  - Go to: PATH/To/CALIBRATION/
  - Start Calibration using command:
      - octave NewAlgorithm.m

### Compare the RMSN results with the correct RMSN Results

If the results are the same with the correct RMSN results below,
CCCongraulations\! you have succeed to run a really complex algorithm.

-----

The correct fn_RMSN.dat

-----

`1.00000000e+00 2.31788542e-01`
`2.00000000e+00 3.58899676e-01`
`3.00000000e+00 3.51568636e-01`
`4.00000000e+00 2.01633371e-01`
`5.00000000e+00 2.34464996e-01`
`6.00000000e+00 2.76655159e-01`
`7.00000000e+00 1.64827796e-01`
`8.00000000e+00 2.51659158e-01`
`9.00000000e+00 2.20492714e-01`
`1.00000000e+01 1.61699909e-01`
`1.10000000e+01 2.21487933e-01`
`1.20000000e+01 1.92788697e-01`
`1.30000000e+01 1.60653335e-01`
`1.40000000e+01 2.15567688e-01`
`1.50000000e+01 1.88816325e-01`
`1.60000000e+01 1.60465063e-01`

-----

### Other Calibration Results

  - Original Sensor File:
  - Sim\* Files: