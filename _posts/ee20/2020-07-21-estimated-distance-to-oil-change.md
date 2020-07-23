---
layout:   page
title:    Estimated Distance to Oil Change
category: ee20
tags:     cars subaru ee20
---

Estimated Distance to Oil Change
Posted on October 18, 2010 by subdiesel | 2 Comments

Estimated distance to oil change is directly driven by oil dilution ratio. Confirmed in several Boxer Diesel ROMs, Euro4 and 5. It uses table interpolation, however the table data makes up this perfectly linear relationship:

DistanceToOilChange[km] = 15000 - 1500 * OilDilutionRatio[%]

Note that the logging parameter Oil Dilution Ratio [%] (SSM2 0x00027C, x[%]) does not report decimal places. Original RAM value however is a 32-bit floating point variable so if you log this one you can spot slight changes. Distance to oil change cannot get negative because interpolation subroutines don’t extrapolate.

Of course both oil dilution ratio and distance to oil change should be considered rough estimations. So far all Subaru control units cannot measure dilution, there’s no suitable sensor attached. Such dilution sensors do exist but add costs, especially development and (reliability) testing. As a result of missing sensor, the ECU must be told to reset oil dilution value when engine oil has been replaced – see Engine Oil Change (DPF models).

10 % oil dilution is critical where ECU will flash DPF light, also stores DTC P1468 Oil Dilution.

We know the oil dilution algorithm in detail and are able to debug issues. Basically, oil dilution gets to increase while active DPF regeneration is being performed. Otherwise it will drop (very) slowly as the ECU estimates oil evaporation. As you might expect, evaporation rate depends on (coolant) temperature, the higher the better.

Articles regarding oil dilution:

    http://www.biodieselmagazine.com/articles/2290/understanding-the-post-injection-problem/
    http://www.1st-in-synthetics.com/articles/fuel_dilution_surfaces_as_issue_in_some_modern_diesel_engines.htm
