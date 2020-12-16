---
layout: default
author: Cameron McKenzie
title: Java Mission Control Tutorial
blurb: Learn how to profile your JVM and fix Java performance issues with Java Mission Control and Flight Recorder.
---

# JDK Mission Control Tutorial
<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
This tutorial provides plenty of examples and material to help you learn JDK Mission Control (7+).

## Preparations
Since it is not practical to pre-package everything required to run the material here at GitHub, there are some preparations required before starting the Tutorial.

### Setting up the JDK
You will need to have a JDK 11 or later to do this tutorial. You can either use the [Oracle JDK](http://java.oracle.com) or any OpenJDK build, for example the one provided by [Oracle](http://jdk.java.net/11/).

You will need to ensure that `java` for your JDK is on your path, and you should also make sure that your JAVA_HOME variable is set to the parent folder of the `bin` folder containing your `java` binary.

### Getting the stand alone version of JMC
The open source version of JMC has not been released yet, but early access builds can be downloaded from here:
http://jdk.java.net/jmc