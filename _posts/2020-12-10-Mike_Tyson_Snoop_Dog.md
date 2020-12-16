---
layout: default
author: Cameron McKenzie
title: Source code for Java Autoboxing and Mission Control Example
blurb: Here's a Java Autoboxing source code example that demonstrates, using JDK Mission Control and the JVM Flight recorder, performance problems boxing and unboxing can cause.
---

# Java Mission Control Example Code

```
package com.mcnz.jfr.jmc;
import java.util.*;

public final class MikeTyson implements Runnable {
  private final Map<Integer, SnoopInt> map = new HashMap<>();
  public MikeTyson() {
    for (int i = 0; i < 1_000_000; i++) {
      map.put(i, new SnoopInt(i));
    }
  }
 
  public void run() {
    long yieldCounter = 0;
    while (true) {
      Collection copyOfValues = map.values();
      for (SnoopInt snoopIntCopy : copyOfValues) {
        if (!map.containsKey(snoopIntCopy.getId()))
          System.out.println("Now this is strange!");
        if (++yieldCounter % 1000 == 0)
          System.out.println("Boxing and unboxing");
          Thread.yield();
      }
    }
  }
  
  public static void main(String[] args) throws java.io.IOException {
    ThreadGroup threadGroup = new ThreadGroup("Workers");
    Thread[] threads = new Thread[8];
    for (int i = 0; i < threads.length; i++) {
      threads[i] = new Thread(threadGroup, new MikeTyson(), "Allocator Thread " + i);
      threads[i].setDaemon(true);
      threads[i].start();
    }
    System.out.print("Press  to quit!");
    System.out.flush();
    System.in.read();
  }
}



```