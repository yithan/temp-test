This section documents the plan for modelling incident from dynamic
segment (i.e., lane-closure as a start) perspective.

## Incident file format

The incident file format has changed and is not backward compatible. One
extra field is added, and this is scheme_id sitting in the first field
of each incident record. We'll give the old capacity based incident
scheme 1, and the new scheme as scheme 2. Now, the incident file
consists of lines like below:

    scheme_id segment_id_or_lane_id start_time end_time reduced_factor incident_id incident_report_time

## The model

During supply initialization phase, the incident file is read, and the
start time and end time of each incident are rounded to the nearest
minute (or more precisely, the update interval). During each update
phase, the lanes affected by the incident with speed reduced to 0 will
be marked "closed". For other lanes where the reduced speed is not zero,
the free flow speed of the parent lane group is set to *max(V_min,
V_reduced)*, and if multiple lanes of same lane group have different
V_reduced, the averaged V_reduced is used.

In this case, lane closure is modelled by setting the lane to "closed"
state. If a lane is "closed", we'll also remove all incoming and
outgoing lane connections of the closed lane. In addition, depending on
the position of its parent segment, we'll also update lane connections
of its neighbouring lanes (left, right or both if both are present). If
the segment is:

  - last segment of a link: the neighbouring lanes will inherit its
    outgoing lane connections.
  - first segment of a link: the neighbouring lanes will inherit its
    incoming lane connections.
  - intermediate segment: currently we assume the network has full lane
    connections in-between intermediate segments, and we do not inherit
    lane connections. However, it may worth to apply the same inheriting
    logic to intermediate segments if the assumptions don't hold.
  - if multiple neighbouring lanes are closed the logic applies
    iteratively so that the outcome is still valid.

During each update phase, if an incident is found to have been cleared,
the "closed" flag of the corresponding lane is also removed and original
lane connection status will be restored.

### More on lane closure

A "closed" lane is treated differently in that:

1.  During speed calculation, closed lanes are not considered in density
    calculation (for both the lane group and the segment).
2.  The output capacity of a lane group is calculated without the closed
    lane.
3.  The acceptance capacity check (segment-wise if no queues or lane
    group-wise otherwise) also excludes the closed lane.
4.  The acceptance rate calculation also excludes the closed lane.
5.  Segment queue length computation also excludes the closed lane
    (<font color="red">Is this intended?</font>).

The outcome is the same as if the lane has "vanished" during the
incident period.

By combining all the effects such as lane connection updating, a closed
lane has following implications:

1.  After incident occurs, new queues will never form on a closed lane
    since it is not connected to any downstream lanes.
2.  If all lanes within a lane group are closed, the lane group will
    never be selected when new vehicles enters it.
3.  Queuing vehicles existing in a closed lane at the very beginning of
    the incident discharge as usual, but new vehicles never enter the
    closed lane.
4.  If all lanes within a lane group are closed, moving vehicles
    existing in the lane group at the very beginning of the incident
    discharge as usual, but new vehicles never choose this lane group.

## Implementation details

Branch: Fix_SupplyModel

Status: Testing

Details: Current DynaMIT assigns a lane group (and lane in case it a
packet is queuing) to a packet based on its next link and path,
therefore the lane connection adjustments for a closed lane actually
only involves removing outgoing lane connections. The consequence is the
same as removing incoming connections too.