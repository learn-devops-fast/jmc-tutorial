---
layout: default
author: Cameron McKenzie
title: JDK Mission Control Introduction and Overview
blurb: Here's how to get started with Java Mission Control and the Flight Recorder. It's a quick introduction to JMC and JFR, but it will get you started with performance profiling and JDK troubleshooting.
---

### Setting up Eclipse
<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/AHT4ZvOe6a4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
## Installing Mission Control

To do the exercises in this tutorial, you must first install Eclipse and Mission Control.


```
https://github.com/thegreystone/jmc-tutorial
```

In this repository you will also find the files and code required to complete the
tutorial.

## Starting JDK Mission Control

There are two separate ways of running JDK Mission Control available: as a stand-
alone application or from within Eclipse.

This exercise shows you how to start both the stand-alone and the Eclipse plug-in
versions of JDK Mission Control.

<a id="markdown-exercise-1a--starting-the-stand-alone-version-of-jmc" name="exercise-1a--starting-the-stand-alone-version-of-jmc"></a>
### The Stand-Alone Version of JMC and JFR

Go to the directory where you installed the stand-alone version of JMC. In the bin
folder, you will find a jmc launcher. Either double-click it or run it from the command
line. A splash screen should show, and after a little while you should be looking at
something like this:

<img src="/assets/jmc-welcome-screen.png" class="img-fluid" alt="JMC Java Mission Control Welcome Screen"/>


The welcome screen provides guidance and documentation for the different tools in
JDK Mission Control. Since you have this tutorial, you can safely close the welcome
screen.

<img src="/assets/jmc-welcome-screen-close.png" class="img-fluid" alt="Close Mission Control Welcome Screen"/>


Closing the welcome screen will show the basic JDK Mission Control environment.
The view (window) to the left is the JVM Browser. It will normally contain the
automatically discovered JVMs, such as locally running JVMs and JVMs discovered
on the network.

<img src="/assets/jmc-start-screen.png" class="img-fluid" alt="JMC Start Screen"/>

### Java Mission Control Introduction

To the bottom left is the Properties view, showing properties for anything selected in
the editor.

Behind the Properties view is the Results view, which shows the results from the
automated analysis relevant to the currently opened page in the editor.

Below the editor area is the Stack Trace view, which shows the aggregated stack
traces for anything selected in the editor.

To launch the different tools, simply select a JVM in the JVM Browser and then
select the appropriate tool from the context menu. For example, the Management
Console can be started on a JVM by selecting the JVM in question in the JVM
Browser and selecting Start JMX Console from the context menu.

In the JVM Browser, the JVM running Mission Control will be shown as The JVM
Running Mission Control.

Since we will be running the tutorial from within Eclipse, please shut down (⌘
+Q on Mac, alt+F4 on Windows) the stand-alone version of JDK Mission Control.