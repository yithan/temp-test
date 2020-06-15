This section provides some additional annotations to DynaMIT supply
models and proposes some improvements, mainly to address the "single
output capacity" issue, the "over-sized queue spill-back" issue, and the
"capacity based incident" issue. In addition, this version inherits the
solution for the "short segment queuing" issue (originally proposed in
ZhengWei's thesis, a.k.a. Beijing paper, then enhanced by followers).

## Mesoscopic supply model

In our virtual mesoscopic world, vehicles move like particles within a
complex pipe system. The general simulation process are described in
"Models and Algorithms, section 4.1 - 4.3" (See
[Beginners_Guide](Beginners_Guide "wikilink")), which includes:

  - Overall simulation process such as processing order of road
    segments, the advance and update phases, etc
  - Speed model, deterministic queue model, and movement model
  - The flow chart of advancing a vehicle, which is modeled as a finite
    state machine.

However, some vital concepts are not explained in detail in that
document, such as the constraints for a vehicle to move a new segment
(e.g., how capacities work in detail). Here we'll explain them, trying
to establish some basic laws that must hold during simulation. We want
to make sure that, given the assumptions, the models and constraints
statisfy necessary conditions for being "correct" (e.g., no violation of
physical constraint, etc.). We will also propose improvements to the
constraints, which are highlighted in <font color="blue">blue</font>.

  - Assumptions

<!-- end list -->

1.  Let's assume each segment has only one lane group (for simplicity)
    until lane groups are introduced, and capacities (output or
    accpetance) are specified at segment level. With the presence of
    multiple lane groups per segment, we just need to apply the capacity
    concept to "lane group" level.
2.  When traffic signals are enabled, output capacities can be obtained
    or calibrated for each lane group.

<!-- end list -->

  - Moving

<!-- end list -->

1.  Vehicles moves in strict order, meaning a vehicle in front of
    another (of the same segment) always moves first, and the one behind
    it never overtakes when they're in the same segment. The speed of a
    vehicle is defined by speed-density function. The speed is
    calculated every simulation minute (assuming the update interval
    length is one minute throughout this article).
2.  When a vehicle is moving, it's NOT associated with any lanes (but it
    belongs to one and only one lane group), but as mentioned later, it
    will contribute to the (output) capacity of only one direction when
    it moves out of a segment.

<!-- end list -->

  - Crossing segment boundaries

<!-- end list -->

1.  If a vehicle (moving towards next link *nlink*) can reach the end of
    this segment before the end of this advance interval (based on speed
    and determinstric queuing model), then it can move to next segment
    only if both output and acceptance capacity requirements are met.
2.  Requirements for output capacity:
    1.  If current segment is the last one in its parent link:
          - <font color="blue">Sum( passed_vehicles_towards_*nlink* )
            \<= Sum( C_out of each_lane_connecting_*nlink* ),
            AND</font>
          - Sum( passed_vehicles_for_entire_segment ) \<= Sum (
            C_out of every_lane )
    2.  Otherwise,
          - Sum( passed_vehicles_for_entire_segment ) \<= Sum (
            C_out of every_lane )
3.  Requirements for acceptance capacity (of next segment):
    1.  The physical constraint must not be violated:
          - <font color="blue">If at least one target lane (the one that
            conforms with vehicle's path) has a queue, there should be
            at least one empty slot in any target lanes.</font>
          - Otherwise, there should be at least one empty slot in the
            entire segment.
    2.  The rate defined by C_acc of <u>next segment</u> should not be
        violated (by comparing its arrival time w.r.t. that of the most
        recent entered vehicle), where C_acc is:
          - If next segment has no queues at all, *C_acc = C_mov = 1/w
            \* (n \* V_u / L )*
          - Otherwise, *C_acc = min(C_out, C_mov)* (see detailed
            explanations in 'annotations' section)
    3.  The fact that C_acc is the rate per segment implies that, if
        upstream segments supply more than acceptable vehicles to
        downstream segment, the max accept rate is always fully
        utilized.

<!-- end list -->

  - Queuing

<!-- end list -->

1.  If vehicle couldn't proceed to next segment due to output or
    acceptance violation, it will start (or join, or moves within) a
    queue in current segment. Note because of the acceptance constraint,
    the output capacity of current segment may not be reached when a
    queue forms.
2.  A vehicle is queuing in a specific lane. The lane must be connected
    through a series of lane connections to the desired downstream link
    in vehicle's path.
3.  Among all lane candidates, the vehicle chooses to queue in the one
    with shortest queue length.

<!-- end list -->

  - Traffic signal modelling

<!-- end list -->

1.  Traffic signals are not modeled as time (or phase) based in
    mesoscopic world, which is too hard to fit into the proposed
    systems.
2.  Instead, traffic signals are modeled by segment output capacities,
    or more precisely, lane group capacities (which are calibrated based
    on the traffic light schedule of each junction). Different lane
    groups may be created to distinguish different capacities for
    different turning directions.
3.  The acceptance capacity formula should be adjusted when traffic
    signals are enabled, C_acc = min(C_out_before_ts_adjusted,
    C_mov).

<!-- end list -->

  - Incident modelling

<!-- end list -->

1.  The existing incident model is to apply capacity reduction of the
    affected segment.
2.  The capacity based incident model implies that reductions are
    applied uniformly to each lane group of the segment, regardless of
    downstream directions.
      - With the old capacity constraints, once output capacities are
        reached, queues start to form in every lane (due to single
        output capacity per segment) of the incident-affected segment,
        and as time goes by it will lead to 'full density' in incident
        segment and possibly upstream segments (over-sized queue will
        start to form due to the old acceptance constraint), until
        incident is cleared.
      - With the new capacity constraints (those in blue),
        oversize-queue will no longer occur. Since output capacities are
        direction-based, it's also possible that queue propagation will
        be restricted to a subset of lanes of the incident segment and
        upstream segments, while traffic on other directions are still
        moving. Note due to the nature of capacity-based queuing model,
        the 'full density' problem could never be fully solved.
3.  The capacity based incident model implies that incident always
    occurs at the end of the segment, effectively.
4.  Finer incident models are also being considered:<font color="blue">
      - Lane-based capacity reduction approach. If the incident is
        happening on a lane that affects traffic towards only one
        specific downstream link, traffic towards other directions may
        be less affected by the incident.
      - Lane-closure and speed limit approach. A lane that is
        effectively closed due to incidents should transfer its
        connectivity to its neighboring lane(s). The detailed proposal
        is discussed in [Dynamic-segment based incident
        modelling](Dynamic-segment_based_incident_modelling "wikilink")</font>

<!-- end list -->

  - Lane groups

<!-- end list -->

1.  At any time, a vehicle belongs to one (and only one) lane group per
    segment. When a vehicle is moving, it's NOT associated with any
    specific lane (but treated at lane group level). When it starts
    queuing, it queues in a lane. Lane change behavior doesn't apply
    here.
2.  Speed (of moving part) is calculated per lane group. All vehicles in
    the same lane group have the same speed within the update interval.
3.  Which lane group a vehicle resides in depends on its path:
      - Whenever a vehicle enters a new segment, it must reside in a
        lane group that is connected via a series of lane connections to
        the next link in its path. <font color="blue">The lane group
        with shortest average queue length per lane is selected. It
        resides in that lane group until reaching the end of the segment
        unless it updates its path (en-route) and that requires it to
        move to a different lane group.</font>
      - Whenever a vehicle starts queuing, it must queue in a lane that
        is connected via a series of lane connections to the next link
        in its path.The lane with shortest queue is selected. It resides
        in that lane until reaching the end of the segment. It's not
        eligible for en-route path decisions when it's queuing.
      - When a vehicle enters a new segment (no matter whether in the
        old segment it was in moving or queuing state), it *jumps* to
        the selected lane group in the new segment.
        <font color="blue">Lane connections between original and new
        lane groups must be respected.</font> However, if in the new
        segment it starts queueing immediately, the connection between
        the new lane and original lane is not respected.
4.  <font color="blue">When a vehicle switches to a new lane group
    (either in-between or within segments), the target lane group must
    have at least one space to accept it (same acceptance check as
    described in "crossing segment boundaries" at lane group level. With
    one exception, it should use segment accpetance rate rather than
    acceptance rate of selected lane group, in order to fully utilize
    max accptance rate whenver possible.</font>

<!-- end list -->

  - En-route path update

<!-- end list -->

1.  <font color="blue">When a vehicle just moves into a new segment and
    it is moving, it is eligible for en-route path decisions.</font>
2.  Will speed-density relationship be invalidated if too many vehicles
    switch to a different lane group en-route?
3.  For ClosedLoop DynaMIT estimations / predictions (with od interval
    of 5 minutes), whether en-route path choice is still necessary is to
    be thought about.

<!-- end list -->

  - Virtual queue

<!-- end list -->

1.  When a vehicle is eligable for moving out, but downstream segment
    (only happens when it's in a new link) hasn't been processed, it's
    temporarily add to the 'virtual queue' of that link which will be
    processed later in the advance phase.
2.  <font color="blue">The size of virutual queue of a link is updated
    every advance interval, and is set to the number of empty slots in
    the first segment of that link.</font> This guarantees free space
    constraint will always hold but it may suffer from same grid-lock
    problems experienced by short segments.

<!-- end list -->

  - Loading

<!-- end list -->

1.  During every advance interval, new packets are loaded after the
    entire road network have been processed. This implies new vehiles
    entering road have lower priorities than those already on the
    network. This may cause starvation for new vehicles.

## Annotations to the supply model

  - Output and acceptance capacities (annotations to **crossing segment
    boundaries**)

<!-- end list -->

1.  Definition
      - A segment (or more precisely, a lane) has a maximum discharging
        rate of vehicles. For example, 10 vehicles moving out of a lane
        within 1 second is not realistic. When a vehicle is moving out
        of a segment, it can not violate the discharging rate. We define
        the maximum number of vehicles that can move out of a segment
        per second as its **output capacity**.
      - When a vehicle is moving into a new segment, at the time it
        arrives at segment boundary, there must be enough physical space
        to accept it. In addition, even when there're enough spaces
        available, there's a maximum rate at which the downstream
        segment can accept arriving vehicles (imagine 10 vehicles from
        different upstream segments arriving at this segment at almost
        the same time). We define the maximum rate at which a vehicle
        can move into a segment as its **acceptance capacity** or
        **acceptance rate**.
      - Capacities should only reflect the "realistic" maximum rate
        which only depends on the characteristics of (mostly the tip of)
        a road, for example, pavements, slopes, curvatures, presence of
        stop-lines or give-way signs, or even weather conditions (which
        may affect other supply parameters as a whole), and traffic
        signals (for output capacity only). Output capacity should
        correspond to the segment max-flow rate, and in speed-density
        model, once the supply parameters are fixed, the max flow is
        fixed, therefore is output capacity redundant? In this scenario
        (where all vehicles are moving) it seems yes, but in other
        scenarios, for example, when there're queues, or in the presence
        traffic signals and other cases like incidents, output
        capacities are necessary. In fact, output capacity also applies
        when a segment only has a moving part too, overriding the
        max-flow rate determined by the speed-density function, thus it
        behaves as a final guarantee in case other supply parameters are
        mis-calibrated which could leads to unrealisticly large flows.
2.  Granularity
      - One question is at what granularity do capacities apply? Output
        capacities are applied on a per-minute basis, and acceptance
        capacities are checked at the finest level of detail, meaning
        when every vehicle moves to next segment we ensure that the time
        difference from the previous incoming vehicle's arrival time is
        not breached.
      - Since output capacities are controlled on a per-minute basis,
        when the capacity of a segment is reached, no vehicles can move
        out during the remaining time of that minute, and a **queue**
        will start to form in each lane. In the next minute, the queues
        will be discharged at the rate as specified by the output
        capacity. This ensures that output capacities hold for both
        queuing or moving conditions.
3.  Direction
      - Do we check capacities segment-wise or on a per-lane basis? In
        the new supply model, output capacities are checked on
        "per-direction" basis or segment-wise basis, depending on its
        location in the link. On the acceptance checks, available space
        is checked either against entire segment or against every target
        lane, depending on the existance of queues in the target lanes.
        Acceptance rate is calculated based on entire segment and is
        checked against every vehicle entering the segment.
      - Segment-based output capacities don't care whether a vehicle is
        going straight or is making a turn. It means when a vehicle
        moves out of a segment, regardless of its direction, output
        counter is incremented unitl segment capacity is reached and no
        more vehicles can move out. One devil with this approach arises
        when there're turning-exclusive lanes (NOT shared turning
        lanes). Imagine a segment has an exclusive right-turn lane, and
        there's far more straight traffic in front of right-turn
        vehicles, what happens next is not going to be good.
      - Direction-based output capacities, on the other hand, avoid this
        problem. Lane groups can solve the problem too. However,
        creating lane groups is a manual task and is based on
        professional experiences (which means a lot of work for complex
        road networks), and direcitonal approach provides the ability to
        avoid the problem for a network without lane groups (by default,
        DynaMIT network file doesn't mandate lane groups in the sense
        that if they're not present, there's a single lane group per
        segment). In fact, the directional output capacities are
        implemented inside lane group rather than segment, and its
        purpose is to complement lane groups rather than replacement.
      - Currently direction-based approach only applies to last segment
        of a link. The question is, should we enable it for remaining
        segments? Keep in mind that one main purpose of output capacity
        is to act as a constraint for incidents or traffic signals.
4.  Acceptance capacity formula:
      - w is a scaling constant, w \>= 1, (interpretation: per each lane
        on average every w vehicle length there's one vehicle)
      - n is number of lanes
      - V_u is speed of moving part
      - L is mean packet length
      - Interpretation: C_out is the output capacity defined by the
        physical constraint of the segment, in principle this would also
        be the upper bound of acceptance capacity. However, due to the
        grid lock problem, we want to breach this limit and use a higher
        acceptance rate <u>when there's no queue</u>. By setting w to a
        small number (say 1.5), C_mov (C_mov \> C_out) is used
        instead. If there are queues, we want acceptance capacity to
        adhere to the physical limit C_out, unless C_mov is smaller
        (which could never happen if w is small) then C_mov is used.

<!-- end list -->

  - Lane connections (annotations to **queuing**)

<!-- end list -->

1.  Lane connections are designed to represent road network
    connectivities. At the same time, they can also be used to represent
    lane changes possibilities in-between segments.
2.  Lane connections at junctions should follow the real world exactly.
3.  Lane connections in-between segments of the same link, we should
    <u>generally</u> connect the lane to the matching downstream lane
    and the neighbouring downstream lanes (if any). In the case of lane
    splitting or merging, more connections may be desired. This models
    the lane change possibilities in-between segments.

<!-- end list -->

  - Lane groups

<!-- end list -->

1.  Lane groups provide finer level of control over traffic, espcially
    for traffic on different directions.
      - model differences for different turning movements at
        intersections, especially signalized intersections.
      - model geometry change between to segments, or model a double
        while line within a segment that makes lane change impossible.
      - finer level of control for segments in the beginning or middle
        of a link.
2.  Lane groups of a segment are disjoint.
3.  Lane groups are not turning groups, meaning lanes within a lane
    group could potentially connect to multiple downstream links. If a
    lane has multiple turnings, due to the fact that capacities are
    directionless, vehicles going in one direciton may block the entire
    lane, just like the real world.
4.  Albeit the benefits, creating too many lane groups per segment may
    not be good either (e.g., one lane group for each lane). We still
    want to capture the general moving properties as a whole so that the
    moving model makes more sense statiscally.
5.  Lane group creation guidelines:
      - For segments upstream of an intersection, neighbouring
        exclusive-turning lanes towards the same direction are advised
        to be grouped, and neighbouring shared turning lanes should be
        treated on a case-by-case mannar. An exception is with
        signalised juctions describled later.
      - For segments downstream of an intersection, neighbouring lanes
        that has a single upstream link are advised to be grouped,
        others case-by-case treatment.
      - For other segments, if it represents a lane split from upstream
        segment and the new lane is connected to a downstream
        turning-exclusive lane at a intersection, it is advised to
        create a separate lane group for that lane.
      - For segments upstream of signalised junctions, a straight-only
        lane and a neighbouring straight-and-right-turn lane should be
        separated in two lane groups, which is for easy calibration of
        different capacities. This is for the situation of left-side
        traffic, for example, Singapore or UK.
      - Otherwise, case-by-case treatment.

<!-- end list -->

  - Limitations of current supply model

<!-- end list -->

1.  It seems hard to represent varying road network structure, such as
    bus lanes, overnight parking lanes, etc.
2.  Virtual queue size, and lack of topological sort to minimize the
    need for virtuals.
3.  Capacity based incident modelling.
4.  En-route path update may invalidate density of a lane group.

## Implementation of proposed enhancements

Code branch: Fix_SupplyModel.

Status: Testing.

Not all proposed features are implemented, some are still under
discussion. Below lists the changes we have made:

1.  New acceptance capacity check described in 'Crossing segment
    boundaries : section 3.1' is implemented in function *canGoTo*
2.  Set link virtual queue size (every advance step) to be the number of
    empty spaces of its first segment at the beginning of advance step.
3.  Default parameter values:
      - Mean packet length = 6 (meters)
      - w = 1
      - queue discharge rate = C_out instread of 3\*C_out
4.  For ramp type segments, Vmin = 6 m/s (21.6 km/h).

Another enhancement made is in the incident modelling, please refer to
[Dynamic-segment based incident
modelling](Dynamic-segment_based_incident_modelling "wikilink").