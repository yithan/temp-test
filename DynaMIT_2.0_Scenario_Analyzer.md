Similar to online calibration page, this page is intended to serve as a
user guide for DynaMIT users and new developers.

## Overview

In DynaMIT 2.0, before starting state estimation of each interval,
DynaMIT-R could be configured to consult an external component, called
"Scenario Analyzer", to obtain more information about current traffic
conditions. Two specific pieces of information are road incidents and
special events that could cause demand spikes to certain places.

Currently only incident prediction is implemented in Scenario Analyzer
(SA). It gathers information from various data sources and issues
DynaMIT its predictions on incidents that has happened on the road. The
predictions mainly consist of how long an incident will last and how
severe it is (capacity reduction). This information is written to
incident file to be read by DynaMIT-R, and it will affect supply
simulation.

### How is incident information used

-----

In DynaMIT 1.0 where supply is not calibrated, the incident information
goes directly into supply simulation, where capacity reducted are appled
to affected segments during incident's active period. However, things
are slightly more complicated in DynaMIT 2.0. If online calibration is
enabled and supply parameters are calibrated, the incident information
first goes to online calibration, and supply parameters coming out of OC
is considered final, and capacity reductions will not be applied in
state estimation phase's supply simulation. During state prediction
phase, we assume supply parameters out of OC are still valid, and thus
again the incident information is ignored and oc calibrated parameters
are used.

Above is for DynaMIT-R only. For DynaMIT-P the situation is not changed
since version 1.0 - incident information is only used in supply
simulation.

### Scenario Analyzer prediction model

[Aidan's model documentation to be
added](Aidan's_model_documentation_to_be_added "wikilink")

## User guide

To enable scenario analyser, adjust **dtaparam.dat** with following
parameters:

| Options                                                    | Descriptions                                                                                                                                                                                               |
| ---------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <font color="Navy">SAScriptName</font>                     | The name of SA script, without .m extension. relative path is supported. If mcc approach is used, the path to the compiled executable. If option is not specifed or name is empty, SA will not be invoked. |
| <font color="Navy">RollbackOnPoorIncidentPrediction</font> | If set to 1, on finding inconsistent predictions from those of previous intervals, it will roll back to an earlier time and re-start state estimation from that time. By default it's not enabled.         |

### Run DynaMIT-R with Scenario Analyser

-----

For general steps please refer to the same section in [online
calibration](DynaMIT_2.0_Online_Calibration "wikilink") page. Additional
notes:

  - You need to copy the *scenario_analyser* folder into DynaMIT
    working directory, and configure *SAScriptName* and *IncidentFile*
    in dtaparam.dat to refer to the right names.
  - By default SA.m sits in the sub-directory of DynaMIT working dir,
    and it generates incident file within its own directory.
  - As of end June 2015, the mcc version of DynaMIT can not be used with
    scenario analyser, due some limitations in MCR handling function
    handles in .mat data files (which contains trained models used by
    SA).

An demo DynaMIT package is available in
[DynaMIT_2.0_Demo_Package](DynaMIT_2.0_Demo_Package "wikilink").