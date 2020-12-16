---
layout: default
author: Cameron McKenzie
title: Java Mission Control Introduction and Overview with Eclipse
blurb: Here's a quick introduction to Java Mission Control and the JVM Flight Recorder tool.
---
<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<a id="markdown-exercise-1b--starting-jmc-in-eclipse" name="exercise-1b--starting-jmc-in-eclipse"></a>

# Introduction to Java Mission Control in Eclipse

First make sure that you followed the instructions in the README.md file in the root
of the GitHub repository to the letter, and that the JMC plug-ins are installed Next
start Eclipse and switch to the Java perspective. You should now see something
looking somewhat like below:


<img src="/assets/eclipse-java-perspective.png" class="img-fluid" alt="JMC Eclipse Java Perspective"/>

First we will need to verify that the JDK 11 runtime is properly configured and
available for Eclipse to use.

1. Open the Preferences (Eclipse | Preferences... on Mac OS X, Window |
    Preferences... on Windows).
2. In the filter box in the upper left of the Preferences dialog, type JRE, then
    select Installed JREs.


<img src="/assets/eclipse-preferences-installed-jres.png" class="img-fluid" alt="Java 11 for Java Mission Control Recorder"/>

3. If you already have various JDKs installed, they may already show up here. If
    they don’t, click add to add them. There is a JDK 11 provided in the HoL zip.

```
Note: when adding a JRE on Mac, select Mac OS X VM. Also note that you
should browse to the <JDK>/Contents/Home folder.
```
4. Ensure that your JDK 11 is the default by checking the checkbox next to it.

5. Ensure that your execution environments are correctly mapped for JDK 8.

<img src="/assets/eclipse-preferences-execution-environments.png" class="img-fluid" alt="Eclipse preferences Java Flight Recorder"/>

```
Don’t forget to click Apply and Close when done.
```

## Java Mission Control and Eclipse


Next we will have to import the projects with all the examples into the workspace.

1. Select File | Import... from the menu.
2. In the Import dialog, select Existing Projects into Workspace and hit Next.


<img src="/assets/eclipse-import-existing-projects.png" class="img-fluid" alt="Eclipse Mission Control Projects Import"/>

3. Browse to the projects folder in the root tutorial folder and click Open.

4. Select all projects and click Finish.


<img src="/assets/eclipse-import-tutorial-all-projects.png" class="img-fluid" alt="Eclipse JMC JFR tutorial projects"/>

You should now see something similar to the following:

<img src="/assets/eclipse-workspace-projects-loaded.png" class="img-fluid" alt="Java JMC JFR projects loaded"/>

### Eclipse Java Mission Control Perspective

To the left the projects for the different exercises can be seen. In Eclipse a
configuration of views is called a perspective. There is a special perspective
optimized for working with JMC, called the JDK Mission Control perspective. To
open the JDK Mission Control Perspective, click the Mission Control perspective in
the upper right corner of Eclipse.


<img src="/assets/eclipse-jmc-perspective-button-toggle.png" class="img-fluid" alt="Eclipse Mission Control Perspective"/>

In this tutorial, you will be constantly switching between the Java perspective, to look
at code and to open flight recordings, and the Mission Control perspective, to access
the JVM browser and optimize the window layout for looking at flight recordings.

As can be seen from the picture below, the JVM running Eclipse (and thus JDK
Mission Control) will be named The JVM Running Mission Control, just like in the
stand-alone version of JDK Mission Control.


<img src="/assets/eclipse-jmc-perspective-jvm-browser.png" class="img-fluid" alt="Eclipse Mission Control JVM browser"/>

## Start JVM Flight Recorder in Eclipse

Launching the tools work exactly the same as in the stand-alone version. Either use
the context menu of the JVM that you wish to launch the tool on, or click the Mission
Control button on the toolbar to launch a Wizard.


<img src="/assets/eclipse-jmc-launch-wizard-jfr.png" class="img-fluid" alt="Java Flight Recorder Launch Wizard"/>

The Java perspective is the perspective with a little J on the icon:

<img src="/assets/eclipse-java-perspective-button-toggle.png" class="img-fluid" alt="Eclipse Java perspective button toggle"/>

Go back to the Java perspective, so that you can see the projects in the Package
Explorer view again.

<a id="markdown-the-jdk-flight-recorder" name="the-jdk-flight-recorder"></a>