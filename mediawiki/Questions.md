<center>

<font size="+3">Questions & Answers</font>

</center>

## Instructions

  - Your questions will be read by other members, so please make your
    questions understandable.
  - You are welcome to comment and answer questions.
  - Please do not remove other's questions.
  - We created 5 users for you to login in.
      - name: Dynamit1, Dynamit2, Dynamit3, Dynamit4,Dynamit5
      - password: dynamit

## General Questions

1.  What is DynaMIT-R?
      - DynaMIT-R is a real time dynamic traffic assignment system that
        provides traffic predictions and travel guidance. GoTo
        [Introduction](Introduction "wikilink") to know more.
2.  What is inside DynaMIT Source Code?
      - There are 4 major executable files:
        1.  DynaMIT/DynaMIT : can call it DynaMIT-R, it is for real-time
            traffic prediction and guidance
        2.  DynaMIT/DynaMITmpi : it is for distributed DynaMIT-R
        3.  DynaMIT_P/DynaMIT_P : it is for offline traffic planning
        4.  DynaMIT_P/DynaMIT_Pmpi : it is for distributed DynaMIT-P
3.  What OS we need to run DynaMIT?
      - Linux (like:Ubuntu)
4.  What is the unit(length) ?
      - By Default: feet & mile/hour & second
5.  What is online calibration doing now?
      - OD Calibration: I have mentioned before.
      - Route Choice Parameters: Not Implemented.
      - Supply Calibration: Segment-Based (mAlpha, mBeta,
        mFreeFlowSpeed, mMinSpeed, mJamDensity, Lane Capacity)
          - Seg(New) = Seg(Old) \* Ratio; Ratio = (0.75-1.25)
          - Different Variables (6) can have different Ratio; But given
            one variable, each segment has the same ratio. It means
            Online Calibration makes the same variable of all segments
            moving in one direction.
          - In order to know what the ratio is: (Assume we focus on one
            variable, like: mAlpha)
              - Step 1: Increase mAlpha +5%; Run Simulation; Measure
                Sensor Counts A;
              - Step 2: Decrease mAlpha -5%; Run Simulation; Measure
                Sensor Counts B;
              - Step 3: jacobian matrix = (SenSensor B - Sensor A) /
                (10%);
              - Step 4: Use Raw mAlpha; Run Simulation; Measure
                Difference between estimated sensor and observed sensor;
              - Step 5: Calculate Ratio based on (1) jacobian matrix and
                (2) Difference; \[I did not understand the Kalman Filter
                here.So, cannot decide which version of Kalman Filter it
                is using\]
          - In Conclusion: for each on line calibration, it needs to run
            Simulation: (6\*2) + 1 = 13; Which is a lot.
          - I do not know whether the code is the same with Jorge's
            version. Also, I did not used it for on-line calibration
            yet.

## Technical Questions

1.  What is the supported gcc/g++ versions?
      - We have tried gcc/g++ 4.4, 4.5, 4.6.
2.  What is flex/bison++ used for?
      - They are used for generating codes to read input files, like:
        demand.txt, incident.txt
3.  In dtaparam.dat, what does "closed loop" means for DynaMIT-R?
      - Combine DynaMIT-R with MITSIMLab
4.  What is the partitioning algorithm I am using? Based on WHAT?
    Especially what to do for prediction?
5.  What is the Stopping Criteria in Estimation Phase?
      - Compare Sensor Data with Simulated Data:
      - reference = idlSurveillance::the()-\>createFlowIterator( ti );
      - candidate = idlSimulatedSensorFlow::the()-\>createFlowIterator(
        );
      - threshold = 0.001; (hardcoded)
      - Compare (Sqrt(pow(A-B),2)) \< 0.001
6.  What is the Stopping Criteria in Prediction Phase?
      - Compare Flow in Last Phase with Flow after guidance;
      - reference = Last Phase;
      - candidate = New Phase after Guidance;
      - threshold = 0.001; (hardcoded)
      - Compare (Sqrt(pow(A-B),2)) \< 0.001
7.  Can I run MATLAB (auto regression) on OpenMPI?
      - YES
      - But, for some machines, like: hermes2, I failed to execute it.