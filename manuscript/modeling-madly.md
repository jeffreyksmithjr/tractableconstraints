-# Engineering data

# Modeling Madly

### Machine learning at hackathons

* * *

I recently wrapped up my second hackathon at [Intent
Media](http://www.intentmedia.com/). You can see my summary of one of our
previous hackathons [here](http://tech.intentmedia.com/post/81329300336/hack-
day-march-2014). These past two hackathons I’ve taken on some slightly
different challenges than people usually go after in a hackathon: developing
new machine learning models. While I‘ve been working on data science and
machine learning systems for a while, I’ve found that trying to do so under
extreme constraints can be a distinctly different experience. A very good data
hacker can easily find themselves with a great idea at a hackathon but with
little to nothing to demo at the end. Accepting that my personal experience is
just my own, let me offer three tips for building new models at a hackathon.

## Time is not on your side.

When you’re doing a more traditional web app hack at a hackathon, you can
almost run out of time and still come up with something pretty good as long as
you get that last bug fixed before the demo. This is a great characteristic to
build into the plan of a hack but one that simply does not apply to a machine
learning hack.

Think about what happens when you do find that last bug in a machine learning
project. You still need to potentially do all of the below:

![](https://d262ilb51hltx0.cloudfront.net/max/600/1*8me9kD0jX0M_vhOuZFyAmA.jpe
g)

  1. Reprocess your raw data.
  2. Regenerate your signals.
  3. Retrain your model.
  4. Evaluate your new model on out of sample data.
  5. Calculate performance statistics.
  6. Draw your conclusions.

That’s no “just hit refresh” workflow. Even with a well-oiled workflow, some
of those tasks can take all of the time your average one-day hackathon is
scheduled for. Take #3, for example. Training a production grade model using,
say, Hadoop, can take a lot of time, even if you have the cash to spin up a
fair-sized cluster of EC2 instances.

What that means for your hack can vary, but you’re just asking for trouble if
you don’t start with that fact taken into account in the scope and goals of
your project. A solid project design is absolutely crucial, if you’re going to
hope to take all of the little steps involved in getting your model ready to
demo.

Which leads me to my next point…

## Bite off less than you can chew.

* * *

![](https://d262ilb51hltx0.cloudfront.net/max/2000/1*wcVX4RW0Q23DPVjUwgRhaQ.jp
eg)

One of the best things about working in data science is all of the really
smart people. But, of course, the corollary is that one of the worst things
about working in data science is all of the really smart people. Sharp
engineers and data scientists can take the nugget of an idea and envision a
useful, powerful suite of products that would take years to build, which is
not so useful when you have a day or two. Mature dataists know just how much
ambition is too much and plan accordingly. I happen to be lucky enough to work
with some very smart _and _very mature data scientists and engineers, so this
has not been a problem for either of my last few hacks. But, I’m just lucky
that way. You might not be so lucky.

Unrealistic ambitions are a constant danger in a machine learning hack,
running along the edge of all activities like a precipice beckoning you to
dive off and see where you land. If you take one thing away from this post,
let it be this: don’t dive off the cliff. Just don’t do it. You won’t like
where you land. You’ll wind up with more questions than answers and you’ll
have nothing to show come demo time. Moreover, your fellow devs who worked on
apps and not models will simply not understand what you spent your time on.

* * *

What does a precipice look like? It could be a novel distance metric. It could
be a fundamental improvement to a widely used technique like SVRs. Or it could
just be something really benign sounding like a longer training set. I would
say that even choosing to pose the problem as a regression one instead of a
classification one could qualify.

The danger originates in the intrinsic tension between the rigorous and
exploratory mode of academic data science/machine learning education and the
pedal-to-the-metal pace mandated by a hackathon. They are very different modes
of working, and you’re just going to have suspend some of your good habits for
a day or so, if you want to have something to demo.

## Use lightweight tools.

This last point can be the trickiest to put in practice, but I think it can
totally be the difference between a project that feels like a hack and one
that feels like just getting warmed up on a weeklong story. If you’ve figured
out how to scope your project appropriately and designed something that can
really be built in a day or two, you can still actually fail to do so. I think
it can the difference can easily come down to technology choices.

For example, I currently make my living writing Cascalog, Clojure, and Java on
top of Hadoop to process files stored in S3. I know these tools well enough to
pay my rent, but I would absolutely hesitate to use any of them in a tight-
paced context. I have spent weeks trying to understand a single Cascalog bug.
Seriously.

If you know the language, Python offers an unbeatable value proposition for
this use case. [scikit-learn](http://scikit-learn.org/) has nearly everything
you could imagine needing. [pandas](http://pandas.pydata.org/),
[NumPy](http://www.numpy.org/), and [SciPy](http://www.scipy.org/) are all
sitting there to be brought in when appropriate. And don’t forget how awesome
it can be to prototype in a purpose-built exploratory development environment
like [IPython](http://ipython.org/).

But this is machine learning, and sometimes our data is just big. Maybe even
web scale. Some people hate these phrases, but they serve a purpose. We don’t
all use Hadoop out of love for horrendously complex Java applications.

https://twitter.com/BigDataBorat/status/372350993255518208

https://twitter.com/GoneCaving/status/419239577837391872

Big data is not just statistics on a Mac Pro, although it can often look like
that. Scale can be a real necessity _even in a hackathon._

When it is, there are no easy answers. If you’re lucky, maybe you can actually
work with multiple hour model learning times. If you’re really lucky, you
might be using [Spark](http://spark.apache.org/) and not Hadoop, in which case
it might not take hours to learn your model.

My point is that, insofar as you have a choice, choose the leaner meaner tool,
the one that will let you do more with less input required from you. Don’t use
that C++ library that promises awesome runtime but with Python bindings that
you’ve never tried. You’ll never figure out its quirks in time. Write as
little data cleanup code as you can manage. Commands like
[dropna](http://pandas.pydata.org/pandas-
docs/dev/generated/pandas.DataFrame.dropna.html) can save you precious minutes
to hours. And if you can get your data from database or an API instead of
files, then, for the love of Cthulhu, do it. Hell, even if you have to load
your data from files to a database first, it might be worth your time. SQL is
one of the highest productivity rapid prototyping tools I know.

And though I love to bash on the clunkiness of Hadoop, there are even ways of
taking some serious pain out of using it under pressure. Depending on what
you’re doing [Elastic Map Reduce](http://aws.amazon.com/elasticmapreduce/) or
[PredictionIO](http://prediction.io/) can get you to the point of being
productive much faster.

## I could have danced all night.

I love hackathons and their variations. They remind me of the fun old days in
grad school, furiously hacking away to come up with something interesting to
say about definitionally uncertain stuff.

http://www.slideshare.net/jsmith54/huhdoop-uncertain-data-management-on-
nonrelational-database-systems

The furious pace and the pragmatic compromises are part of the fun. Compared
to things like [pitch events](https://medium.com/@porlando/eradicate-the-
startup-pitch-event-dd1a9c714788), hackathons have way less problems (even if
they have [their issues](http://thenextweb.com/insider/2013/12/02/amid-
controversy-dreamforce-hackathon-salesforce-awards-1-million-prize-top-two-
teams/) as well). At their best they’re about the love of unconstrained
creation. I’ve tried to do machine learning hacks because it’s just so damn
cool to go from zero to having a program that makes decisions. It amazes me
every time it works, and doubly so when I can manage to get something working
on a deadline.

Taking on a challenge like building a new model in a hackathon is also a great
learning experience, especially if you get to work as part of a strong team.
Machine learning in the real world is an even larger topic than its academic
cousin, and there’s always interesting things to learn. Hackathons can be
great places to rapidly iterate through approaches and learn from your
teammates how to build things better and faster. That’s pretty likely to come
in handy sometime.
