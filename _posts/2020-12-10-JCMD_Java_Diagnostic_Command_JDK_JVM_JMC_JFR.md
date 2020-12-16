---
layout: default
author: Cameron McKenzie
title: JCMD Tutorial
blurb: Learn how to use the JCMD Java Diagnostic command through examples in this tutorial.
---

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

# JCMD (Java CoMmanD) Tutorial



This exercise will explain the basic usage of the JDK command line tool jcmd. You
can find it in the JDK distribution under **JDK_HOME/bin**. It will already be on the
path if you open the command line interface by double clicking
**C:\Tutorial\cmd.exe**. 

Start any Java application. If you already have Eclipse or the stand-alone version of
Mission Control running, you are already running one and can skip this step.

Next open a terminal. At the prompt type **jcmd** and hit enter. Assuming you have
jcmd on your path, this will list the running java processes and their Process IDs
(PID). If not, either add it to your path, or specify the full path to
**JDK_HOME/bin/jcmd**. Since jcmd uses Java, and it is running, it will list itself as
well.

## Java Diagnostic Command JCMD 

The jcmd uses the PID to identify what JVM to talk to. (It can also use the main class
for identification, but let’s stick with PID for now.) Type **jcmd <PID> help** , for
example **jcmd 4711 help**. That will list all available diagnostic commands in that
particular Java process. Different versions of the JVM may have different sets of
commands available to them. If <PID> is set to 0, the command will be sent to all
running JVMs.

Attempt to list the versions of all running JVMs.


## JCMD Example Exercises

21. Start the Leak program. Use the **GC.class_histogram** command. Wait
    for a little while, and then run it again. Can you find any specific use for it?
22. You decide that you want your friend to access a running server that has been
    up for a few days from his computer to help you solve a problem. Oh dear,
    you didn’t start the external agent when you started the server, did you? Can
    you find a solution that doesn’t involve taking the server down?

```
Note: If you want to try the solution without specifying keystores and
certificates, make sure you specify jmxremote.ssl=false
jmxremote.authenticate=false. Also, specifying a free port is considered good
form. Using jmxremote.ssl=false
jmxremote.authenticate=false jmxremote.port=4711 should be
fine.
```
23. Could you start flight recordings using jcmd? How?

Note: Have you noticed that there is a very similar feature set available from the
Diagnostic Commands discussed in Exercise 10 .b and jcmd. As a matter of fact,
everything you can do from jcmd you can do using the DiagnosticCommand MBean
and vice versa.


<a id="markdown-more-resources" name="more-resources"></a>