---
layout: default
author: Cameron McKenzie
title: How to Create Custom Flight Recorder Events for Java Mission Control
blurb: Learn to quickly create custom Flight Recorder events for analysis in Java Mission Control.
---

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
# Create Custom Events for Flight Recorder

In this custom events for JFR exercise we will use an example from a different repository – the java-svc
repo. Clone the following repository:

```
https://github.com/thegreystone/java-svc
```
Follow the instructions to build the application which uses custom Flight Recorder events. Make sure you use a JDK 11 or later.

Open a command line and go to the **java-svc/jfr** folder.

Next run target/bin/runFibonacci.

## View custom Flight Recorder events

Connect to the process with JMC. The process starts with a recording already running,
so you can simply dump the whole thing when you feel ready. Either let it run for a
few minutes and then dump it, or go with the pre-recorded recording present in the
09_JFR_CustomEvents project.

Open the Threads view. Sort on Thread Groups and shift-click to select the two
threads in the Fibonacci thread group:


<img alt="eclipse jmc jfr fibonacci threads" class="img-fluid" src="/assets/eclipse-jmc-jfr-fibonacci-threads.png"/>

### Inspect custom Mission Control events


Right click on the graph and enable the viewing of other event types in a separate lane
per thread:
<img alt="eclipse jmc jfr fibonacci threads other event types" class="img-fluid" src="/assets/eclipse-jmc-jfr-fibonacci-threads-other-event-types.png"/>


You can now hover over the events to see what they contain.

### Custom Flight Recorder Events Example Exercises

8. How long did it take to calculate the longest Fibonacci number? How long did
    it take to calculate the shortest one?

```
Hint: Go to the Event Browser, click on the Fibonacci Event. Sort on
Duration.
```
9. Verify that the iterative version is not cheating by making sure that the
    calculation of both the iterative and recursive version of the algorithm come to
    the same value.

```
Hint: Go to the Event Browser, click on the Fibonacci Event. Sort on
Fibonnaci Number.
```
10. Did you notice any difference in performance between the two algorithms?


<a id="markdown-exercise-10--custom-rules-bonus" name="exercise-10--custom-rules-bonus"></a>