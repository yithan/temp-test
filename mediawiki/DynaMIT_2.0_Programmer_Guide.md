If you're new to DynaMIT, you may also want to take a look at [Beginners
Guide](Beginners_Guide "wikilink") and/or [Running
DynaMIT](Running_DynaMIT "wikilink") in Training section of this wiki
website.

Alternatively, if you just need a quick start guide, refer to the
**README** file in code repository, see below.

## Code repository

DynaMIT 2.0 code repository resides in github, under "smart-fm"
organisation. The code access is managed by administrators of this
orgnisation. To get access, register a github account yourself and ask
the administrators to grant you access to "smart-fm" project "dynamit".

There's another repository in SMART internal git repository, but it is
out-of-dated and should be avoided.

## Building and Running DynaMIT

After cloning dynamit repostory, you'll find several folders under the
root. Among them, *SourceCode* folder contains all source codes and 3rd
party libraries for DynaMIT, DynaMIT_P and a couple of toolkits used
for debugging, visuallisation and so on. DynaMIT 2.0 developers please
do have a read on the **README.txt** in repo's *SourceCode* folder for
instructions for building and running DynaMIT. The page [New developer
guide](Tutorial "wikilink") written during DynaMIT 1.0 period also
contains lots of useful information too.

Just to emphasize on one important pre-requisite - do remember to set up
MCR environment before running it. For details refer to the README.txt.

## Highligths

First thing, DynaMIT-R is driven by the so-called "path impedance" (path
travel times). Having an idea on how the impedances are generated and
transformed and how they affect state estimation and prediction will
help you to quickly grabbing the essence of the system. Before getting
deeper into each item below, it would help a lot if you have rough
understanding of the system.

Below list some of the key points which could greatly help the
understanding the flow of DynaMIT.

  - Historical impedance table are w.r.t to simulation start.
  - Current guidance impedance table is reset every prediction interval,
    and it covers the periods designated by prediction horizon plus
    historical extension.
  - Under planning (or supply-only) mode, planning impedance table is
    used, and it is updated every iteration from supply simulator result
    from previous iteration.
  - No link travel times are aggregated during state estimation, neither
    there is impedance auto-regression during state prediction (only
    demand, or strictly speaking deviations in demand, is an
    auto-regressive process).
  - During state prediction, initial guidance is generated by running
    supply simulation by dis-aggregating demand using historical
    impedance.
  - The interaction between estimation and prediction:
      - estimation -\> prediciton : demand
      - prediction -\> estimation (of next interval) : guidance
  - Link toll and impedance lookup always chooses the value at the time
    when the vehicle is estimated of reaching the corresponding link.
  - When a vehicle passes through a link, its travel time along this
    link (averaged with similar vehicles) will be used to update the
    link time entry corresponding to the time when the vehicle enters
    the link.
  - Behavioral update and online disaggregation don't re-generate list
    packets from scratch. Instead only changes to existing packets (mode
    change, trip cancellation, departure time change, route change) are
    applied.

## Issues

Below lists issues currently identified, but whose solution has not yet
been decided:

  - Pretrip decision change route (in state estimation) **seems** to
    have no effect - it affects "habitualLink" and "habitualPath" field
    of packets, but the "nextLink" and "nextPath" field (used by supply
    simulator to determine path) of packets are not affected.
  - Behavior update for existing packets (in state prediction) **seems**
    to have no effect, reasons to be investigated.
  - Decisions on en-route path update are made at wrong time, the
    en-route decision to change path is made when a packet arrives at a
    node and is about to move to next link, even if it is currently
    queuing in a lane that has no connection to that link.
  - Guidance is not fed back when strategy generation is turned on
  - Impedance values in historic table extension should use last value
    instead of historical value

## Suggestions

Below is a list of things which would greatly benefit the project, if
they had been implemented in the first place when the project was being
developed. We think in the next phase below practices should be
implemented / followed strictly.

  - Unit testing, unit testing, unit testing\!
  - Service based data feed architecture
  - Unused (or maybe unused) code cleanup
  - Editable programmer guide
  - Automated regression