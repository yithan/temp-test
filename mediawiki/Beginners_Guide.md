DynaMIT-R (Dynamic Network Assignment for the Management of Information
to Travelers) is a real time dynamic traffic assignment system that
provides traffic predictions and travel guidance. DynaMIT generates
prediction-based guidance with respect to departure time, pre-trip path
and mode choice decisions and en-route path choice decisions. It
supports both prescriptive and descriptive information. In order to
guarantee the credibility of the information system, the guidance
provided by DynaMIT is consistent, meaning that it corresponds to
traffic conditions that most likely will be experienced by drivers.
Hence, DynaMIT provides user-optimal guidance, which implies that users
cannot find a path that they would prefer compared to the one they chose
based on the provided information.

This guide provides a list of essential reading for beginners to
DynaMIT. It is suggested that the user reads all documents in the
Overview section. Depending on what the user will be working on they
should read the sections as follows:

  - Software: people who will be developing or tweaking the DynaMIT
    software
  - Calibration: people who will be working on calibrating DynaMIT
  - Implementation: people who will be involved in implementing DynaMIT
    somewhere

After reviewing the above documents it is suggested the user looks at
the rest of the WikiMedia site. In particular the
[Papers](Papers "wikilink") and
[Presentations](Presentations "wikilink") section

## Overview of DynaMIT

The following document provides a very comprehensive overview of
DynaMIT:

**`"Traffic``   ``Simulation``   ``with``
 ``DynaMIT"`**`, (2010), Ben-Akiva et al.  This is chapter 10 of the book entitiled "Fundamentals of Traffic Simulation", edited by Jaume Barcelo.  ISBN: 978-1-4419-6141-9`
![<File:DynaMITChapterBarceloBookFullText.pdf>](DynaMITChapterBarceloBookFullText.pdf
"File:DynaMITChapterBarceloBookFullText.pdf")

Beow two power-points provide a good introduction to both DynaMIT and
DynaMIT-P (the links are available in [Running
DynaMIT](Running_DynaMIT "wikilink")):

`DynaMIT_Demand_Simulator_Overview`
`DynaMIT_P_Tutorial`

## Theories

DynaMIT simulations can be split into two main parts:

  - Demand: The relates to modelling the trips that are made and the
    route that travellers use for these trips
  - Supply: This relates to the state of the transport network given the
    trips being made. In particular what is the state of each road
    segment: travel time, queue length, speed, etc.

Below two documents are 'must-read's for understanding the models used
in DynaMIT (both demand and supply). They can be found in [Papers by
Year](Papers_by_Year "wikilink") section.

`TASK A Evaluation Report partA`
`Appendix D: Models and Algorithms`

The document below provides an overview of some of the key concepts used
in modelling packets of vehicles in DynaMIT.

**`"DYNAMIT``   ``-``   ``Dynamic``   ``Network``   ``Assignment``
 ``for``   ``the``   ``Management``   ``of``   ``Information``   ``to``
 ``Travelers"`**`, (1998) Sridhar Rajagopal.  `
![<File:Sridhar_DynaMIT_MS.pdf>](Sridhar_DynaMIT_MS.pdf
"File:Sridhar_DynaMIT_MS.pdf")

## User guide

The data required for DynaMIT is described in detail in section 10 of
the following guide

**`"DynaMIT``   ``System``   ``User``
 ``Guide"`**`, (2008), Balakrishna et al.`
![<File:DynaMIT_system_user_guide.pdf>](DynaMIT_system_user_guide.pdf
"File:DynaMIT_system_user_guide.pdf")

## Calibration

DynaMIT uses thousands of parameters. These paramaters include: segment
capacities, segment speed-density characteristics, Origin-Destination
flows in each time period, and other behavioural characteristics. Since
it is not possible to measure all of these, the parameters must be
"intelligently guessed" in a process called calibration. There are two
types of calibration:

  - off line calibration: This is the initial calibration of the OD
    demand files and network characteristics. This is done BEFORE the
    DynaMIT simulation is run
  - on line calibration: This is the calibration to "tweak" the OD
    demans and network characteristics as the DynaMIT simulation is
    running in real time

`"`**`Off-line``   ``Calibration``   ``of``   ``Dynamic``   ``Traffc``
 ``Assignment``   ``Models`**`" (2006), Ramachandran Balakrishna`
`phd thesis = `![<File:PhD>`   ``Thesis``   ``of``   ``Ramachandran``
 ``-``   ``Off-line``   ``Calibration``   ``of``   ``Dynamic``
 ``Traffic``   ``Assignment``
 ``Models.pdf`](PhD_Thesis_of_Ramachandran_-_Off-line_Calibration_of_Dynamic_Traffic_Assignment_Models.pdf
"File:PhD Thesis of Ramachandran - Off-line Calibration of Dynamic Traffic Assignment Models.pdf")

`Calibration of the Demand Simulator in a Dynamic Traffic Assignment System (2002), Ramachandran Balakrishna`
`master's thesis = `![<File:Rama_Masters.pdf>](Rama_Masters.pdf
"File:Rama_Masters.pdf")

As part of the research in Singapore, a masters student in USA developed
a new approach to off-line calibration called W-SPSA. This is well worth
reading:

`Lu Lu (2014) "W-SPSA: An Efficient Stochastic Approximation Algorithm for the Off-line Calibration of Dynamic Traffic Assignment Models", Masters thesis at MIT`
`master's thesis = `![<File:Thesis_LuLu.pdf>](Thesis_LuLu.pdf
"File:Thesis_LuLu.pdf")

## Software

People who will be involved in coding DynaMIT in any way should read the
following documentation:

**`Development``   ``of``   ``a``   ``Deployable``   ``Real-Time``
 ``Dynamic``   ``Traffic``   ``Assignment``
 ``System`**` (2002): This document contains detailed information on DynaMIT-R for programmers.  It is slightly out-of-date`
![<File:DynaMIT_Programmer_Guide_Aug2002.pdf>](DynaMIT_Programmer_Guide_Aug2002.pdf
"File:DynaMIT_Programmer_Guide_Aug2002.pdf")

**`Tutorial`**
`There is also an excellent tutorial on developing DynaMIT and on using the GIT repository here: `[`Tutorial`](Tutorial "wikilink")

**`Source``   ``Code`**
`DynaMIT source code is available here: `[`SourceCode`](SourceCode "wikilink")

<b>It is strongly recommended to read the README.txt under the
SourceCode folder before attempting to compile and run DynaMIT.</b>

## Overview of DynaMIT 2.0 project

DynaMIT 2.0 is a new project that will add new functionality into
DynaMIT. In particular this includes:

  - Public Transport
  - Novel data sources
  - Strategy Simulation
  - Data Quality improvements

Significant enhancements will aslo be made. This includes in areas such
as:

  - Scalability
  - Calibration (both off-line and on-line)
  - Modelling supply in urban areas

The following document provides a brief summary of the main concepts in
DynaMIT and summarises some of the aims of the DynaMIT 2.0 project:

**`DynaMIT``   ``2.0:``   ``Advances``   ``in``   ``real``   ``time``
 ``traffic``   ``simulators`**`, (2013) Steve Robinson`
![<File:DynaMIT_2_ITSWC_20130802.pdf>](DynaMIT_2_ITSWC_20130802.pdf
"File:DynaMIT_2_ITSWC_20130802.pdf")

## MITSIM

MITSIM is a traffic micro simulation that can be used to test DynaMIT in
a closed loop fashion. MITSIM documentation is available here:
[MITSIM](MITSIM "wikilink")