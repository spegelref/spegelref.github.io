---
layout:   post
title:    Oil Dilution Graph
category: ee20
tags:     cars subaru ee20
---

# Oil Dilution Graph

contains a complete DPF active regeneration process – the rising section
(750 seconds duration = 12.5 minutes).

Basically, oil dilution is driven by:

1. post-injections during active DPF regeneration
2. estimated diesel fuel evaporation

According to internal algorithm and logged data, normal operation does not
increase dilution. Oil dilution slowly decreases as the ECU estimates fuel
evaporation out of engine oil. (On Euro 4 at least, this algorithm is also
running if ignition is on, engine not running but coolant temperature warm
enough).

Active regeneration however uses one or more post-injections (small additional
late injections – during exhaust stroke) in order to heat up the DPF, raising
oil dilution amount, at much higher rate therefore winning over evaporation.

Notice these short intermittent steps during 
regeneration—these are caused by coasting—ECU suspending all injections, 
including post-injections.

Wouldn’t coasting cool down the DPF then by pushing rather cold air through the
system? To mitigate this, the software fully opens EGR valve (70 deg). As soon
as injections resume, EGR valve is being closed again. Normally, during active
regeneneration it is in fully closed position (0 deg) helping to increase
exhaust temperature (more oxygen).

If you look carefully, you can spot more evaporation going on after
regeneration had finished compared to before it started. This is mainly due to
higher engine temperature, having reached normal operating conditions of
around 90 °C. For evaporation to get going it needs temperatures beyond 30 °C,
the higher the better.

Also take a look at post “Estimated Distance to Oil Change” for additional
information.
