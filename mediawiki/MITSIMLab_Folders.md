## Introduction

Before go into each folder, there are some high-level guidance that can
help to understand the whole source code.

1.  The code of MITSIMLab takes the form of several individual modules
    that can be run individually or together.
2.  MITSIMLab attempts to module the action of the communication between
    Traffic Management Systems and the traffic itself (MITSIM).
3.  Beside of these 2 components, there are 3 other components:
      - MesoTS (Mesoscopic Traffic Simulator) is used by TMS to predict
        what influence the suggested guidance will have on traffic
      - MDI (MITSIMLAB/DynaMIT Interface) acts as a communicator with
        the separate program DynaMIT.
      - the module TMCA allows for the connection of MITSIMLab to
        Traffic Master Controllers, or real Traffic Management Systems,
        and act according to inputs from these controls.
4.  Finally, The 5 modules of MITSIMLab are controlled by the Simulation
    Master Controller (SMC)

## Folder Framework

1.  As said before, MITSIMLab is composed of the six modules.
2.  At the center of each module is an engine, which is based upon
    SimulationEngine, a class in Tools.
3.  Each engine has the name of a master file in it and the ability to
    set it in the method master(char). The master file is the file
    containing parameters needed for the module to run correctly.
4.  each Engine has a number of states, including OK, DONE, QUIT,
    ERROR_QUIT, etc found in the header file.
5.  In addition to running an Engine, each module, whether run alone or
    separately, either creates or uses a SimulationClock.
6.  Each module has a CmdArgsParser, which is used to parse common
    command line arguments that may be used when calling the module to
    run.
7.  The communicator, another essential part of each module, is used to
    parse arguments sent from the other modules running,

## Major Folder 1:Simulation Master Controller (SMC)

The 5 other modules of MITSIMLab are controlled by the Simulation Master
Controller (SMC).

1.  When created initially the main process of SMC does several things.
    It initializes the Toolkit, which includes basic utilities used by
    various parts of the program.
2.  It creates the SMC_Engine and loads the master file for the SMC,
    and it creates a SMC_CmdArgsParser, which parses the arguments
    which were input in the calling of the class.
3.  SMC_Interface uses Xmt and the Xmw_Interface class to create an
    interface for the SMC. It can be paused or run, and the interface,
    when in its main loop, runs the simulation of the engine.
4.  SMC_Engine when run creates an array of 5 SMC_SimlabModules, which
    are the modules that run concurrently in MITSIMLab. In order of
    index, they are MITSIM (Microscopic Traffic Simulator), TMS (Traffic
    Management Simulator), MESO (Mesoscopic Traffic Simulator), MDI
    (MITSIM/DYNAMIT Communicator), and TMCA (Traffic Management Center
    Adaptor).
5.  SMC_SimlabModule is a class that represents the modules that are
    run together in MITSIMLab. It is a subclass of IOService, the class
    which serves as a basis of communication between the modules of
    MITSIMLab.

## Major Folder 2:Traffic Management Simulator (TMS)

In the use of MITSIMLab as a simulation of the effectiveness of Traffic
Control Stations, TMS represents a simulation of the Traffic Control
Station, providing guidance for the network based on MESO simulations.

1.  Essentially when the SMC is run the TMS serves as a communicator
    between MITSIM and MESO, telling MESO to calculate the tables
    (congestion and shortest path tables) that MITSIM will use, and
    telling MITSIM when MESO is done calculating the tables and when to
    take in the tables as input.
2.  TMS also saves the best guidance created throughout the run of the
    program.
3.  To the MDI, TMS asks that it start the OD estimation and prediction.
4.  Finally it alerts SMC to the end of a cycle of simulation and
    guidance creation.

## Major Folder 3:Microscopic Traffic Simulator (TS)

1.  In the use of MITSIMLab as a simulation of the effectiveness of
    Traffic Control Stations, MITSIM is the representation of the
    traffic on the network of roads.
2.  Compared with MESO, MITSIM uses another group of files, Road
    Network, to model the Road Network found in MITSIM, as well as a
    Drawable road network to graphically display it if it is running on
    it own.
3.  MITSIM communicates through TMS to MESO which allows it to use the
    routing tables calculated by MESO.
4.  MITSIM models many significant aspects of the traffic simulation
    including: Car Following in TS_CFModels.cc, Lane Changing Model in
    TS_LCModels.cc, TS_SRModels.cc, TS_OtherModels.cc and MOE
    calculation in TS_Moe.cc (if external MOE is turned on).
5.  TS_Network is the most important class in MITSIM after the engine.
    It contains the Road Network used throughout MITSIM simulation.
6.  TS_Network calculates acceleration and lane changing status of
    vehicles in the calcVehicleStates() method, which uses the model
    classes listed above, and then moves them based on
    moveVehicles(void).
7.  The network also triggers sensors based on vehicle counts and speed,
    etc.
8.  It can also save the state of the network, send sensor readings, or
    dump sensor readings, depending on the methods called.

Since TS is the most important module in current study. More details are
explained.

### Main Function

1.  main function is in Mitsim.cc;
      - int main( int argc, char \*\*argv )
      - {
      - ::Welcome(argv\[0\]);
      - ToolKit::initialize();
      - TS_Engine engine;
      -
      - theCloParser = new TS_CmdArgsParser;
      - theCloParser-\>parse(\&argc, argv);
      -
      - engine.run(); // Run the simulation.
      - engine.quit(STATE_DONE); // Stop the simulation.
      - return 0;
      - }

### TS_Engine

TS_Engine is the class that:

1.  load in configuration files: void loadMasterFile();
2.  start the simulation: void run();
3.  simulate one time step: int simulationLoop(); //huge function
4.  init close_loop controller: closedLoopRunManager& clRunManager

### theSimulationClock

theSimulationClock controls the time unit, start_time and end_time and
current simulation time; Functions include:

1.  init(start, stop, step);
2.  advance();
3.  currentTime();
4.  delay(double nSeconds);
5.  currentClockTime();

### closedLoopRunManager

The class closedLoopRunManager is in Tools. It is responsible for
controlling progress of close loop.

1.  int checkRunStatus(std::string fileName);
2.  int checkRunStatusBlocking(std::string fileName, double startTime,
    double nowTime); //block MITSIM if too large delay
3.  int getFileLock(std::string fileName);
4.  int removeFileLock(std::string fileName);

### Route Guidance

1.  The first class is: RN_Route.
2.  inside the class, there are 2 types of routing table:
      - extern RN_Route\* theGuidedRoute;
      - extern RN_Route\* theUnGuidedRoute;
3.  There is one function is used to update travel time; It is only used
    for guided drivers;
      - updatePathTable(char \*altname = NULL, float alpha = 1.0,double
        start = 0, double stop = 0);

### tsNetwork

As mentioned before, tsNetwork is the most important class that manage
the supply side. The major functions include:

1.  guidedVehiclesUpdatePaths();
2.  calcSegmentData();
3.  calcLaneSpeeds(); //update lane speed;
4.  drawSensors(); //GUI related;
5.  tsNetwork-\>writeSensorReadings(); //output;
6.  tsNetwork-\>resetSensorReadings();
7.  tsNetwork-\>enterVehiclesIntoNetwork(); //Move vehicles from vitual
    queue into the network
8.  calcVehicleStates(); //Loop each vehicles currently in the network
9.  moveVehicles();
10. outputSegmentStatistics(); //output;
11. dumpNetworkState();
12. dumpTrajectoryRecords();

### Parameter

There are 3 classes in TS parameters:

  - ./GRN/Parameter.h: Base Parameters
  - ./TS/TS_Parameter.h: Detailed Parameters: including car following
    models, vehicle types, etc.
  - ./Tools/SimulationEngine.h: Output related configurations.

### TS_Incident

Each incident has a status, say: INCI_ACTIVE, INCI_REMOVED

1.  checkIncidents(); //loop each incident and check the status of the
    incident.

Note: list of incidents are inside class: tsNetwork

### theODTable

Inside the class, there is another class: OD_Parser。 OD_Parser is used
to load in data format in demand.dat.

There are 2 major functions:

1.  read(); // Update OD trip tables
2.  emitVehicles(); // Create vehicles based on trip tables

### theCommunicator

this class is for receive and response to other modules. Since our
research does not use TMS, do not detailed the class here.

### theInterface

the class is processing users' inputs from GUI. So, it is not detailed
explained here.

## Major Folder 4:Mesoscopic Traffic Simulator (MESO)

In the use of MITSIMLab as a simulation of the effectiveness of Traffic
Control Stations, MESO is a slightly less accurate simulation of roads
used by TMS to create the best guidance it can based on MESO simulations
of congestion.

1.  MesoTS represents vehicles in groups called Traffic Cells, which are
    updated based on the speed of the leader and follower and then
    advanced in an advance stage.
2.  Cells are created and split based on the difference in position of
    the adjacent vehicles. If they are too far apart, they split, and if
    they are too close, they merge.
3.  The slightly less accurate but quicker to run MesoTS is used by TMS
    to simulate future traffic conditions given certain route guidance.
4.  MESO_Network is used to model the network in the Mesoscopic Traffic
    Simulation. It calculates the upSpeed and dnSpeed of each “cell” of
    vehicles on the road and then advances them based on their
    individual speeds.

## Major Folder 5:MITSIM/DYNAMIT Interface (DMI)

DynaMIT is another traffic modeling software that effectively models an
entire network, including the offstreets, not just high traffic areas.
MDI uses CORBA to bind the process to Dynamit, a separately running
program.

## Major Folder 6:Traffic Management Center Adaptor (TMCA)

The traffic management center Adaptor appears to adapt MITSIMLab to
TMCs, which are the environment in which DynaMIT was initially proposed
to run inside, and which MDI attempts to simulate with DynaMIT. This is
accomplished by using CORBA to unite the processes of MITSIMLab with
TMCs.

## Other Folder 1:GRN

This folder keeps classes related with Road Network. In order to
represent the entirety of a network and be as accurate as possible, the
Road Network contains many different classes.

## Other Folder 2:DRN (Drawable Road Network)

1.  The Drawable Road Network extends the Road Network and adds drawing
    states and the ability to draw certain parts of the Road Network.
2.  It includes a method to find the nearest Road Segment to the
    pointer, a method to select nodes, edit states, etc.
3.  Essentially it is a version of the Road Network with the ability to
    be displayed on a GUI and interacted with by the user.

## Other Folder 3:IO

IO contains classes that are the basis of the communication between the
separate modules of MITSIMLab. These files include Communicator,
Exception, Message Tags, and PVM_Service.

## Other Folder 4:Tools

Tools contains a variety of classes which are used throughout the
program to simplify tasks which would otherwise be duplicated and more
difficult. It contains ArgsParser, CmdArgsParser, GenericSwitcher,
GenericVariable, Math, Normalizer, Parser, Random, Scaler,
SimlabLicense, SimulationClock, SimulationEngine, and ToolKit.

for example:

1.  The SimulationClock is the clock used in the simulation, and is only
    created once. It deals not only with the amount of time passed in
    the simulation, but also with the amount of CPU clock time used and
    whether the program is sharing the CPU with other processes or if it
    is dedicated.
2.  The SimulationEngine is a generic class used as the base class of
    all the Engines, which has a simulation loop, a quit, and other
    necessary files.

## Other Folder 5:Xmw

Xmw contains a system by which documents may be rendered in a text file
and be graphically represented, as well as files which can create data
plots and other graphical representations of data.