---
layout: default
author: Cameron McKenzie
title: Create custom pages & filters in JDK Mission Control
blurb: Learn how to customize pages and filter data events in Java's JDK Mission Control so it's easier for you to view JVM Flight Recorder data files
---

<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/E3gxhuATmHs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
# Java Mission Control Custom Pages

After some time with JDK Flight Recorder you may find yourself repeatedly wanting
to look at specific pieces of information. Java Mission Control Custom Pages custom pages provides an easy way to set up
custom views of profile data.

We will use the recording from the 05_JFR_WLS project for this exercise. Open the
**wldf.jfr** recording, and switch to the JDK Mission Control perspective.

<a id="markdown-filters" name="filters"></a>
## Java Mission Control Filters

We would like a nice view of the servlet requests taking longer than 2 seconds. Start
by going to the Event Browser page. Use the filter box to quickly find the Servlet
Request Run event type, and then use the context menu to create a new page using
the selected event type.


<img alt="eclipse jmc custom pages" class="img-fluid" src="/assets/eclipse-jmc-custom-pages.png"/>

Right click on the name of the new page, and name it “Long Lasting Servlets”:


<img alt="eclipse jmc rename custom page" class="img-fluid" src="/assets/eclipse-jmc-rename-custom-page.png"/>

### JDK Mission Control Attribute Filters

Add a new attribute filter on Duration:


<img alt="eclipse jmc custom page filter duration" class="img-fluid" src="/assets/eclipse-jmc-custom-page-filter-duration.png"/>

And set it to > 2 seconds:


<img alt="eclipse jmc custom page filter duration threshold" class="img-fluid" src="/assets/eclipse-jmc-custom-page-filter-duration-threshold.png"/>

Now we have a custom page showing the longest lasting servlet requests:


<img alt="eclipse jmc custom page view" class="img-fluid" src="/assets/eclipse-jmc-custom-page-view.png"/>

<a id="markdown-grouping" name="grouping"></a>
#### Grouping Java Mission Control Flight Data

In the custom page, events can also be grouped. Create a new page, using the Servlet
Request Run event again. Name the page Request Log. Add a new filter from
attribute, this time ECID. Select isn’t null as the predicate relation.


<img alt="eclipse jmc request log ecid grouping" class="img-fluid" src="/assets/eclipse-jmc-request-log-ecid-grouping.png"/>

Now remove the Type filter:


<img alt="eclipse jmc request log remove type filter" class="img-fluid" src="/assets/eclipse-jmc-request-log-remove-type-filter.png"/>

Use the context menu in the table to group by ECID:


<img alt="eclipse jmc request log context menu group by ecid" class="img-fluid" src="/assets/eclipse-jmc-request-log-context-menu-group-by-ecid.png"/>

Add a column for the longest duration in the ECID table:


<img alt="eclipse jmc request log add column" class="img-fluid" src="/assets/eclipse-jmc-request-log-add-column.png"/>

Next sort the ECID table on the Longest Duration column. Select the longest lasting
ECID, and next sort the List, which will now show all events with the ECID selected
in the ECID table, on Start Time.

After some time rearranging the columns in the List to your liking, you should now
have a nice Log of what was happening, in Start time order, for any ECID you select.


<img alt="eclipse jmc request log view" class="img-fluid" src="/assets/.png"/>

<a id="markdown-boolean-filter-operations" name="boolean-filter-operations"></a>
#### Boolean Mission Control Filter Operations

Lastly we will build a custom view in Java Mission Control to find any contention on Log4J lasting longer
than 400ms, or 200ms if the contention is somewhere else, as this will neatly illustrate
the use of Boolean filter operations.

First create a new page on the Java Monitor Blocked event type. Go to Java Mission Control's Event
Browser. Next use the filter box to quickly find the event type. Use the context menu
to create the new page. Name the new page Log4J Contention.

Use the context menu in the List table to show the search box. (This is available in all
tables.)


<img alt="eclipse jmc log4j contention show search" class="img-fluid" src="/assets/eclipse-jmc-log4j-contention-show-search.png"/>

### Inspecting Java Flight Recorder Events 

In the search box, type log4j, then select one of the Java Flight Recorder events. Next add a filter from the
attribute Monitor Class.


<img alt="eclipse jmc log4j contention add filter" class="img-fluid" src="/assets/eclipse-jmc-log4j-contention-add-filter.png"/>

The log4j class should automatically be added for you. Disable the search from the
context menu in Java Mission Control on the List table by using the context menu.

Add a new Java Mission Control filter from the attribute Duration. Set the filter predicate to be more than
400 ms.


<img alt="eclipse jmc log4j contention combine filter" class="img-fluid" src="/assets/eclipse-jmc-log4j-contention-combine-filter.png"/>

Select the Monitor Class filter and the Duration filter both, and select Combine with
AND from the context menu. Next add a filter for Monitor Class !=
org.apache.log4j.Logger, and Duration > 200 ms. Combine them with an AND filter,
and finally combine the both AND filters with an OR filter.

Note: There is a bug (fixed in Java Mission Control 7) that makes applying AND/OR filters sometimes
not immediately evaluate the expression. If that happens, try clicking in the list or
select another page and return.


<img alt="eclipse jmc log4j contention bug" class="img-fluid" src="/assets/eclipse-jmc-log4j-contention-bug.png"/>

Adding grouping on monitor address would yield a custom page in Mission Control that looks something like this:


<img alt="eclipse jmc log4j contention add grouping" class="img-fluid" src="/assets/eclipse-jmc-log4j-contention-add-grouping.png"/>

<a id="markdown-the-management-console-bonus" name="the-management-console-bonus"></a>