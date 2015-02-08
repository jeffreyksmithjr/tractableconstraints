##  Consistent State and Other Delusions

I find that computer science is at its most engaging when it's making a really
big point, but couching it in very subtle, almost cryptic terms. It's kind of
funny how such a nerdy discipline can get very excited about tremendously
small things, but then almost mumble a truly major insight. I mean, it's
actually not that hard to find a world class computer scientist who will jump
up and down shouting about function subtyping being contravariant in the
arguments ([Dan Grossman](http://homes.cs.washington.edu/~djg/) if you haven't
seen it). But then when a broad point of huge applicability is illuminated
through CS, well, that's worthy of some brief asides before getting on with
the exciting work of lemmas or simulation results.

### consistent is a state of mind

Database nerds have this concept called consistent state. At it's simplest, it
means that if you have, say two sales recorded, one for $2 and another for $3,
then the record for total revenue says $5. Trivial, as they say in the
literature.

Of course, this isn't trivial, not even in the literature. Because consistent
state actually encompasses two very large and tricky concepts.

Consistency seems like a nice enough guy until you get to know him, but then
he turns out to be a total mess. Sure, we can all agree that 2+3 does equal 5,
but things go to hell in handbasket not long after that. More on that in a
minute.

State is also a tricky concept, because state is a pure abstraction. At a very
real level state is not real; it's a frame we talking monkeys have fit upon
the world to make it less horribly difficult to comprehend. Just sticking with
simple database examples, what is the current state of a given datastore? Does
it include just the records written to disk storage? What about the records in
RAM? Or even things currently being flushed from the cache to disk? Maybe
someone is entering new data in their browser _right now_. Is that part of the
state? And my personal favorite, what if that magnetic spinning disk made a
tiny error? Does it then cease to be the one canonical source of all knowlege,
carried down by Charlton Heston from on high?

### ACID reflux

Let's get back to consistency.

> Hi, I'm consistency. You may remember me from such films as the The Lost
Update or Phantom Read: the Perils of NoSQL.

Consistency is sorta part of this club of database properties called ACID.
Along with atomicity, isolation, and durability, it forms the basis of all of
the simplifying assumptions that allow us to get through our day-to-day lives
without going mad from constant anxiety over what might happen with our
precious data.

I think consistency made into the club on a special case quota. Likely someone
really wanted the acronym to work out to be ACID, and they worked backwards
from there. We do these things, nerds; it's in our nature.

So, in traditional SQL systems we pretended that the database handled 3 of
these 4 properties for you, through magical database elves or something. But
only the crudest discussions ever really tried to sell anyone on the idea of
databases resolving internal consistency. It's an absurd concept. The party
line is that "it's handled by the application logic", which as academic way of
saying, "I see no possibility of publication in your question."

### the older I get, the less I know

Lots of software developers aren't comfortable with the idea that all of these
simplifying assumptions might not just be literally untrue but meaningfully
untrue. One of the easiest ways to see how this can all come unraveled is to
look into how our old friend state is in inherent conflict with consistency,
that paragon of virtue.

Embedded in the concept of state is the concept of time, or rather, a dramatic
simplification of time. As I touched on somewhat obliquely in a post on the
[shelf life of data](http://toromon.com/shelf-life.html), the accuracy and
thus value of data decays over time, sometimes in dramatic fashion.

My [advisor](http://i.cs.hku.hk/~ckcheng/) and [second
examiner](http://i.cs.hku.hk/~kao/) have done some really interesting research
on this issue. In particular, they've dug deep into some of the issues
surrounding the difficulties of maintaining derived values (like our $5 of
revenue from above) under tight, real-time circumstances. Summarizing their
work, very, very briefly, they say that you've got to lighten up: there is no
perfectly accurate up to the minute value. Even if you say you demand some
tight, artificially notion of temporal consistency, you're just asking for
poor performance and inefficient resource usage. But if you just loosen your
artificially narrow boundaries a bit, you can get a good enough answer. I view
this as a more detailed and actionable version of, "All models are wrong, but
some are useful."

### ideas worth spreading

My big question when I come across insights like this, is:

> Why is no one jumping up and down?

Really. Understanding that you can't truly know the value of your checking
account unless you make observing your cash flow your full-time job is a
hugely relevant insight. This is not inside baseball. Normal people should
care. At the very least, it's a precursor to understanding, say, how a
retirment account is going to behave over your lifetime.

There are lots of other expansions I could make on this point. After all, I
did write a thesis on uncertain data management, but I'm sure you can imagine
[roughly what it says](http://xkcd.com/793/). But for now, I'm off; I've got
to jump up and down about the limitations of accurate aggregation of
temporally uncertain values, and that requires some serious stretching and
warm-ups, first.
