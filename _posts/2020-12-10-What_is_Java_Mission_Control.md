---
layout: default
author: Cameron McKenzie
title: What is Java Mission Control?
blurb: Wondering what Java Mission Control is? Here's a quick explaination for you, along with insight on how to get started with Java and JDK performance monitoring.
---

# What is Java Mission Control?
<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
JDK Mission Control is a suite of tools for monitoring, profiling and diagnosing
applications running in production on the HotSpot JVM.

## Java Mission Control Features

JDK Mission Control mainly consists of two tools at the time of writing:

- The JMX Console – a JVM and application monitoring solution based on
    JMX.
- The JDK Flight Recorder – a very low overhead profiling and diagnostics tool.

There are also plug-ins available that extend the functionality of JDK Mission Control
to, for example, perform heap waste analysis on heap dumps.

### Java Mission Control Tutorial 

This tutorial will focus on the JDK Flight Recorder part of JDK Mission Control, with
bonus exercises for the heap dump analysis tool (JOverflow) and the JMX Console
towards the end.

JDK Mission Control can be run both as a stand-alone application and inside of
Eclipse. This tutorial can be used with either way of running Mission Control.