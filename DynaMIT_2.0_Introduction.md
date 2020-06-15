The functionality of DynaMIT is currently being improved as part of the
DynaMIT 2.0 program. In particular the following features are being
added:

  - Contextual information: Ability to use textual sources of data both
    structured and unstructured. For example incident reports or event
    information obtained from the website.
  - Scenario Analyser: Ability to use additional sources of information,
    including contextual information, to improve network state
    estimation and prediction.
  - Strategy Simulation: Measure how effective mitigation strategies
    could be in reducing any predicted problems.
  - Public Transport: Modelling of trips made by MRT, LRT, and bus.

**`Requirements``   ``for``   ``DynaMIT``   ``2.0`**
`A meeting was held on 17th January 2013 in Washington DC following TRB with the "Founding Fathers" of DynaMIT.`
`At this meeting a list of requirements for the new DynaMIT 2.0 was produced.`
`These requirements are given in the following file: `![`File:``
 ``requirements_DynaMIT_TRB_20130117_v02.xlsx`](_requirements_DynaMIT_TRB_20130117_v02.xlsx
"File: requirements_DynaMIT_TRB_20130117_v02.xlsx")

## Overview

In DynaMIT 2.0, we developed three compoenents based on the 1.0
framework, namely

  - Online Calibration
  - Scenario Analyser
  - Strategy Simulation

The functionalities of these components are developed in separate
scripts from DynaMIT-R core, to allow modellers to test different
methodologies as easiler as possible. They're discussed in detail in
later sections. Here we present an overview of the DynaMIT 2.0
architecture:

![File: D2.0.archi.png](_D2.0.archi.png "File: D2.0.archi.png")