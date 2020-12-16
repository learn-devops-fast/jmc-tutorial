---
layout: default
author: Cameron McKenzie
title: Performace Profile JavaFX Apps with Flight Recorder JFR JMC
blurb: Learn how to profile your JavaFX apps and identify performace problems with Java Flight Recorder and JDK Mission Control
---

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/DM8hiMrQB7g" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<a id="markdown-exercise-7-bonus--javafx" name="exercise-7-bonus--javafx"></a>
# JavaFX, JVM Flight Recorder and Mission Control

In this exercise, we will explore the Java FX integration with JDK Flight Recorder.
Use the GUIMark launcher to launch the GUIMark Bitmap benchmark application.
You should see a tower shooting a laser at monsters.

<img alt="javafx application lasers" class="img-fluid" src="/assets/javafx-application-lasers.png"/>

We will use a pre-recorded recording for this exercise,
**06_JFR_JavaFX/guimark.jfr** , so you starting GUIMark was mostly pointless.
But, come on – lasers? Monsters? It had to be seen.

## Run GUIMark in Flight Recorder

Note: If you insist on having a locally produced recording, it is better to run the
GUIMark Auto Record launcher. If you insist on not using the auto recording
launcher, make sure to enable the JavaFX events in the recording wizard, or import
the template in the project folder.


<img alt="eclipse jmc jfr javafx" class="img-fluid" src="/assets/eclipse-jmc-jfr-javafx.png"/>

### JavaFX Performance Profile
Try looking at the recording using the special Java FX page. Can you tell which pulse
took the longest time (disregard the weird pulse 0)? What phase was the one that took
the longest for that particular pulse? Which was the input event that took the longest?


<img alt="eclipse jmc jfr javafx pulse" class="img-fluid" src="/assets/eclipse-jmc-jfr-javafx-pulse.png"/>

<a id="markdown-exercise-8-bonus--exceptions" name="exercise-8-bonus--exceptions"></a>