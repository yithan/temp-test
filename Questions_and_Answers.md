1.    - Question: How frequently real-world data is collected and feed
        into DynaMIT-R?
      - Answer: It is configurable. 5 mins & 15 mins are used in our
        case study.

2.    - Question: How about the time delay from the real-time data
        collection to real-time strategy feedback?
      - Answer: It is configurable. Currently, in order to make the
        problem simply to analysis, we force the real world (MITSIMLab)
        to stop and wait for DynaMIT's results. But, we allow the
        real-world to move, in order to mimic the delay of real-time
        strategy feedback.

3.    - Question: How Drivers response to Information Guidance?
      - Answer: It is configurable. In paralib\*.dat, \[Compliance
        Rates\], the last parameter;

4.    - Question: Why DynaMIT does not load in sensor data from MITSIM,
        even though the data is already there?
      - Answer: Please check the file name and file type and file path;
        And also check the first time interval;

5.    - Question: what does batchTime, macroTime, microTime, pathTime
        mean in TS_Engine::simulationLoop()?
      - Answer:
      - batchTime: the time decision point to output network status;
      - macroTime: the time decision point to update segment status,
        like: density and speed;
      - microTime: the time decision point to update GUI;
      - pathTime: the time decision point to update link/segment travel
        time of guided drivers and change routes if requested;

6.    - Question: Where is LWC data getting from?
      - Answer: trmpet server -\> backup -\> sarvee's home folder -\>
        testKalman/testAVI/cl_lwc