Welcome to Source Code of DynaMIT-R. Hopefully this Wiki can help you to
understand what is happening inside DynaMIT-R. Before you start to read
the Wiki, we suggest you to first read the Framework section, in order
to get the whole idea of the design of DynaMIT-R.

`A `**`DynaMIT``   ``developers``
 ``guide`**` has been written.  Although it is slighly out-of-date it is a very useful resource for understanding the code in more detail: `![<File:DynaMIT_Programmer_Guide_Aug2002.pdf>](DynaMIT_Programmer_Guide_Aug2002.pdf
"File:DynaMIT_Programmer_Guide_Aug2002.pdf")

Note that, you can not get more information about the structure from the
source code. The source code is only for you to better understand the
implementation of DynaMIT-R, so that you know how to modify some parts
of the source code, in order to improve DynaMIT-R.

**`DynaMIT``   ``source``
 ``code`**` is available from GIT server.  More details from the link: `[`dynamit_git`](dynamit_git "wikilink")

This section contains 3 parts:

  - **Code Structure**. This part explain all the folders and the
    relationship of these folders.
  - **Flow Chart Diagram**. This part explains the flow chart of key
    functions in DynaMIT-R, including OD Estimation, OD Prediction,
    Incident Processing, etc.
  - **Key Classes**. Some examples are dtaAssignMatrix, dtaODMatrix,
    etc.

Note: the wiki is under development, so if you find something wrong
please provide changes and comments.

## Code Structure

### **Step 1**: The 12 folders in DynaMIT (Source Code version 1).

1.  3rdparty:
      - There are 2 open-source software used in DynaMIT
      - One is METIS, it is used for road network partitioning for
        distributed version. you can read more
        from:<http://glaros.dtc.umn.edu/gkhome/metis/metis/download>
      - The other is TNT Sparse Matrix, it is used for processing large
        number matrix. you can read more from:
        <http://math.nist.gov/tnt/overview.html>
2.  components:
      - This is one of the most important folders. There are 23
        components inside this folder.
      - Examples include: Parameters, NewPathTopology, SimulatedDensity,
        Surveillance, SocioEcoData, etc. You can guess the functions by
        the name.
      - There are also some components, which does not have a
        easy-to-guess name, like: NewListOfPackets,
        ClosedLoopRunManager, ImpedanceTables. For these cases, the
        components might have been used for many different conditions,
        so do not have a clear name. If you want to know more about the
        folders. You have to read the source code.
3.  DynaMIT:
      - There are only 2 files inside.
      - One is DynaMIT.cc, which controls the logic of DynaMIT-R.
      - The other is DynaMIT_MPI.cc, which controls the logic of
        DynaMIT-R Distributed version.
4.  DynaMIT-P:
      - There are only 2 files inside.
      - One is DynaMIT_P.cc, which controls the logic of DynaMIT-P.
      - The other is DynaMIT_Pmpi.cc, which controls the logic of
        DynaMIT-P Distributed version.
5.  etc:
      - This folder contains the environment setting files.
      - Suggest you not changing anything in this folder. Otherwise, it
        may cause DynaMIT not working.
6.  include:
      - This folder contains the basic setting of variables and
        functions used inside DynaMIT.
      - One example: idlODType defines what is included inside one OD
        element.
      - Another example: dtaPointer defines what functions should be
        included inside a point.
7.  MatlabEstimateOD:
      - This folder contains the Matlab Code to execute "OD Estimation".
      - Note 1: this folder is only part of "OD Estimation".
      - Note 2: this folder is pre-compiled. So, if you only change the
        estimateOD.m, the changes will not be reflected inside the new
        source code. (reported by Lulu)
8.  MCR:
      - This folder contains everything that required to execute Matlab
        Source Code.
      - You need to configure the MCR. (If you want to run Matlab Source
        Code)
9.  modules:
      - This is one of the most important folders. There are 7 modules
        inside this folder.
      - Examples include: ATMS, Supply, PreTripDemand, Guidance.
10. processes:
      - This is one of the most important folders. **If you want to
        modify the source code, you have to understand what happened in
        this folder**.
      - There are 2 parts inside this folder.
      - One is Estimation.
      - The other is PredictionGuidance.
11. Tools:
      - This folder contains 6 tools.These tools are used outside of
        DynaMIT.
      - Examples include: (1) CreateGraph4METIS, which is used to test
        route network decomposition algorithm. (2) PrintPathTopoUserID,
        which is used to change the format of candidate routes into
        use-friendly format.
12. utils:
      - This folder contains small fucntions, which are used inside
        DynaMIT.
      - Examples include: string processing and time processing.

### **Step 2**: Relationship of the 12 folders in DynaMIT (version 1).

1.  The major relationship is shown in the figure below. (*Click twice
    to see the clear figures*)
2.  MatlabEstimateOD is called by modules/PreTripDemand, which is not
    shown in the figure.
3.  Tools are not shown also in the figure, because these tools are
    executed outside of DynaMIT.

![<File:Relationship_of_folders.png>](Relationship_of_folders.png
"File:Relationship_of_folders.png")

### **Step 3**: Some Notes (version 1).

1.  the source code has been always changed by many PhD & Master
    students. While the manual might not updated frequently. So, it is
    important to check whether the theory has been implemented inside
    the source code.
2.  CORBA has been removed from DynaMIT, instead, we use MPI now. (like:
    OpenMPI & MPICH)

\[One old introduction from Rama Balakrishna @ 2012 is available here:
![<File:DynaMIT.pptx>](DynaMIT.pptx "File:DynaMIT.pptx")\]

## Source Code Flow Chart Diagram

There are some difference between the source code and the state-of-art
theory. We will try to mention the difference, so that you can have a
right expectation of the outputs of DynaMIT. Note: some of them are not
exactly flow chart diagram. It can be a formula or a paper, if the flow
chart diagram can be messy.

### DynaMIT-P

It is included primarily for calibration purpose.

[DynaMIT-P Flow Chart](DynaMIT-P_Flow_Chart "wikilink")

### DynaMIT-R

TBD

### Off-line Calibration

1.  State-of-Art Theory: ![<File:PhD> Thesis of Ramachandran - Off-line
    Calibration of Dynamic Traffic Assignment
    Models.pdf](PhD_Thesis_of_Ramachandran_-_Off-line_Calibration_of_Dynamic_Traffic_Assignment_Models.pdf
    "File:PhD Thesis of Ramachandran - Off-line Calibration of Dynamic Traffic Assignment Models.pdf")
2.  SPSA by Lulu: ![File: Off-line Calibration in
    DynaMIT-R.pdf](_Off-line_Calibration_in_DynaMIT-R.pdf
    "File: Off-line Calibration in DynaMIT-R.pdf") and ![File: using
    SPSA on Singapore
    Expressway.pdf](_using_SPSA_on_Singapore_Expressway.pdf
    "File: using SPSA on Singapore Expressway.pdf")
3.  W-SPSA by Lulu:

### On-line Calibration

1.  State-of-Art Theory: ![<File:PhD> Thesis of Costas - On-line
    Calibration for Dynamic Traffic
    Assignment.pdf](PhD_Thesis_of_Costas_-_On-line_Calibration_for_Dynamic_Traffic_Assignment.pdf
    "File:PhD Thesis of Costas - On-line Calibration for Dynamic Traffic Assignment.pdf")
2.  Implementation in DynaMIT-R: ![<File:OD> Estimation in
    DynaMIT-R.pdf](OD_Estimation_in_DynaMIT-R.pdf
    "File:OD Estimation in DynaMIT-R.pdf")

### OD Estimation

1.  State-of-Art Theory: ![<File:OD> Estimation
    Theory.pdf](OD_Estimation_Theory.pdf
    "File:OD Estimation Theory.pdf")
2.  Implementation in DynaMIT-R: ![<File:OD> Estimation in
    DynaMIT-R.pdf](OD_Estimation_in_DynaMIT-R.pdf
    "File:OD Estimation in DynaMIT-R.pdf")

### OD Prediction

1.  State-of-Art Theory: (in the same file as OD Estimation) ![<File:OD>
    Estimation Theory.pdf](OD_Estimation_Theory.pdf
    "File:OD Estimation Theory.pdf")
2.  Implementation in DynaMIT-R: TBA

### AutoRegression

1.  State-of-Art Theory: It is also explained in Costas's PhD Thesis
    ![<File:PhD> Thesis of Costas - On-line Calibration for Dynamic
    Traffic
    Assignment.pdf](PhD_Thesis_of_Costas_-_On-line_Calibration_for_Dynamic_Traffic_Assignment.pdf
    "File:PhD Thesis of Costas - On-line Calibration for Dynamic Traffic Assignment.pdf")
2.  Implementation in DynaMIT-R:

### Speed-Density Relationship

1.  Please check section 10.1.8 in user guider
    [Materials](Materials "wikilink"), DynaMIT has implemented exactly
    the same thing mentioned inside the user guider.

### Capacity and Package Sorting

1.  Implementation in DynaMIT-R:

### Guidance and VMS

1.  State-of-Art Theory: ![<File:PhD> Thesis of Jon - Consistent
    Anticipatory Route
    Guidance.pdf](PhD_Thesis_of_Jon_-_Consistent_Anticipatory_Route_Guidance.pdf
    "File:PhD Thesis of Jon - Consistent Anticipatory Route Guidance.pdf")
    and ![<File:Master> Thesis of Vaibhav - Assessment of Impact of
    Dynamic Route Guidance through Variable Message
    Signs.pdf](Master_Thesis_of_Vaibhav_-_Assessment_of_Impact_of_Dynamic_Route_Guidance_through_Variable_Message_Signs.pdf
    "File:Master Thesis of Vaibhav - Assessment of Impact of Dynamic Route Guidance through Variable Message Signs.pdf")
2.  Implementation in DynaMIT-R: TBA

### Convergence

1.  Convergence of Off-line Calibration
2.  Convergence of On-line Supply Calibration
3.  Convergence of On-line OD Matrix Estimation
4.  Convergence of Consistent Guidance

### Real-Time Data Feeding

1.  Sensor Counts (on segments)
2.  Incidents (on segments)

### Incident Processing

TBD

### Distributed Supply

1.  Map Decomposition:
      - The theory in the Wen Yang's PhD Thesis has been implemented
        inside DynaMIT-R: ![<File:Scalable> traffic
        simulation.pdf](Scalable_traffic_simulation.pdf
        "File:Scalable traffic simulation.pdf")
2.  Boundary Processing
      - The theory in the Wen Yang's PhD Thesis has been implemented
        inside DynaMIT-R.
3.  Synchronization
      - The theory in the Wen Yang's PhD Thesis has been implemented
        inside DynaMIT-R.

## Key Classes in DynaMIT-R Version 1

The way we explain the classes is "Topic-Based".

1.  we tell which classes are related with one topic, but we do not
    explain the classes themselves.
2.  if you want to modify or improve DynaMIT-R, you should firstly
    understand which part of DynaMIT-R you want to work on, and then you
    know which classes you need to access, understand and modify.
3.  Note: The higher level you change, the more work it takes. For
    example, if you want to change the On-line Estimation Logic, you
    have to check all the topics under it (You cannot just modify the
    structure and leave others away). But if you only want to output
    some information from the simulator, it is easier to implement.

### Top-Level Logic Control Classes

1.  /dynamit/SourceCode/processes/DynaMIT/DynaMIT.cc
2.  /dynamit/SourceCode/processes/Estimation/dtaEstimation.cc
    \[*Careful, Huge Class*\]
3.  /dynamit/SourceCode/processes/PredictionGuidance/dtaPredictionGuidance.cc
    \[*Careful, Huge Class*\]

### Network Related Classes

1.  /dynamit/SourceCode/components/NetworkTopology/dtaNetworkTopology.h
      - You can see the definition of Segment, Lane, LaneGroup, Loader,
        Sensor, etc
2.  /dynamit/SourceCode/components/NewPathTopology/dtaNewPathTopology.h
      - You can see how to get the candidate path, given inputs of O &
        D.

### User Behavior (Route Choice) Related Classes

1.  /dynamit/SourceCode/components/BehaviorModels/dtaBehaviorModels.h
      - You can see Pre-Trip Decision Making, including: route choice
        (most critical), Mode Choice, Departure Time Choice (or
        Departure Interval Choice).
2.  /dynamit/SourceCode/modules/ODTravelTime/dtaODTravelTime.h
      - You can access the candidate routes of each OD pair using this
        class.

### User Behavior (Speed & Queue) Related Classes

1.  /dynamit/SourceCode/modules/Supply/dtaSupply.cc \[*Careful, Huge
    Class*\]
      - Please check function: (dtaSupply::advancePacket)
      - You can see how the package (vehicle) is updated at both Moving
        Part & Queue Part.

### OD Estimation & Prediction Related Classes

It is not easy to explain how the functions of OD Estimation &
Prediction has been divided into the below 5 classes. So suggest you to
read all these 5 classes. In fact, OD Estimation and Prediction are 2
separate functions. But, since the source codes are all together, So, I
put them together here.

1.  /dynamit/SourceCode/processes/Estimation/dtaEstimation.cc
    \[*Careful, Huge Class*\]
2.  /dynamit/SourceCode/processes/PredictionGuidance/dtaPredictionGuidance.cc
    \[*Careful, Huge Class*\]
3.  /dynamit/SourceCode/modules/PreTripDemand/dtaPreTripDemand.cc
4.  /dynamit/SourceCode/modules/PreTripDemand/dtaODEstimationAndPrediction.cc
    \[*Careful, Huge Class*\]
5.  /dynamit/SourceCode/modules/MatlabEstimateOD/estimateOD.m
      - One bad issue is that Currently,we do not have the experience to
        compile this file. So, cannot modify the matlab code.
      - The problem has been Temporarily solved by moving from Matlab to
        Octave.

If you want to know more details, you can check the list of classes
below.

1.  dynamit/SourceCode/components/AssignmentMatrixList/dtaAssignmentMatrix.cc
      - You can see operations like: Smooth Assign Matrix, Normalize
        Assign Matrix, Deal with negative values., etc.
2.  dynamit/SourceCode/components/ODFactory/dtaODFactory.cc
      - There are many types of OD Tables (Historical, Estimated,
        Predicted, Temporary), you can see here, How DynaMIT pick the
        right one to use based on the current simulation time and
        purpose.
3.  dynamit/SourceCode/components/ODMatrixList/dtaODMatrixList.cc
      - This class manager a list of OD Matrix, based on different time
        periods.

### Output/Report Related Classes

In this part, there are 3 roles:

  - Report File Format Controller:
  - Report Object, like: flow, density, speed, queue length, assign
    matrix etc.
  - Report Caller, which means where or when to call the report
    functions.

Each of these 3 roles maps to:

1.  /dynamit/SourceCode/components/Report/dtaReport.cc (Format
    Controller)
      - You can see the supported report type: including HTML, TXT,
        Binary.
2.  /dynamit/SourceCode/components/SimulatedFlow/dtaSimulatedFlow.h
    (Report Object)
      - You can see the flow data is stored inside this class. The same
        thing,
      - You can see Density in
        components/SimulatedDensity/dtaSimulatedDensity.h
      - You can see Speed in
        components/SimulatedSpeed/dtaSimulatedSpeed.h
      - You can see Queue in
        components/SimulatedQueueLength/dtaSimulatedQueueLength.h
3.  In the source code, "idlReport::the()-\>writeMessage(Object)" is
    everywhere, used to call the defined functions. (Report Caller)
      - The object can be dtaSimulatedDensity and others.

### Guidance Related Classes

In this part, there are 3 roles:

  - Time Table: the table contains the weights for each segment. In
    DynaMIT-R, the weight can include time, money and others. But now,
    we only use Time.
  - Time Table Update Algorithm: It means how fast we update the table
    between historical value and the latest value.
  - Route Choice using the Time Table. (mentioned in Route Choice
    Section)

The details are in the classes.

1.  dynamit/SourceCode/components/ImpedanceTables/dtaImpedanceTables.cc
      - This class is the Time Table for route choice.
2.  dynamit/SourceCode/modules/Guidance/dtaGuidanceAlgorithm.h
      - The class has 2 sub-classes.
      - One is dtaNaiveAlgo.cc, which updates time table like:
        \[Value_Time_Table\] = \[Old_Value_Time_Table\]\*0.5 +
        \[New_equilibriumTravelTimes\]\*0.5;
      - The other is dtaTimeSmoothingAlgo.cc, which updates time table
        like: \[Value_Time_Table\] = \[Old_Value_Time_Table\]\*0.75
        + \[New_equilibriumTravelTimes\]\*0.25; (Configurable)

### Incident Related Classes

In this part: there are 3 roles:

  - Incident Table
  - Update Incident Table
  - Change Capacity based on incident type

The details are in below classes:

1.  dynamit/SourceCode/modules/Supply/dtaSupply.cc \[*Careful, Huge
    Class*\]
      - You can check the function: dtaSupply::initializeSupplyModule(),
        and then goto dtaSupply::reloadIncidentFile();
      - These functions is called once, before starting simulation.
      - This is where DynaMIT-R try to load in network.dat file.
2.  dynamit/SourceCode/components/ClosedLoopRunManager/closedLoopRunManager.cc
      - In this class, you can see DynaMIT-R is waiting for the
        incident.dat file, in function waitForIncidents().
3.  dynamit/SourceCode/modules/Supply/dtaSupply.cc \[*Careful, Huge
    Class*\]
      - This is the same class as the first one, but on different
        function.
      - You can see the capacity reduction in function
        dtaSupply::insertIncident().
4.  All incidents are kept in the variable "mpIncidents" inside class
    dynamit/SourceCode/modules/Supply/dtaSupply.h

### Distributed Supply Related Classes

1.  Map Decomposition:
    1.  ./modules/Supply/idlSupply.cc -\> theSupply = new
        dtaParallelSupply; \[select Parallel Supply\]
    2.  dtaEstimation::executeBaseCase(); \[for DynaMIT-P\]
    3.  idlSupply::the()-\>initializeSupplyModule(); \[for each OD
        interval (15 monutes)\]
    4.  dtaParallelSupply::initializeSupplyModule -\> getNodePartition(
        time ); \[re-generate partitions\]
        1.  related parameters:
        2.  getAllowLoadPartition:true;
        3.  m_fixed_partition: false;
    5.  dtaParallelSupply::getNodePartition -\> m_pm-\>doPartition()
        1.  m_pm is essentially use class dtaSmartPartitioner
    6.  dtaPartitionManager-\>doPartition()
    7.  dtaPartitioner.h -\> dtaPartitioner.h -\> part();
    8.  dtaParameters.cc -\> mPartitioningWeightType( PW_AUTO ); \[set
        the weight type\]
    9.  modules/Supply/dtaPartitioner.cc -\> fillFromNumPackets(); \[set
        weights\]
    10. modules/Supply/dtaPartitionBasis.h -\> dtaWeightsForMETIS;
        \[data structure to keep weights\]

## Units & Definition in Source Code

  - Link Length: meter
  - Vehicle Length: 5 meters
  - Segment-Based Density: (nPacs_in_Moving_part + (que /
    meanPacLength)) / (nL \* mLength);
  - Segment-Based Flow: () ([DEBUG_FLOW](DEBUG_FLOW "wikilink"))

## References

  - Review of DynaMIT source code, May 2012: ![<File:DynaMIT> code
    review-2.pptx](DynaMIT_code_review-2.pptx
    "File:DynaMIT code review-2.pptx")
  - Overview of source code by Rama, April 2012:
    ![<File:DynaMIT.pptx>](DynaMIT.pptx "File:DynaMIT.pptx")