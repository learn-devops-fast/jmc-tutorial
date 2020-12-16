---
layout: default
author: Cameron McKenzie
title: JVM Heap Waste Analysis in Java Mission Control
blurb: Learn about the new JVM Heap Waste Analysis tool in Java Mission Control and the JVM Flight Recorder.
---

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
# Heap Waste Analysis & Java Mission Control

There is an experimental plug-in available for JDK Mission Control which provides
heap waste analysis. Heap waste analysis aims to find inefficient use of Java heap
memory, and provides suggestions on how to improve the density of an application.

To use the Java Mission Control's Heap Waste Analysis tool, it must usually first be installed. For this JavaOne Hands-on-Lab, however,
it has already been installed into the Eclipse lab environment.

Open the file 11_JOverflow/jmc41dump.hprof by double clicking on it. This is a
dump from an earlier version of Mission Control, which traded quite a lot of memory
for a dubious performance gain in the JMX Console.

<img alt="eclipse jmc joverflow" class="img-fluid" src="/assets/eclipse-jmc-joverflow.png"/>

## JOverflow in Mission Control

Within Mission Control, JOverflow will open, and show the contents of the heapdump. There are four
quadrants in the JOverflow user interface. Also notice the little reset button in the
upper right corner ( ). It will reset all the selections in the user interface.

<a id="markdown-object-selection" name="object-selection"></a>

### JOverflow Object Selection

The top left quadrant, Object Selection, will show you what heap usage anti-patterns
the analysis has found. The first column in the Object Selection table show the kind of
objects found. The second how much memory they use in total. The third column,
Overhead, shows how much of the memory was wasted, in percent of the total heap
used.

<a id="markdown-referrer-tree-table" name="referrer-tree-table"></a>
### Waste Analysis Referrer Tree-table

The top right quadrant contains the Referrer tree-table. This tree-table will show the
aggregated reference chains for whatever is selected. Note that the way to reset the
selections in the Referrer table-tree is to right click in the table. This is since you can
make multiple consecutive selections to arrive at the reference chain you are
interested in.

<img alt="eclipse jmc referer tree" class="img-fluid" src="/assets/eclipse-jmc-referer-tree.png"/>


```
(Screenshot showing multiple available paths to select from)
```
<a id="markdown-class-histogram" name="class-histogram"></a>
### Heap Waste Class Histogram

The lower left in Mission Control's Heap Waste Analysis shows a class histogram for whatever is selected, allowing you to filter
on class. If you want to reset your selection, click the button representing the selection
you have made.


<img alt="eclipse jmc reset class histogram" class="img-fluid" src="/assets/eclipse-jmc-reset-class-histogram.png"/>


<a id="markdown-ancestor-referrer" name="ancestor-referrer"></a>
### JOverflow Heap Ancestor Referrer 

The final table, in the lower right, will show the objects grouped by the closest
ancestor referrer. It provides a pie chart to show the memory distribution, and filter
box, making it easy to home in on to instances of classes belonging to specific
packages.

<img alt="eclipse jmc ancestor referer" class="img-fluid" src="/assets/eclipse-jmc-ancestor-referer.png"/>


Note: it is possible to directly select a piece in the pie chart.

<a id="markdown-exercise-13--reducing-memory-usage" name="exercise-13--reducing-memory-usage"></a>
### Reducing Sparse Array Memory Usage

It seems that quite a few objects used by this old version of Java Mission Control, are Sparse Arrays.
This means that there are arrays with very few actual instances referenced to from
them. In other words, they are mostly empty.

- How much memory (in percent of the total heap used) would be saved if the
    JDK Mission Control 4.1 JMX Console switched to a more compact
    representation?
- How many instances are holding on to all that memory?
- What is the name of the field holing on to those instances?
- Can you, just by looking at the names in the reference chain, figure out how
    these sparse arrays were used?


<a id="markdown-jcmd-java-command-bonus" name="jcmd-java-command-bonus"></a>