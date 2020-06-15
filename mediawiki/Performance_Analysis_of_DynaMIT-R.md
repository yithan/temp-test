## Notes

1.  DynaMIT (Dynamic Network Assignment for the Management of
    Information to Travelers) is a real time dynamic traffic assignment
    system that provides traffic predictions and travel guidance.
2.  The accuracy of DynaMIT-R is measured by RMSN of predicted traffic
    flow in the next K intervals.
3.  DynaMIT runs following [Rolling Horizon
    Model](Rolling_Horizon_Model "wikilink"). So, the performance of
    DynaMIT-R means "How much time DynaMIT-R needs to support Traffic
    Predictions in one Interval?". We call it DynaMIT-R's running time
    in one interval (To be simply, sometimes, I will omit "in one
    interval").
4.  In one interval (for example: 15 mins), DynaMIT-R needs to do 3
    things.
      - Load in Real-Time Fusion Data. (Counts, Incidents, Others)
      - Estimate the traffic conditions in previous interval.
      - Predict the future traffic conditions in next K intervals.
5.  This page introduces how we can reduce the running time of
    DynaMIT-R.
      - Generally, we have two directions to reduce the running time.
      - Solution 1: Add more computers (with an acceptable time
        speedup).
      - Solution 2: Change some parameters to re-balance between
        accuracy and running time.

## Outline

1.  DynaMIT-R (MPI) Distributed Version
    1.  Theory
    2.  Implementation
    3.  [Base Case](Base_Case "wikilink") Speed Up (5 times)
    4.  Speed Up & Parameters (UnSure: whether accident matters)
          - Speed Up & Accidents
          - Speed Up & Traffic Demand
          - Speed Up & Iteration
          - Speed Up & Traffic Update
          - Speed Up & Prediction Length
          - Speed Up & Road Network (important, but cannot do now)
2.  DynaMIT-R Parameters & Performance
    1.  Theory
    2.  Balance With Accidents
          - Balance Traffic Demand With Accidents
          - Balance Iteration With Accidents
          - Balance Traffic Update With Accidents
          - Balance Prediction Length With Accidents
    3.  Balance Without Accidents
          - Balance Traffic Demand Without Accidents
          - Balance Iteration Without Accidents
          - Balance Traffic Update Without Accidents
          - Balance Prediction Length Without Accidents

Besides:

1.  In this section "Distributed Version", we talk about increase
    Machines to reduce the running time. We assume that the accuracy of
    DynaMIT-R is not seriously changed when change the number of
    Machines. (Read YangWen's Thesis \[There are slight difference when
    increasing the number of Machines\])

## Materials

![<File:Incidents.pdf>](Incidents.pdf "File:Incidents.pdf")