## DEBUG FLOW in DynaMIT-R

  - All the debugs are done on a small network, created by Lulu.
  - The small network is a one direction road, comprised by 2 links and
    4 segments and 4 lanes.
  - Capacity of each segment is 3600 vehicle pr hour.

### Problem

  - Even loading 10 vehicles per hour, the flow can be 60 and 120;
  - Where is the flow come from?

### Debug

  - Does the loader loaded in exactly 10 vehicles?
      - YES. in the 4 intervals, the number of packs are {3,4,3,3}