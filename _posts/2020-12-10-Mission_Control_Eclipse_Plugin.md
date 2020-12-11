---
layout: default
author: Cameron McKenzie
title: How to install the Java Mission Control Eclipse Plugin
blurb: Here's how to install the Java Mission Control Eclipse Plugin and get the latest version of Java Flight Recorder.
---

## Java Mission Control Eclipse Plugin

<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


## Mission Control in Eclipse Tutorial

There is a complete tutorial on how to build Java Mission Control and install the Java Flight Recorder plugin for Eclipse over on TheServerSide:

[How to install the Java Mission Control Plugin for Eclipse](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Java-Mission-Control-8-Eclipse-plugin-Install)

### Transcript of JMC JFR in Eclipse Tutorial

_NOTE: This is just a quick transcription of the Java Mission Control in Eclipse tutorial, done using an automated trancription bot. I apolgize if it's not 100$ accurate._


If you're in Eclipse the only plugin you can install right now is version 6 which is Oracle's which requires a commercial license. 

I'm going to show you how to get the open source AdoptOpenJDK plugin installed so you don't need that commercial license at all. Right now if you try and install Java Mission Control in Eclipse you'll be installing version 6 which is Oracle owned and doesn't allow you to do Java Flight Recordings unless you have a commercial license, so the best way to get the latest version of Java Mission Control is to build it from OpenJDK. 

That might sound intimidating, but if you've got Apache Maven and Git installed it's not that hard. All you have to do is go over to the Java Mission Control Github repository, it's not on Mercurial anymore, it's over on GitHub, and copy that URL. You'll see the green button there you copy the GitHub URL and then you come to a folder on your local file system. I've got a folder here called tutorial I'm going to open up the Git BASH shell then I'm just going to clone that repository. 

## GitHub and Java Mission Control

Just git clone that repository url in there and all of a sudden that repo will get cloned to my local machine. Now there's a couple of interesting folders inside of this repo, one of them is this 'releng' third party folder. There's a bunch of third-party libraries that you need to build in order to get the Java Mission Control Java Flight Recorder plug-in working, so you have to come into this folder here and then you just do a quick mvn p2:site which is going to kind of set up a whole website that's going to host a Maven repository with all these third-party libraries. 

The core build of the java mission control java flight recorder tooling is going to need so yeah so that command was maven p2:site now I'm actually just going to hope this hosts that site on jetty so I say jetty:run and this is all configured to host a maven repository on localhost:8080 which is going to give the core build of java mission control java flight recorder eclipse plug-in access to the third-party libraries that it needs okay so you leave this open right now there's a jetty server running on localhost 8080. You've got to leave that open if you close that window that's going to stop the server and that's going to stop your maven build what we need to do is we need to go into this jmc folder again that's where we did the clone and we have to go into this core folder and from this core folder we need to do another build again so I go get bash here and then what are we going to do we're going to do a maven clean install and the install command covers compile test and package so it's going to compile the code run some tests and then package all of the core stuff up into appropriate jar files and you can see in the output there it actually says that certain jar files are being generated.

## Build Java Flight Recorder

 Okay and once all of that succeeds I need to move from that core folder cd dot dot down to the base JMC folder you can see I move folders there and then the last command I need to do is maven package which is going to take everything that's been built in that previous maven install and then slice and dice and package it up into the various jar files that I need one of those jar files is going to be the Java flight recorder maven plugin

And there we go the build has completed and there's a very special file that's been placed on the folder system so I'm going to go back to JMC here you'll see this folder called application I'm going to dig right down org open JDK JMC update site where is it jmc or it's alphabetical so you would be at the bottom...

There it is right there inside that target folder and there we see the org open jdk ups update site ide that is the java flight recorder eclipse plugin version 8 that needs to be installed in eclipse so what we do is we head over to eclipse I go help I go install new software and then I click add and I say I want to add from an archive now I'm going to go and find that thing again where is it it was over in c:\tutorials

## Install Flight Recorder Eclipse Plugin

Not temp but tutorials, JMC applications right at the bottom under update site ide target and right there is the java flight recorder java mission control eclipse plugin I click open to install it I click add there's a few options here I'm going to select all three click next click finish accept any of the license agreements that might be required click finish that's going to take a moment to install and then I need to reboot my eclipse ide i'm going to install even though the software might not be signed I will restart now and now that java mission control eclipse plugin should be installed and ready for use on reboot

And there it is right over here we can actually see the java mission control icon it's asking me if I want to open up my firewalls I will allow access then I can create a new connection even go on to something local I think I've actually still got that jetty server running right there so I can start a flight recorder and maybe record for I don't know one minute and now you can actually see the flight recorder is happening and in one minute I will actually have my first flight recording that I can look at with mission control

And there you go we actually can see the flight recorder analysis here we can take a look it looks like I've got too many processes running on my machine you can take a look at the memory that was used if there was any garbage collection that happened or class loading all the threads that were in use and were blocked the memory the file socket I o and everything like that and there you go that's how you get the java flight recorder java mission control plug-in installed in eclipse and there you go that's how you install java mission control in eclipse now if you enjoyed this tutorial why don't you head over to the serverside.com i'm the editor-in-chief over there we've got all sorts of great content on java eclipse enterprise software development DevOps you name it if you're interested in my personal antics you can follow me on twitter cameronmcnz and subscribe on the YouTube.