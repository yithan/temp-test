1.  METIS functions are defined in ./modules/Supply/dtaPartitionBasis.h
    ![<File:METIS_Functions.png>](METIS_Functions.png
    "File:METIS_Functions.png")
      - The forth function should be used in DynaMIT, by default. It
        means to decompose network equally.
2.  Who is calling partitioning in DynaMIT?
      - dtaPartitionBasis.h -\> METIS_WPartGraphKway(); &
        METIS_WPartGraphRecursive();
      - dtaPartitioner.h (Class dtaSmartPartitioner) -\> void part();
      - dtaPartitionManager.h -\> doPartition();
      - dtaParallelSupply.cc -\> getNodePartition(); //will write
        results to output folder
      - dtaParallelSupply.cc -\> initializeSupplyModule();
      - dtaEstimation.cc -\> execute() & dtaPredictionGuidance.cc -\>
        execute();
3.  Who is the logic of road network partitioning in
    initializeSupplyModule()?
      - Case 1: 1st interval, 1st iter, then call getInitPartition();
      - Case 2: fix partition for all intervals, then do not change any
        file.
      - Case 3: 1st iter for a new interval,
      - Case 3.1: if in estimation phase, then use predicted weights.
      - Case 3.2: if in prediction phase, then use previous weights in
        estimation phase. (In case, the prediction length is only 1).
      - Case 4: not the 1st iter, then use weights in previous iter.
4.  What parameters is used for load balance?
      - in file dtaParameters.cc -\> mPartitioningWeightType.
      - Candidate: dtaConst.h -\> PW_AUTO = 0 (default),
        PW_NUM_PACKETS = 1, PW_DSY, PW_FLW, PW_FILE, PW_UNKNOWN
      - Mapping Functions: dtaPartitioner.cc -\>
        dtaPartitionWeightAllocator::fillFromNumPackets (example
        PW_AUTO)
      - Count = Density \* Length;