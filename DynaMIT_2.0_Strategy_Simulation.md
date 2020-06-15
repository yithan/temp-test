Like previous two pages, this page is intended to serve as a user guide
for DynaMIT users and new developers.

## Overview

In DynaMIT 2.0 Strategy Simulation (SS), we try to evaluate the impact
of different control strategies to future traffic, and based on some
predifined objective measure, we choose the best strategy to be
implemented in real world (in closed loop it's Mitsim). Strategy
simulation is somehow similar to an enchanced state prediction, and
indeed it is implemented like this. Currently we're evalutating
different toll strategies.

From implementation point of view, the procedures are similar to those
of online calibration. The optimisation algorithm is implemented as an
external component (such as a matlab script or C executable), and
DynaMIT-R communicates with it before each prediction interval. To be
specific, in closed loop, if DynaMIT-R has SS enabled, at the end of
every state estimation interval, DynaMIT-R saves its current state
(including estimated ODs, current network state etc), and invokes the SS
component. SS then generates different control strategies (different
toll vectors), evaluate them by running supply simulation for a future
period, and choose the "best" tolls and give them to Mitsim. The
evaluation of different toll vectors could run in parallel on multicore
computers.

SS runs supply simulations by making copies of original DynaMIT-R
folders and runs an executable specially tailored for this purpose.
Actually the term "running supply" is not quite accurate. In closed
loop, Mitsim requires another critical guidance from DynaMIT, and that
is the predicted travel times, thus when SS evaluates a strategy, the
simulation it runs must also be able to generate proper tt guidance
under this toll vector. This guidance generation is already implemented
in DynaMIT-R's state prediction, thus the specially tailored executable
works in below mannar:

1.  it receives toll vector from SS, along with other control parameters
    such as prediction horizons etc.
2.  it restores the state where DynaMIT-R has left off, ie. picks up
    estimated ODs and network condition
3.  it runs the same state prediction procedure, in which the tt
    guidance is iterated until convergence is reached
4.  it reports travel times, packet utilities etc to SS for strategy
    evaluation

In this mannaer, the toll vector being evaluated is consistent with the
travel time guidance, and together the best tuple are feed back to
Mitsim.

The procedures described above correspond to "Purpose Of Run"
**PredictiveStrategic** of DynaMIT_P.

### Strategy Simulation optimisation algorithms

[Algorithm documentation to be added, for Samarth, Shi and
Jenny](Algorithm_documentation_to_be_added,_for_Samarth,_Shi_and_Jenny "wikilink").

## User guide

Parameters in **dtaparam.dat** for DynaMIT-R:

| Options                                    | Descriptions                                                                                                                                                                                                            |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <font color="Navy">GenerateStrategy</font> | The control switch; if it's set to 1 Strategy Simulation is turned on, and original state prediction phase will be repalced by strategy simulation procedures; otherwise traditional state prediction would take place. |

### Run DynaMIT-R with Strategy Simulation

For general steps please refer to the same section in [online
calibration](DynaMIT_2.0_Online_Calibration "wikilink"), with some
addional comments:

  - DynaMIT-R now requires a new input file "toll.dat", in which the
    toll values for first estimation interval should be specified.
  - You probably need to install "gnu parallel" package to gain
    performance on multicore computers.
  - The source code for strategy simulation optimisation resides in
    "GenerateStrategy" folder of git repository. Build it and place the
    binary under DynaMIT-R working directory.

For format of toll files or how they're used in Mitsim, refer to
[Supporting_Tolls_in_ClosedLoop](Supporting_Tolls_in_ClosedLoop "wikilink").

An demo DynaMIT package is available in
[DynaMIT_2.0_Demo_Package](DynaMIT_2.0_Demo_Package "wikilink").