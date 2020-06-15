DynaMIT is organized around two main functions: state estimation, and
prediction-based guidance generation. The overall structure with
interactions among the various elements of DynaMIT is illustrated in the
right Figure.

DynaMIT utilizes both off-line and real-time information. The most
important off-line information, in addition to the detailed description
of the network, is a database containing historical network conditions.
This is the system's memory. The real-time information is provided by
the surveillance system and the control system. DynaMIT is designed to
operate with a wide range of surveillance and control systems.

The state estimation component determines the current state of the
network and the current demand levels given historical and surveillance
data. Two simulation tools are being used iteratively in this context:
the Supply Simulator and the Demand Simulator (see Antoniou et al. and
Ben-Akiva et al. for more details). The Demand Simulator estimates and
predicts Origin-Destination (OD) flows and drivers decisions in term of
departure time, mode and route choices. An initial estimate of the
demand is directly derived from the data. The Supply Simulator
explicitly simulates the interaction between that demand and the
network. Assignment Matrices, mapping OD flows into link flows, are
produced by the simulator. The Assignment Matrices and real-time
observations are then used by the Demand Simulator to obtain a better
estimate of the demand. This loop is executed until congruence between
demand and supply is obtained, that is when the simulation reproduces
sufficiently well the observed data.

The prediction-based guidance generation module provides anticipatory
guidance using as input the state estimate. Traffic prediction is
performed for a given horizon (e.g. one hour). The Demand Simulator and
Supply Simulator are also used for prediction. The guidance generation
is based on an iterative process between traffic prediction and
candidate guidance strategies. The system enforces consistency between
the travel times on which the guidance is based and the travel times
which result from travelers' reactions to the guidance.

![File: DynaMIT Structure.png](_DynaMIT_Structure.png
"File: DynaMIT Structure.png")