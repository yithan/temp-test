Turning sensitive travel time gives more than one travel times for a
link at a given time, accounting for the differences of traffic moving
towards different downstream links. Compared with the case where a
single travel time for each link, it gives better estimation of path
travel times.

To use turning sensitive tt in closed loop, we need to provide both
DynaMIT and MITSim a special version of historical_tt file, and tell
them in their configuration file that turning sensitive is enabled.

## Link time format

    start_index
    num_periods
    period_length
    {
    link_id next_link_id length tt tt tt ...
    }

The row starting with \<link_id, next_link_id\> identifies the (time
depedent) travel times on link_id towards next_link_link. If a link
has no downstream links, we must to provide a dummy next_link_id as
"2147483647" (INT32_MAX) to indicate the link has no downstream links.

Similar to the old travel time file, if you don't provide the record for
a specific pair, both systems would calculate the travel time based on
link length and free speed.

## DynaMIT configuration

In *dtaparam.dat*:

  - Under \[Files\] section, add **DirectionalTT = 1**.

## MITSim configuration

In *master.mitsim*:

  - enable option 0x0010 in **spFlag**.

## Demo package

A demo package is availabe in DynaMIT
[dropbox](https://www.dropbox.com/sh/3pe3ovxhu1c2tyh/AABO0D6XYQjEisyghrWYumb0a?dl=0)
folder.