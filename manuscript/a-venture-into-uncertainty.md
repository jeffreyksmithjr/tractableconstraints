# A Venture into Uncertainty

I've covered a range of different topics on this blog, but (surprisingly?) I
have not yet gotten to the main topic that I started this blog to discuss: my
thesis. Strange, right?

Instead of jumping right in, I'm going to try to lay a foundation, by
introducing some fundamentals first. All of the material that follows is
directly adapted from materials by my advisor, [Reynold
Cheng](http://i.cs.hku.hk/~ckcheng/), and, indirectly, my second examiner,
[Ben Kao](http://www.cs.hku.hk/research/profile.jsp?teacher=kao), but all
errors are likely my own. They're structured a bit like lecture notes, so if
you're looking for something a bit more blog-like, I'll understand if you nod
off.

## models of uncertainty

Discussing of uncertain data occur can focus on two tightly connected
concerns: how do we model uncertain data and then how do we query it. First,
we'll start off with a discussion of some basic models of uncertainty, with
examples taken from (entirely fabricated) data about [the Venture
family](http://www.venturefans.org/vbwiki/Main_Page), Venture Industries, etc.

## point level uncertainty

Point level uncertainty consists of a tuple or attribute with a single
probability.

### point level attribute uncertainty

A discrete (or nominal) attribute is not precisely known.

In this example, because he was only observed in passing, it is uncertain what
color kerchief Hank is wearing.

Person Kerchief_Color Probability

Hank

Yellow

0.1

Hank

Red

0.1

Hank

Blue

0.8

### continuous, point level attribute uncertainty

While not always the best way of representing this type of uncertainty, it is
possible to have a continuous attribute with uncertainty.

In this example, due to Dean’s rapid growth, it is uncertain what his current
weight is.

Person Weight Probability

Dean

48.2

0.4

Dean

47.5

0.3

Dean

49.1

0.3

As is evident from the above example, this is not the ideal way of
representing this type of uncertainty.

### point level tuple uncertainty

The represents the belief that some attributes are precisely known, if the
tuple is valid.

This example is from the Venture family’s large collection of vehicles. Due to
the age of many of them, their operational characteristics are uncertain, such
as their top speed in m/s.

Vehicle Type Top_Speed Probability

X_1

jet

347.2

0.1

X_1

jet

400.0

0.2

X_1

jet

423.7

0.7

The attributes may be discrete, continuous, or both. Regardless, the
uncertainty occurs at the tuple level.

## interval uncertainty

An uncertain interval consists of a closed region and its probability density
function. It is only meaningful for an attribute.

### interval attribute uncertainty

This example is for a wireless sensor network at the Venture compound, used
for security. The database stores an uncertainty interval of the number of
Monarch henchman near each sensor.

Sensor_ID Butterflies_in_range

12

Uniform[0,2]

37

Uniform[1,4]

51

Uniform[42,97]

Uniform distributions are used as a simple example. PDFs can be any arbitrary
function in practice.

## uncertain queries

Now we're going to shift focus to the queries than can be posed of these
simple models of uncertainty. One useful mental model to use is to divide the
classes of queries along two dimensions. First, consider whether a query is
value based or entity based (i.e. What is it trying to return?). Second,
consider whether a query can consider all records in independently of each
other or has to take into account the dependencies or interactions between the
records.

### value based

In value based queries, some computation is performed over an attribute and a
single value is returned.

### value based, independent

The only example of this query type is a Value Single Query (VSingleQ).

From the relations above, a VSingleQ would be, “How many butterflies are near
sensor 37?” It should return the uncertainty region from 1 to 4, with a
uniform distribution or more compactly U[1,4].

### value based, dependent

The examples for this query type are Value Average Query (VAvgQ), Value Sum
Query (VSumQ), Value Maximum Query (VMaxQ), and Value Minimum Query (VMinQ).

An example of a VMinQ would be, “What is the lowest number of butterflies near
any sensor?” The answer would be some PDF over the interval [0,2].

### entity based

Entity based queries are focused on returning particular entities, based on
their uncertain attributes.

### entity based, independent

The primary example of this query type is an Entity Range Query (ERQ).

An example of an ERQ would be, “Which sensors have between 1 and 2 butterflies
within range?” The answer would be sensors 12 and 37.

### entity based, dependent

This type of query consists of the following queries: Entity Minimum Query
(EMinQ), Entity Maximum Query (EMaxQ), Entity Nearest Neighbor Query (ENNQ),
and Join.

An example of an EMaxQ would be, “What is the sensor with the largest number
of butterflies within range?” The answer would sensor 57, with a probability
of 1.

Contrast that with an EMinQ, “What is the sensor with the smallest number of
butterflies within range?” The answer would be sensor 12 with a probability of
0.67 and sensor 37 with a probability of 0.33.

An example of of an ENNQ would be, “Which sensor has the closest number of
butterflies within the sensor range to 3?” The answer would be sensor 47 with
a probability of 1.

## bringing it all together

Everything I've presented in this post is fairly classic, basic stuff, but if
you have the time and interest, it will give you a major head start on
understanding the body of uncertain data management literature.

The upcoming materials, getting a bit closer to the heart of my thesis, are
going to take these basic models and queries and see how they work when we
venture beyond traditional relational databases. Don't worry: it'll be fun.
There are elephants! I promise.
