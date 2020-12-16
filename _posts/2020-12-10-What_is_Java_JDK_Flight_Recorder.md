---
layout: default
author: Cameron McKenzie
title: What is the Java JDK Flight Recorder?
blurb: What exactly is the Java Flight Recorder? Like the black box in an airplane, the JDK Flight Recorder continuously aggregates data.
---
# What is the Java Flight Recorder?
<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
The JDK Flight Recorder (JFR) is the main profiling and diagnostics tool in JDK
Mission Control. Think of it as analogous to the "black box" used in aircraft (FDR, or
Flight Data Recorder), but for the JVM. 

## JDK Flight Recorder Explained


The recorder part is built into the HotSpot
JVM and gathers data about both the HotSpot runtime and the application running in
the HotSpot JVM. The recorder can both be run in a continuous fashion, like the
"black box" of an airplane, as well as for a predefined period of time. For more
information about recordings and ways of creating them, see
[http://hirt.se/blog/?p=370.](http://hirt.se/blog/?p=370.)