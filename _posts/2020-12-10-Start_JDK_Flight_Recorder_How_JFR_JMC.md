---
layout: default
author: Cameron McKenzie
title: How to start Java Flight Recorder JFR
blurb: Here's how you start Java Flight Recorder and generate a file that profiles your JVM's performance.
---
<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/SzRq99Qy96Y" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<a id="markdown-exercise-2a--starting-a-jfr-recording" name="exercise-2a--starting-a-jfr-recording"></a>
# Starting a JFR Recording

There are various ways to start a flight recording. For this exercise, we will use the
Flight Recording Wizard built into JDK Mission Control.

First switch to the Java perspective. Note that there is an empty project named
Recordings. Next start the DoNothing program by right clicking on the
**DoNothing.launch** file in the **Launchers** folder of the 01_DoNothing project,
as show below.


<img alt="eclipse run do nothing program" class="img-fluid" src="/assets/eclipse-run-do-nothing-program.png"/>


Note: _There are “Auto Record” versions of most launchers, which will launch the_
application and automatically create a recording in the **_autorecordings_** folder in
the tutorial root. This is since, in certain environments (slow machines running a
virtualized Windows for example), the highly loaded JVM that JMC is trying to
communicate with will take so long to getting around to communicate with JMC that
it simply is no fun to wait. _If that is the case, simply run the “Auto” launchers._ Or,

you know, if _you’re lazy. I will not judge._ Just try doing this first exercise without
Auto, as it is about doing recordings from JMC.

## Java Mission Control Perspective


Switch to the Mission Control perspective and select the newly discovered JVM
running the DoNothing class in the JVM Browser. Select Start Flight Recording...
from the context menu. The Flight Recording Wizard will open. Click Browse to find
a suitable location (e.g. the Recordings project) and filename for storing the
recording. Don’t forget to name the recording so that it can be recognized by others
connecting to the JVM, and so that the purpose of the recording can be better
remembered. The name will be used when listing the ongoing recordings for a JVM,
and will also be recorded into the recording itself.

Next select the template you want to use when recording. The template describes the
configuration to use for the different event types. Select the Profiling – on Server
template, and hit Finish to start the recording.


<img alt="eclipse jmc start flight recording" class="img-fluid" src="/assets/eclipse-jmc-start-flight-recording.png"/>
The progress of the recording can be seen in the JVM Browser, when the Flight
Recorder node is expanded. It can also be seen in the status bar.


<img alt="eclipse jmc jvm browser flight recorder node expanded" class="img-fluid" src="/assets/eclipse-jmc-jvm-browser-flight-recorder-node-expanded.png"/>
Use the minute to contemplate intriguing suggestions for how to improve Mission
Control (don’t forget to e-mail them to marcus.hirt@oracle.com), get a coffee, or read
ahead in the tutorial.

Once the recording is done, it will be downloaded to your Mission Control client, and
opened. Switch to the JDK Mission Control perspective.

You should be looking at the automated analysis of the recording.


<img alt="eclipse jmc automated recording analysis do nothing" class="img-fluid" src="/assets/eclipse-jmc-automated-recording-analysis-do-nothing.png"/>

## Start Java Flight Recorder 

This exercise is just to familiarize you with one of the ways to create a flight
recording. This will be a rather boring recording, in terms of results from the
automated analysis, so don’t mind the results of this analysis.

Since the recording was done on a process not doing any actual work, the auto-
analysis didn’t find anything other than that I should probably run less stuff on my
laptop:

1. I am starting to run out of physical memory. I am guessing MS Word ate a
    good portion of it. ;)
2. I have a lot of other processes running aside from the JVM. Since this is my
    laptop, and not a dedicated server, I am not surprised.

The Outline view shows the various pages in the JDK Flight Recorder user interface.
Select Java Application.


<img alt="eclipse jmc application outline view do nothing" class="img-fluid" src="/assets/eclipse-jmc-application-outline-view-do-nothing.png"/>

Here we get an overview of commonly interesting properties of the recording. This
process didn’t do much, but we can see that what little it did was spent transferring
data.

This exercise was mostly to describe how to make a Java Flight Recorder recording, and basic navigation
in the user interface. Once you are done with the recording, remember to shut down
the DoNothing application.




- Either go to the Java perspective and hit enter in the Console view,


<img alt="eclipse java perspective console view" class="img-fluid" src="/assets/eclipse-java-perspective-console-view.png"/>
- ... or go the Debug perspective, find the LoadAndDeadlock process and click the Terminate button


<img alt="eclipse debug perspective terminate" class="img-fluid" src="/assets/eclipse-debug-perspective-terminate.png"/>
Note: Also, remember to close the recording editor window when you are done with a
recording. Recordings contain a lot of information and can consequently use a lot of
memory.


<img alt="eclipse close recording window" class="img-fluid" src="/assets/eclipse-close-recording-window.png"/>
