## Description

MITSIM is a simulation-based laboratory developed for evaluating the
impacts of alternative traffic management system designs at the
operational level. It was developed at the MIT Intelligent
Transportation Systems (ITS) Program.

In this page, MITSIM is used inside the closed-loop of "MITSIM-DYNAMIT".

  - MITSIM is the real world;
  - DynaMIT-R is simulation & prediction based TMC;

## Documentation

`MITSIM users guide, includes guide for road network editor: `![`File:``
 ``MITSIM_Manual.pdf`](_MITSIM_Manual.pdf "File: MITSIM_Manual.pdf")

`MITSIM new developers guide: `![`File:``
 ``MITSIM_NewDeveloper.pdf`](_MITSIM_NewDeveloper.pdf
"File: MITSIM_NewDeveloper.pdf")

## SourceCode Download

[SourceCode with SCATS](SourceCode_with_SCATS "wikilink"):

[SourceCode without SCATS](SourceCode_without_SCATS "wikilink"):

## SourceCode Structure

### MITSIMLab Flow Chart

[MITSIMLab Flow Chart](MITSIMLab_Flow_Chart "wikilink")

### MITSIMLab Folders

[MITSIMLab Folders](MITSIMLab_Folders "wikilink")

## Close Loop Framework

### The framework

  - MITSIM: Real-World
  - DynaMIT: Decision Maker

![DynaMIT_MITSIMLab_Close_Loop.png](DynaMIT_MITSIMLab_Close_Loop.png
"DynaMIT_MITSIMLab_Close_Loop.png")

### User guide

A very brief guide for setting up closed-loop is listed below, and the
detailed guide is available in [MITSIM notes](MITSIM_notes "wikilink"):

  - MitSIM side: in *master.mitsim*,
      - set *ClosedLoopGuidance* parameter to point to the guidance file
        generated by DynaMIT (recommend to use absolute path).
  - DynaMIT side: in *dtaparam.dat*,
      - set *MitsimSensorsFile* parameter to point to the sensor output
        file generated by MitSIM (recommend to use relative path). In
        addition, *MaxEstIter* must be greater than 1 in order for
        DynaMIT to wait for MitSIM's sensor data.

In addition, below items provide good supplementary documentation on
setting up and running closed-loop with special needs.

  - Enable tolls in ClosedLoop: [Supporting Tolls in
    ClosedLoop](Supporting_Tolls_in_ClosedLoop "wikilink")
  - Turning sensitive travel times: [Turning sensitive tt in
    ClosedLoop](Turning_sensitive_tt_in_ClosedLoop "wikilink")

### Q\&A

[Questions and Answers](Questions_and_Answers "wikilink")