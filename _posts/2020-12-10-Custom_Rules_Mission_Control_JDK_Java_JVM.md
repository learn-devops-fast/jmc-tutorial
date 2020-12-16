---
layout: default
author: Cameron McKenzie
title: How to Create Custom Flight Recorder Rules & Java Mission Control in Eclipse
blurb: Learn to create custom Flight Recorder rules with Eclipse and JShell to be used by Java's JDK Mission Control.
---

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
# Custom Flight Controller Rules with Eclipse

There is one more Parser for Java Flight Recorder recordings. One that can run on JDK 7, and which
also allows the parsing of JDK 7, 8, 9, 10 and 11 recordings transparently. It is the
parser used in JDK Mission Control. 

This parser supports internal iteration of events,
and provides statistical aggregators. It is also the parser used when evaluating rules. In
this exercise, we will evaluate the JDK Mission Control rules headless using the JMC
core libraries. A Java Mission Control custom rule will also be created, using the JDK Mission Control
Eclipse PDE support.

<a id="markdown-jmc-in-jshell" name="jmc-in-jshell"></a>
## JShell Java Mission Control Integration

First we will perform a GitHub clone of a different repository:

```
https://github.com/thegreystone/jmc-jshell
```
Next follow the instructions in the README.md to try some of the various things
that can be done using the JMC core API.

## Java Mission Control Reports with JfrRulesReport

In JDK Mission Control 7 there are two built in classes for producing HTML reports.

The JfrRulesReport class can output the results of the automated analysis in xml
and html, and which can be configured with a custom xslt.

The JfrHtmlRulesReport class will output html very similar to the Automated
Analysis Results page in JMC.

Deep Dive Exercises:

11. Try analysing some of the recordings you have been analysing so far.
12. Try using both JfrRulesReport and JfrHtmlRulesReport, with various
    arguments, to perform the analysis.


<a id="markdown-creating-rules" name="creating-rules"></a>
#### Eclipse and Custom Mission Control Rules

The easiest way to get started creating Java Mission Control custom rules is to use the PDE plug-in for Eclipse.

Note: The JMC PDE plug-in should already be installed in your lab environment.

Press ctrl-n (or click the File | New | Other... menu) to bring up the New wizard.


<img alt="eclipse plugin project wizard" class="img-fluid" src="/assets/eclipse-plugin-project-wizard.png"/>

Select Plug-in Project and hit Next. Name your rule project something exciting.


<img alt="eclipse plugin project window" class="img-fluid" src="/assets/eclipse-plugin-project-window.png"/>

Unccheck that this plug-in will make contributions to the UI and hit Next.


<img alt="eclipse plugin project no ui contribution" class="img-fluid" src="/assets/eclipse-plugin-project-no-ui-contribution.png"/>

### Java Mission Control in Eclipse

Next select the Simple Java Flight Recoder Rule Wizard and click Finish (or Next, if you really wish
to do some further customizations).

<img alt="eclipse plugin project simple jfr rule" class="img-fluid" src="/assets/eclipse-plugin-project-simple-jfr-rule.png"/>

You will now have a new project in your workspace. Open up the project and study
the source of the rule. Can you see what it does?

### Custom Mission Control Rule Inspection


Go to the Run Configurations and check out the Idle launcher. In the Environment tab
you can set up an environment variable. Launch the Idle launcher by hitting Run.


<img alt="eclipse run configurations application idle" class="img-fluid" src="/assets/eclipse-run-configurations-application-idle.png"/>

Next launch a JMC with your rule running by launching JMC with Workspace Plug-
ins.


<img alt="eclipse jmc launch with workspace plugins" class="img-fluid" src="/assets/eclipse-jmc-launch-with-workspace-plugins.png"/>

### JDK Mission Control error

If you get a validation complaint, it will be about localization – simply click Continue.
In the JDK Mission Control client that now starts, find your Idle program and make a
short (3s or so) recording with the default profiling template.


<img alt="eclipse jmc jfr recording idle" class="img-fluid" src="/assets/eclipse-jmc-jfr-recording-idle.png"/>

### Trigger Custom Mission Control Rules

Depending on the value you set the environment variable to, you should now see your
rule triggering:


<img alt="eclipse mission control custom rule triggering" class="img-fluid" src="/assets/eclipse-jmc-custom-rule-triggering.png"/>

<a id="markdown-exporting-the-rule" name="exporting-the-rule"></a>

#### Exporting Mission Control rule

The rule can be exported and shared with others. To export it, simply right click on
the rule project and select Export.... In the Export wizard, type Depl in the filter box,
and select Deployable plug-ins and fragments.


<img alt="eclipse plugin project export rule" class="img-fluid" src="/assets/eclipse-plugin-project-export-rule.png"/>

Hit Next, select a destination directory and click Finish. The resulting plug-in can
either be dropped in a JMC dropins folder
( **JDK9_HOME/lib/missioncontrol/dropins** ), or put on the classpath to a
program running the automated analysis headless.

### Custom JFR Rules Examples and Exercises

13. Duplicate the RunRulesOnFile launcher by right clicking on it in the Run
    Configurations dialog. In the new launcher, set the arguments to
    C:\Tutorial\workspace\09_JFR_CustomRules\ruletest.jfr 51,
    and add the exported plug-in to the class path (Add External Jars). Run it!
14. Do the same for the JfrRulesReport.