---
layout: default
author: Cameron McKenzie
title: Java Performance Tips
blurb: Here's a Devoxx video from Jack Shirazi about Java performance tips.
---

### Setting up Eclipse
<div class="embed-responsive embed-responsive-16by9">
<iframe width="560" height="315" src="https://www.youtube.com/embed/OYpTn0nWKR4" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
## Java performance tips

we're again inflated do it make sure so
let me let me just get started with a
Who am I of course and there's a item
down there at the bottom I'm not a sumo
wrestler and there's a specific reason
for that when I was writing by my book
my first book for O'Reilly they said is
there something interesting you've done
that we can we can you know advertise
for the book because people like some
sort of character indications on
something that will give that give the
author of it a character and they said
like one of our authors is a sumo
wrestler maybe you've done that I said
no but I've done these kind of other
interesting research things that I find
kind of cool which is you know black
hole thermodynamics is pretty
interesting I published on protein
structure prediction and they say no
we're looking for something more
interesting like sumo wrestling or maybe
boxing they said so my advice if you
want to be an author start having a
career as a sumo wrestler or as your
side issue okay Who am I dressing
hopefully I'm addressing to you guys I'm
talking to dead my current system is all
the kind of things that you'd expect for
a real-time system we do micro services
and all the current stuff that's I've
been putting into practice a lot of the
things that I've learned about and I'm
just going to start with my three axes
of performance so there's three axes
that I think are important which a
responsiveness data size and concurrency
and I'll explain as in in a moment that
we I'll be talking about what's
achievable initially for those axes but
there's a first I'll start with the
outliers here and the outliers are what
Google's learn and a hedge-fund random
hedge fund and Google is 40,000 requests
per second CERN is 25 gigabytes per
second hedge funds the the ones that are
really state of the our sub microsecond
response times
those are outliers and it costs a lot of
money to achieve those out lows and they
do stuff that you almost certainly don't
want to do they'll be it's a waste of
money
Google so Google have a site reliability
engineering team several of them I think
they put millions of dollars into it and
they've written a book there's a lovely
online books you can get fre look it up
and so Google s re is quite quite
well-known about maintaining their site
and keeping it available I've got two
guys and that's not even there full-time
they're like admin two guys our time is
better than Google last year so but
there's a difference in in in scale
obviously they're kind of a couple of
orders of magnitude bigger and that the
point is what the outliers are doing
it's very interesting but it's not
necessarily right for you I'm talking to
the 10 million or so Java developers who
aren't working on outliers and so this
point is where you can walk out because
this is the spoiler for the entire talk
what did I learn and that is that apart
from outliers pretty much everything you
need to know about job performance is
well-defined
there's only concurrency and the
outliers are difficult and the rest of
it is really well-defined
you shouldn't have any problems with it
it's just a matter of knowing what what
look for and that's what I'll be talking
about telling you all the techniques you
need to understand exactly where
performance issues are so for non
outliers I call it in Liars but then
I've tried to invent in Liars but in
fact that's it's a geographical term
down there sorry for that there's
there's it's quite straightforward you
just need to know what is what is
reasonable to achieve so you're trying
to do something you need to know is this
actually an outlier am i doing something
that's going to cost the fortune and I
can't achieve or is it something that's
quite reasonable to achieve and then
that's fine if I know it's reasonable to
achieve I can use standard techniques so
you need to know what's reasonable to
achieve
and then in order to know what you need
to achieve you have to have targets okay
so that's step two have targets and then
step three is just what tools you need
to use when you know that you've missed
those targets so I'm going to talk about
what is achievable now for those three
axes of performance and I've just know
just want to know that stateful versus
stateless matters so just to explain
stateful means you have a request and
that will that request needs to change
something persistently on the server or
on the service before it can reply to
you the bank account transaction is a
typical one yet it actually has to
deduct the money from your account
before it then replies to you and says
it's been successful that's a stateful
transaction a stateless one is where I
send the request and as long as it's
accepted the request that's all it needs
to do and it can reply immediately so
state this is much easier and Google is
an interesting example because if Google
only had a thousand sites that it
covered literally anybody here could do
Google it's like two boxes and one one
little dev thing you could get out of
40,000 requests per second really easily
because a search request is actually a
stateless request you send something it
doesn't have to change anything on the
server they do change stuff on the
server what they do is they load the
request so they can later on process it
so they've got all the stats about who
what kind of requests in happen but all
that can be that isn't synchronous that
doesn't have need to happen synchronous
all they need to do is lock the requests
well they need to do is get the data
from the back end and that's the real
business advantage of Google is those
massive data centers with a huge amount
of data but just in terms of stateless
concurrency on a server that's really
straightforward and quite simple so if
you can get your service to be stateless
you can move it over to some aspect of
things it's really really easy to do
when we're staple stateful concurrency
is different there's a theorem the c.a.p
theorem it's about consistency
availability and partition tolerance and
if this theorem basically says you can't
have all three so what we tend to do is
you tend to look for either lis either a
globally consistent transaction say so
there's a there's a single database
somewhere it might be a huge database
and all transactions have to go through
so that database or you go for what's
nowadays a globally consistent a
globally eventually consistent
transactions they can be faster but it
means that you have to worry about that
lack of immediate consistency so here's
what's achievable the database industry
has a nice benchmark to TPCC one which
would cover the stateful globally
consistent transactions and that's
that's gives you an idea with one box if
that database is based on one box you
can have 2,000 transactions per second
where the five-second response time for
those transactions that's the kind of
that's the bank account all right that's
where you're doing a band transaction
for an eventually consistent one with
one box I'm talking about you know like
a standard 32 cores just something you
can easily get off Amazon one of those
small small not know you know it's quite
an easy standard box to get server books
you can you can achieve 300 per second
with a hundred millisecond response time
so this is transactional okay it's not a
stateless system it's a transaction
system that means you send use you're
sending 300 quests into that system and
they are transacting on that system
persistently storing a change and
responding to you within that all of
them within a hundred milliseconds
that's achievable okay so when you're
doing stuff this is an idea
so you need to know these are achievable
that means that if I'm not achieving
this I just need the tools to figure out
why so we had three axes I had three
axes there
the first was concurrency second one is
data and data is slightly different it's
not so much as achievable as the
consequences of achieving different data
sizes there's and there's a number of
boundaries and the first boundary is the
CPU cache which even ten years ago where
it wasn't that important but Moore's law
has made the processor much faster but
the time for memory to get to the CPU
not any faster so it's become important
so you can get cash souls you can get
these pipelines for you on the cache
everything is a cache line so if you
have two different variables that fit on
one line even though they could be even
two different objects but if their tutor
or could be two different variables on
the same same object doesn't really
matter if they're fit on one line one
cache line because that's the way Java
has laid it out then that means that
there is contention if you have two
different threads updating those two
different variables as far as the CPU is
concerned there are two threads are
updating the same thing and they're
contending with each other even though
from the point of view of your
application there's no contention there
there is a CPU level so you get there's
a lot of different effects on on the
cache most applications don't notice it
because you're already hitting these but
if you're doing a very highly concurrent
application or a very low latency
application these become important and
if you're pushing a lot of throughput
through the through the cache again it
becomes important there's a very nice
talk there that I'm linking to at the
bottom but it gives you a lot more
detail on that
the next boundary is orders of magnitude
bigger
that's a Numa node ok and the Numa node
is you've got your 32 core server but
it's not actually 32 separate cores
they're what you have is a socket with 8
cores and there are four of those
sockets with eight cores and the memory
of the system is split up between those
sockets
so nowadays we'll have a lot of it your
r2 socket service for circuit service
and it is if you've got 256 Meg's and
it's a two socket server with eight
cores on each socket and that would be
16 cores the memory the 256 Meg's of RAM
is split between the two cores 110 th
typically it can actually be a different
but typically will be split between them
and that has an effect on the size of
the heap that is efficient okay so if
and it's not actually just the hot heap
it's the full process size but you need
to have all the data of the heat stay on
one of the Numa nodes otherwise you
start getting impact its performance
impact from that so that's something
that you need to be aware of if you're
looking at very big heaps and there's
there's a focus in Java 9 with g1
garbage collector to improve the support
of also Numa nodes and very large heaps
and there's an item down there that I'm
saying it's worth going off heap quite
often when you have very large data sets
next boundary of course is the total
round so not there's the Numa no gram
and then there's a total Ram you don't
exceed to note the total Ram because
when you're paging all the time and it's
really really performance impact so
you've got you've got a couple of orders
of attitude there that you can you can
lose especially when garbage collection
hits and then boundary the next boundary
is clearly the local disk space because
once you're up in that area you want to
do a lot of off heap work and if you can
do it
if you can keep it within the system
that's much more efficient because
otherwise you're over onto the final
boundary which is remote persistent
storage is your database or you're in no
sequel database or whatever you want to
call it and it's remote and there's a
lot of it's it's it's much more
difficult to get good performance from
that so for example you have to be
really careful about the type of access
the type of update you're doing because
each of the no sequel one
they're all optimized for different
patterns of behavior and you need to do
a lot of analysis there and I speak from
experience when I say that it's
painfully expensive if you if you've
done the wrong thing with the ROM no
sequel database you tend to hit the
limit before you realize you phablets
you've done the wrong thing and then
it's it's it's really painful it's
there's there's like this there's a
about 30 or 40 that that's reasonable
for you to use and they're all different
there's like there's a huge report I
think from ah that's JLo be website that
just directs I think is they've got one
of their reports gives lists from all
okay so the third axis we've done two
axis concurrency data size they're
really both three important the third
axis is responsiveness obviously that
depends on your app but then assuming
you can get your app down to whatever it
latency you need to reach the garbage
collector tends to be the limitation and
again stateless versus stateful
stateless can give you faster times and
you need to be aware of jitter so 100
milliseconds as I said already if it's a
stateful responsiveness at scale so I'm
talking about app scale I'm not talking
about one request I'm talking about
hundreds of requests per second so at
scale 100 milliseconds is achievable for
a stateful response that means that
includes a transaction on the service
and the things that you have to watch
out for to avoid that is replacing large
data structures I mean it typically it's
reloading an XML config some document
but really it's any large data structure
you need to do in place replacement if
you're editing the the data and not
replace the whole thing because it's
replacing large data structures that
really impact both object creation and
garbage collection and typically you
want to use the concurrent mark-sweep
because 100 milliseconds is
challenging pause time to achieve in a
stateful transactional system and
there's a problem with concurrent
mark-sweep because you can't achieve it
with concurrent mark-sweep but it has it
so it doesn't defragment as it goes you
build up fragmentation by remark sweet
all you ever do is delay that however
much each tune is just delaying the
fragmentation at some point it's going
to go whoa
I can't do any more I'm really
fragmented I have to pause and do a huge
long pause like ten seconds twenty
second pause crazy suppose times so a
typical technique to handle that apart
from using somebody else's garbage
collectors I'm talking about the Oracle
ones of course a typical technique is to
use a clustered system and you take one
node from the cluster actually stop
servicing stops any requests that node
and just force the garbage collection
that'll be fragmented and then you can
put it back into the node you do that
sequentially with all the nodes in the
cluster and that works really well I've
had that in another production for years
now
stateless responsiveness is easier of
course stateless is state this is always
easier with everything 40 milliseconds
is a human perception limit I'm dealing
with real-time voice systems so we need
to head a 40 millisecond pause time
maximum 40 milliseconds is actually
quite easily achievable with a sailor
system 20 milliseconds not too hard you
you need to do a little bit of garbage
collection tuning or maybe not at all
but it depends on your application when
you're targeting around 5 milliseconds
you need to do garbage collection tuning
and object tuning so it's object
lifecycle shooting you need to cut down
on object churn object allocation you
start doing pooling objects which is
ugly but that's the kind of thing to
keep the objects not not have them
churned and then 2 milliseconds 2
milliseconds is really hard so 2
milliseconds and down
you you have to change your style it's
like a DSC programs fail okay it's
really different you can't have any GC
pauses at that stage because pretty much
you can't guarantee that you'll hit two
milliseconds so at that stage is kind of
you want to avoid GC pauses at zero copy
of objects do all the object creation
initialization upfront and then it's
this very much in data structure in
place processing and the other thing if
you need to have some objects and I
generated a runtime then you can have
which do is you have a very large heat
wear and then you can restart the
service i know it's once a day obviously
if it's a 24/7 application you can't do
that but a lot of the the banks will use
this kind of technique because they have
a day cycle where they can restart at
the end of the day close of business
hours so they'll just have a really
large heap and it doesn't matter if
they're doing they're creating a few
objects that's okay for for really low
latency if you're hitting ten
microseconds the OS gets in the way and
there's a very nice talk down there by
mark price
he's from the Lmax team if you know Lmax
disruptor if you've ever heard that he's
part of that team and he gives quite a
lot of very interesting detail there on
how you have to what do you have to do
to move the earth out of the way I would
say that it's it's not it's not
techniques that's beyond anybody I mean
it we're not talking about hedge fund
techniques hedge fund techniques are
hardware okay they're putting FPGAs in
there to get Hardware scale sub
microsecond they're doing the work in
hardware and and it's it's completely
different this can be still done in
software
it's just techniques it doesn't take
that long few weeks a month and you
could be up to speed on that it's not
it's achievable but you need to
understand these techniques it's the
kind of thing you have to rewrite from
scratch so I'm not going to go through
these but there's a bunch of designs at
the design level that you need to avoid
as I said you can download the slides
and read them all but if you're doing
any of these design
things then it means you need to do a
rewrite so it's about avoiding the wrong
things so there's you can't there's
design level things and architectural
level things but you can't use a tool to
figure out a bottleneck which will just
get you around you have to do a full
rewrite and these are the kinds of
things that a design level so you know
like the typical one the one down at the
bottom not paging that's not OS level
paging that's if you're returning a huge
data set you need to return pages of the
data set it's a standard JDBC type thing
is I'm a standard in JDBC standard
mechanism if you're if you start
returning huge data sets then that means
you have to have a huge data set in
memory which then gets dumped and you're
just churning masses amount of memory so
it's just not possible so this is a this
is another point where you can you can
leave now because this is the full
troubleshooting diagram it's fine
I didn't do this at all this is Oracle
team did this so it's a very detailed
troubleshooting diagram what to do what
utilities to run what metrics to follow
if you have a problem with your system
if you don't have the metrics you'll
need to turn them all on of course but
that's not that terrible because your
problem will still be there so you'll
still we all see it and it's a very nice
comprehensive methodology there of what
of the flow for troubleshooting
so one item to bear in mind there is
always a bull neck ok people think oh
there's a volunteer I've got to fix it
and it's not the case if there's no
bottleneck then it takes no time at all
you've got the most fantastic program
you've ever in anyone's ever written or
it's hello world right so there is
always a bottleneck that doesn't matter
what matters is failing to achieve the
targets that you need to do now most
program at most performance guides will
tell you you need to set program
performance targets upfront you need to
do it at the design stage you know it's
kind of true you need to but it's not
table if you haven't because what you'll
have is your system out there in
production you haven't set targets and
at some point people are going to say
something is slow and at that point
you'll need to set the target you need
to specify what exactly is it slow and
what is that the target that I need to
do to achieve at that point so it's not
either
obviously if you're right we wouldn't
have any technical debt which is a great
position to be in but we do have
technical debt we don't do it all right
up front so it's not an irrecoverable
point you just need to decide that I
understand that at that point you need
to specify a target and then then you
look for the bottleneck so it is usually
a shared resource and this is a another
slide here which I'm not going to go
through but just to mention the bit in
bold at the top you do have those shows
resources everybody mentioned CPU memory
and i/o but the locks are critical show
resource
ok so when your system is doing nothing
but being really slow that's because of
locks
so you're looking at CPU utilization and
you're expended system seems to be
overloaded and there's no CPU
utilization
there's memory is not overloaded and is
not particularly bad you're going what
the hell is happening it's because it's
look so you just need to bear in mind
that there's four high level resources
that are shared again it's a this is a
reference slide so when you get the
slides you can look through them there's
things to monitor at the application
level and there's common problems with
some solutions at each level again these
are all slides that are left in there as
reference points for you to look at what
I'm going to look at are these the most
common problems so these are the ones
that have been repeatedly reported in
various surveys by people as the most
common problems they've encountered in
systems that have caused them to need to
address performance so I'll give
hopefully by the end of the talk a
techniques to handle every single one of
these and to identify what the problems
are and then
the rest of it's quite straightforward
okay so just starting and this is it's
an interesting title there the most
common cause of downtime is human error
okay
that's like Amazon's AWS outage human
error almost all the major outages tend
to be human error the most common cause
of downtime that is not human error
tends to be resource leaks historically
that's the case on women there's in any
kind of surveys and resource leaks
memory leaks very typical JDBC
connections running out of running out
of those file handles and disk space
that's really common so the one I'm
going to focus on which is the most
common one we tend to see in Java is
memory leaks so stage one is that you
should turn on juicy logging okay this
is the first tool that you should have
on your system there's negligible impact
on having it on there's a bunch of flags
I'm suggesting you turn on in Java 9
it's changed completely because there's
a universal logging and it looks like
that
there's I'll go through a couple of them
very quickly this this one it's miss
named it's not print GC applications
time that's the name for it but it is
actually print safe point
application stop time which may not be
much doesn't matter if you don't know it
safe points are but it doesn't mean that
you get lots of stops not just the GC
stops you get context which is thoughts
you get lots of other stops locking
global lock stops and they're all listed
when you turn that flag on and it's
quite interesting most of them don't
matter to you like this one here 0.0002
so that's one set to 20 microseconds
from their app they're interesting if
you like to see how much context
switching your applications do so that's
that's quite a good one to turn on and
then these ones you know it's a fairly
standard what I just wanted to show you
a log line in case you haven't seen it
you guys I like to have all the all the
date time information there but as you
can see it's the the actual load line
when people first look at garbage
collection logs they think oh my god
this is really difficult to read but
actually it's just it's it's very
straightforward it's telling you which
which garbage collector it was the heat
before is little arrow the heap after
the heat that's possible for that space
and then there's like a total and then
there's a time and then there's user
cysts and real times and they're all
they're all quite useful I'm not
suggesting you learn how to how to read
garbage collection loads but if you need
to don't get phased by all that text
there it is readable in Java 9 as I said
it's all changed the format it's
designed to be more consistent and
useful for tools and there's a nice talk
by Tony Princess if you want to go to
that so I'm just going to do a really
quick heat primer just so you understand
about the spaces there are two spaces
there there's a young generation an old
generation the young generation is split
up into Eden and two survivor spaces the
old generation is also called tenured
and prior to Java age you have the prohm
space from Java if this.method space
metastasis outside the old generation so
sperm and they're kind of different but
I'm just going to do one quick garbage
collection so you get Eden that's where
all the purple objects are for this case
they're by definition everything in Eden
has aged 0 so the little little numbers
of the ages of the objects across the
top there so this is you won't
necessarily see survivors space pull up
but it can be so this is this is when a
garbage collection happens a young
generation garbage collection happens
when even is full okay
the only time it doesn't happen when
Eden is full is if the the tenured space
needs a garbage collection and it does a
full garbage collection sort of halfway
through even being full but almost all
the garbage collections you'll see it's
when Eden is full that's what triggers
the garbage collection a young
generation garbage collection so
evenings will
and this example I've got lots of dead
objects those are the ones with dots in
and a few live objects when the garbage
collection comes around and and at the
same time in the survivor space you've
got lots of dead objects because it's
been a while since the last garbage
collection and a few that are alive so
what what if the garbage collects does
is it copies over so let's go back I've
got a BCD down there in purple there a
zero they get copied over to the other
survivor space the one that's empty all
the rest that just ignores it doesn't
care about them and then it copies over
from the first survivor space the
objects that are still live and the dead
ones that doesn't care about so you end
up with just the live objects eden's
nice and empty that's a garbage
collection I'll just skip back again so
you notice down there in the survivor
space we've got x and y if you look at
the top there there are three ages old
three garbage collections old that's
their age there's a parameter that says
if they're a certain number of ages old
then I'm not going to copy them into
Survivor space I'm going to copy them
over into the old generation so with
this example I decided that's going to
be four so you can out be up up to age
three and then you move over to the old
generation so when it's clearing out
survivor space all the rest will get
copied into the survivor space too
except those those ones that are hit
that age and that's that that's called a
tenuring threshold there's a parameter
that sets that and the reason for that
is because it's inefficient to keep
copying objects it's an actual copy it's
not just the pointer address this is
quite inefficient so you don't want to
copy objects a lot of time that is what
takes up the time in a young generation
pause so you don't want to keep doing
that the idea is that if they're going
to last too long then they're probably
going to be around for a long long time
so just throw them over to the old gen
the tenured space this is a quick aside
if there's a finalized method in object
if you don't override it the JVM knows
to ignore it if you do override it this
is the situation you'll have you've got
the all these purple objects are the
same
the instance of the same class which
overrides finalize all the dead objects
should normally at the garbage
collection they would all be ignored and
we've just got x y&z over there they're
the only ones that we've copied but if
you'd finalized them they all get copied
at the end of the garbage collection
because the garbage collector says ah
okay these are all dead but they're live
for me because I need to run the
finalize method on it because it's it's
an overridden finalized method so you
get this really ugly view and it is
really ugly where you've filled up
Survivor space and you've overflowed
into ten in space dead objects okay and
that's really really costly so I mean
I've emphasized over overemphasized
things by having the entire eden full up
with these finalized objects is unusual
for that to be that's a pathological
situation but you just need to
understand that's what it looks like
when you override finalize on objects
and you just adds ugly so as I said I
try and avoid reading job GC logs I can
read them but I try and avoid them as
much as I can
I'm much prefer using a utility that
views it I use GC viewer there's there's
a I maintain a page there there's a list
of a quite a lot of them including so
all the tools that I'm talking about
here are free tools as with everything
if you pay you if you get if you use a
paid forward tool tends to be better I
wouldn't say that all the paid for tools
are better than all the free ones but
certainly the best tools will cost a bit
of money all the ones I'm talking about
are free tools and that's the one I
prefer it's quite good it looks like
this so I'll just go over it a little
bit which you've got you've got this
dual scale on the on the left hand side
it shows both size heap size and the
time taken for the garbage collections
and then along the top you've got a
elapsed time and you can toggle that to
get actual time if you've set the date
stamps in into the log file and then it
there's lots of lots of colors you can
turn them on and off and they they tell
you the young generation side the old
generation size
and a typical garbage collection so
remember what happens is the Eden gets
full and then it's emptied out so you'll
get this sawtooth line which is at the
bottom
Eden is empty and then it gets full and
the next set of the garbage collections
and then it goes down it is empty so
that's a typical NGC virus also shows
some full GCS which you want to avoid so
this is a this is an example of if you
have a quick look at this one it's a
really straightforward example you see
these every hour on the one hour on the
two hour this is long black line we're
doing a full GC every hour and that's
I've seen actually a lot of applications
do this because if you engage the RMI
system even if your application isn't
that something else is it automatically
turns on this distributed garbage
collection which will force the folds
you see every hour and there's a
property to turn it off basically you
just set set it set the time interval
for that to be really long but I've seen
a lot of applications where this
happening and not people not even
realizing because for the most part it
doesn't matter it's only when you have
the pause time targets that it matters
so this is a perfect GC the blue line
down the bottom that's the sawtooth is
going up and down and down and down and
you see that the it's not it's not
increasing at all so basically what's
happening is that all the objects are
being created even and then nothing is
ever flowing over to to the tenured
space this is up this is perfect if you
can achieve this awesome you can't
achieve this okay but if you can
obviously it's like a little little one
that I did and you can't you probably
can't see but there's a green line
that's the time taken by the GCS if you
can see it on the scale it's actually
0.1 milliseconds so less than a
millisecond pause times consistently
that's a if you have an application a
real-world application that does that
please tell me I would love to see it
this is more realistic this is a kind of
thing you see with spikes and things and
it's going up
down now this is also kind of kind of
thing you see now looks looks okay
because you know okay what's happening
is you're getting overflow so the blue
line spike is saw two thing up and down
but there's there's it's overflowing
some objects are overflowing into the
tender generation so it's gradually
going up and then obviously when it hits
the heap size it had any to do a full GC
and then it goes that clears out there
the tenner generation because by then
those objects are dead and so they can
all be clear that so looks it's not too
bad as long it's bad if you can't afford
the time the time pause for the old
generation it doesn't look too bad but
I'm going to scale out and it doesn't
look so nice now and this is a typical
object leak and memory leak okay so the
very first way you can identify memory
leaks before they start impacting your
application is to look at the garbage
collection log and what you're looking
for is the after the full GC there's at
the bottom point after the full GC is
gradually increasing so it's we're not
talking about the Sawtooth the blue
lines when the blue line reaches the top
you get a Falls you see and it and it
clears out as much as it can because
you've got an object leak that means
that gradually that space is being
filled up and each time it tries that it
can only release less there's less able
so that bottom line the very the very
bottom of those points gradually
increasing that's an absolute standard
memory leak an indication of memory leak
so just use that and you say you can
identify that way before it starts
impacting application in this case you
let it run eventually it just does
continual full GCS and your application
comes to a standstill
so the typical things to do is a heap
dump there's a number of different ways
you can use the heap dump on memory
error flag I never do that because that
means that your application sort of I've
got systems with four gigs eight gigs 16
gigs whichever they freeze okay at that
point when they're doing a dump on out
of memory error they freeze
and that's that's not what you want it
to freeze it's just going to freeze and
do that memory dump and then and it
doesn't die until the memory dump is
over assuming it does die so so
something like Tomcat will just catch
the error I'll do the memory dump but it
will carry on I tend not to do that I
instead have alerts on the system
looking for memory leaks and then I will
explicitly do well I'll take care of the
cluster most of the things I deal with a
clustered I'll take it out of the
cluster and do an explicit memory dump
using one of the one of the different
techniques to typically J map that's one
I like to use the most so yeah there is
there big I'm just going to do a quick
detour because there's an alternative to
memory dumps which is the heap histogram
so that's just again J map with a minus
system flag and that gives you it's much
less overhead there is still a freeze
but it doesn't think as long and it just
gives you a nice histogram is this is
exact this is output it just tells you
in order the class with the number of
instances and how many bytes they take
in total and sure you use to that kind
of nomenclature where the square bracket
means an array B is a by C is a char
eyes and integer all the rest as just
class names so square square bracket L
java.lang object means it's an array of
objects and that's obviously going to be
the internal of an ArrayList that's the
typical thing there let's see yeah
there's forty four hundred seven
thousand of those and three hundred
twenty-nine thousand or a list and most
of those are probably ArrayList so this
is this is a much lower overhead it's
the sort of thing you can do
periodically in production not too often
it does have cost but you can do it
periodically and it's really easy to
load this into a spreadsheet with
another later version and do a
comparison against them and see if
what's changing so it's quite a cheap
way of finding out memory leaks so fair
enough that's a detour if you can do
that if you can you can you need to do
the dump analysis whoa I am cutting it
close
okay this is memory their kids memory
- memory analysis tool it's really
straightforward you can just go to the
dominators panel you find the one that's
that that's taking up all the space and
just open it you know open up the tree
until you find the in this particular
one I it's it's a class called fast leak
and it's got a cache now so
straightforward really easy to use I'm
going to go straight through tuning the
heap so generation count
okay generation count is there's a
little explanation there it's basically
long-lived objects they like you
generate them initialization there's one
two three four five ages and they all
live for a long time so when they get to
the tenth generation an hour later
there's five generations of them and
short-lived objects they all die quite
quickly so there's only like five
generations of them but if you have
leaking objects then every generation
there's a new leaked object so the
number of generations of an object is a
good indication of a memory leak so this
is what you can do again this is not
again this is jvzoo vm and don't use
this in quod never used a visual
there's no profilers that are
appropriate for production there's a few
paid ones there's no free profilers that
are perfect for production this is a
really straightforward mechanism of
finding out memory leaks in development
just look for the generation count so I
just give a quick talk here I'm just
going to go through de visual VM it's
got a lot of features profiling and
sampling they're two different things
for execution profiling you want to use
the sampler for memory profiling you
want to use the profiler okay I have two
more things
two more techniques so and I've just got
time for them which is why I've skipped
through that everything is in the slide
and it should all be explained
understood by the slides I just wanted
to go over a jdbc logging this is this
is really straightforward
it's JDBC is built actually very nicely
and
other people complain it's actually very
nicely as a plug-in component so it's
very easy to plug in your own component
that wraps the JDBC JDBC layer and
there's quite a few JDBC tool logging
tools out there I use peace expire I'm
used to it I've used it for a long time
the only thing you have to remember
about JDBC is it uses that paging
mechanism so the request that you send
doesn't return all the data in one go at
some point as you as you iterate through
results set one of those will trigger
another request for more data so when
you're looking at logging it's not this
inish the initial time is not the time
taken for the full execution its there
are there will be like if you look at
individual logging statements you'll see
individual results a lot of them take
zero time and then one will take some
some milliseconds because it's the next
patch that's really straightforward
again it's a tool you can use in
production it's really easy to analyze
and it identifies exactly where you have
problems on there on the JDBC side ok
I'm not doing too bad now
so concurrency is kind of the last set
of tools that you need for analysis and
you need to determine pretty much what's
happening and it the only standard kind
of tool is actually just thread on
dumping threads you just have to not
dump too often and what I mean though
there are there's a few other things
here like there's the J stack - L that
gives you actually lock information from
the java.util concurrent classes and
there's a few techniques in terms of you
immediately get deadlock information you
get information about synchronized
monitors from the spec traces and
there's also there's a thread MMX beam
which gives you some usable information
but pretty much the the main thing to do
at the moment I would love to have
better tools but there aren't very many
to take a stack trace and this is a
typical contention example what you'll
see is you see I've chosen two of the
threads that are blocked you can see
this just there both if you look at the
headline of the
the thread they're all ActiveMQ ones I
don't know if anyone uses that there's
two there are blocked and they're
blocked and it tells you what the lock
is that they're blocked on and then
there's a third one down there that
holds the lock okay in this example
actually it was a production example and
there were something like 30 threads 30
ActiveMQ threads all all blocked on on
one that was running it's not so it's
not one thread that's consistently
running that lock is changing over so
it's not going to block everything what
it is is it's serializing the execution
across all those threads because only
one of them at a time can progress okay
that's a very standard contention
example that's exactly the kind of
examples you want to identify and you
can finally notify very easy for the
factories you can find out what is that
actually doing the lock and it's quite
easy to then say okay I need to change
that lock so a way back I gave you the
slide with the top common problems and
what I've tried to give you is an
understanding of what is achievable okay
that's the first thing you need to
understand because if you've got a
problem you need to know is it am I
trying to do something that's achievable
okay that was that first section because
if it's not achievable you need to know
that up front if something is not
achievable I need to put a huge amount
of effort time and money into doing that
or I have to change my achievement my
ten what I can tell the business so is
it achievable okay most things are
achievable
only those outliers are difficult so
then once it's achievable you just need
to say okay so I've got a problem I just
need to set a target what is what is it
that I'm required to achieve for our
system that's the second step and the
third step is I have a problem let me
identify the problem let me find out
what's causing it these are the tools
that will let you do almost all the
common problems as my MA tools and there
aren't that many techniques and a little
bit of practice will get you there but
even without practice you can use these
tools quite straightforwardly okay and
then these are the top
and problems of people have-have
announced and those are the tools that
apply for them and I'm going to leave it
on that slide because the next one is
just asking if there's any questions
