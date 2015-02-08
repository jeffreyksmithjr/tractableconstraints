
## In Search of Diversity

A machine learning perspective on meaningful differences

* * *

![](https://d262ilb51hltx0.cloudfront.net/max/600/1*bKtfaHwz5JBMtBu7m5aLfA.jpe
g)

On this MLK Day, I want to talk about diversity, but not in the terms that
might have made sense to Dr. King. I’m a startup guy who spends his days
building machine learning models. Sure, as a person, I believe that [tolerance
of diversity is an important aspect of freedom](https://medium.com/tractable-
constraints/free-to-be-1e549cd94f97).

But I don’t want to stray too far from the areas I know. The problems that
tech startups face aren’t anything close to the challenges of African-
Americans fighting for equality, but they’re the challenges that I know and
can act on. So that’s where I’ll focus. Drawing liberally from AI, biology,
and the social sciences, I’m going to talk about the utility of diversity and
why we technologists and startuppers should care about protecting it.

### Ensemble models

In machine learning (ML), we build models. These are programs that make
decisions based on data. Typically, they learn from some set of past data and
are used on new data as it comes in. Over the lifetime of the field,
researchers have developed many approaches to learning from data. These
techniques (i.e. algorithms) are things you may have heard of: linear
regression, naive Bayes, decision trees, and so on.

One of the most important developments in the history of the field of machine
learning has been the development of ensemble learning methods. At its
simplest, ensemble methods are just using more than one model to make a single
decision.

One of the more interesting consequences of using multiple models in an
ensemble is that you may not be getting the supposed benefits of an ensemble,
even though you nominally have multiple models. How could this happen? A lack
of diversity.

#### Classifying cute

Let’s take for an example a simple classification problem. We’ll try to
determine if my dog looks cute in this dress:

![](https://d262ilb51hltx0.cloudfront.net/max/800/1*v07Ab_9X8bbkWa5Pdl9saw.jpe
g)

I’ve asked a bunch of people, and not one of has ever said that she looks
anything but very, very cute in this dress. So while we have multiple decision
makers, we’re not actually seeing a diversity of opinion.

The potential for lack of diversity has all sorts of implications for the use
of ensemble models. Put in terms of code, you can view the situation above
being analogous to the following two models:

Even if you don’t know
[Lisp](http://en.wikipedia.org/wiki/Lisp_%28programming_language%29), I think
that it’s not too hard to understand that these two models are exactly
equivalent. Each one will always return the same decision given the same data.
Given a dog, who is cute and is in a dress, these functions will always return
true. This means that we don’t really have two models here; we only have one,
written in two different syntaxes.

This observation leads to some interesting follow-ons. If these two models are
equivalent, just written in a different order, then we could come up with a
standard syntax, called [a normal
form](http://en.wikipedia.org/wiki/Normal_form_%28abstract_rewriting%29), that
always imposes the same ordering on the function applications (e.g. checking
to see if the dog is cute, then checking if the dog is in a dress). A normal
form for expressing these models makes it trivially simple to see when two
models are in fact identical. This process of going from multiple models
models into a normal form that allows the redundancies to be discarded is
called reduction.

So, sometimes we _think_ that we have multiple models, but since they all
agree, all of the time, we don’t. All we have is likely a slower, more complex
way of expressing the same decision making process.

### Diversity in startup teams

Zooming out of this somewhat abstract discussion of machine learning, it’s
easy to see how these concepts have clear corollaries in our working life.
Consider Max Levchin’s [infamous
lecture](http://blakemasters.com/post/21437840885/peter-thiels-cs183-startup-
class-5-notes-essay) on how PayPal succeeded because it lacked diversity:

> The notion that diversity in an early team is important or good is
completely wrong. You should try to make the early team as non-diverse as
possible.

> The more diverse the early group, the harder it is for people to find common
ground.

While I object to most of what he has to say on this topic, I do understand
the challenge he’s trying to characterize. It’s very hard to get a small group
of strangers to work together effectively to build something that’s never
existed before.

> Developing a shared vision of a startup and its technology is incredibly
hard stuff, and anyone who tells you differently probably hasn’t tried to do
it.

So Levchin’s view is that you need a team full of nerdy men (no women
allowed!) who all reach the same conclusions quickly. This allows them to
build trust and get to common ownership of the problems of the startup quicker
than a more diverse group. To me, this sounds a great deal like our multiple
models reducing to a single model. It also results in a organizational plan
that is classist, sexist, and a bit racist, but hey, Levchin made a bunch of
money, so who am I to disagree with his perspective?

#### Diversity’s difference

Instead, I’ll call out the work of the incredible [Scott E.
Page](http://vserver1.cscs.lsa.umich.edu/~spage/), in particular, his book
[The
Difference](http://vserver1.cscs.lsa.umich.edu/~spage/thedifference.html). In
it, he systematically defines and develops a theory of diversity and
demonstrates its utility in problem solving contexts.

In Page’s formulation, there are diverse perspectives and diverse heuristics.
You can think of perspectives as views of the world, whereas heuristics are
closer to approaches to a given problem. To understand how the two work, let’s
look at the following situation.

![](https://d262ilb51hltx0.cloudfront.net/max/600/1*MerjIw-
rVBwUtkyAbPkHSQ.jpeg)

These two canine citizens want to exercise their rights to participate in the
American system of representative democracy. Although they’re both Americans,
one from birth the other through naturalization, no one will let them into
their polling station.

So between them, they need to find a way to slip the chains of oppression,
make their voices heard, and vote for increased funding for dog parks in
Manhattan.

They are, according to the definition that we’ve been using so far, absolutely
an ensemble. In terms of perspectives, they do exhibit diverse perspectives.
The black dog thinks that they’re not being allowed in to vote because they
didn’t bring any bones for bribes, whereas the white dog thinks it’s because
they’re not tall enough.

They also exhibit diverse heuristics. The black dog favors just ducking out of
their collars and rushing the polling station. The white dog thinks that
attempting to persuade a human voter is the best approach and has been begging
to be taken in for the past ten minutes.

Whether or not these two ever get to participate in the democratic process, I
think that it’s pretty clear that they’re likely better off for their
diversity of perspectives and heuristics. The range of solutions that will be
explored by this diverse ensemble are going to more broadly explore the
problem space for potential solutions than either of the dogs would in
isolation.

Of course, the Levchins of the world have a point, in some contexts. If the
white dog can convince the black dog to share her perspective, then we no
longer have a diverse ensemble. What we likely have is two dogs stacked up on
top of each other, in a trench coat and a hat. That is bound to be an
impressive feat of balance, and maybe the VCs and the public markets will
reward this high-risk, high-return strategy. Maybe the polling volunteers will
be won over by this bold new vision of French bulldogs in trench coats. Or
maybe it will all come toppling down in a pile of fur and stolen clothes. Such
are the risks of homegeneity.

### Creating diversity

In neither machine learning nor in startups do we need to take things as they
come. When we find a lack of diversity, we can act to preserve the diversity
that we do find or even induce the emergence of diversity.

To do this for ML models all we really need is some sort of metric to evaluate
the amount of diversity in a given set of models. Some examples might include
simple percentage agreement, variance, separation, or any one of several
common distance metrics for comparing vectors of predictions. From there, we
can try to construct the set of models with the maximum amount of diversity
through things like random selection of training instances, varying fitness
function parameters, etc. Depending on how you approach this problem, you
might run into computation explosion, but there are definitely “good enough”
solutions possible that can consistently produce diverse ensembles of models.

So then, what are the corollaries for a startup or a tech team? If preserving
and inducing diversity is a tractable problem for ML models, how about
something more complex, like people?

> How can we encourage diversity in our tech teams?

All of us in tech now know that we have a problem with achieving meaningful
diversity in technology company employment. Imbalances occur in gender, race,
and other harder to characterize elements of diversity. It seems like this
every week, there’s [some new discouraging report](https://blog.hired.com
/market-trends-report-quantifying-gender-gap-in-tech/) about just how
insidious this problem is. Diversity in technology is a big, hairy problem
that some of the richest corporations in the world haven’t cracked. I won’t be
solving it in this blog post, but I’d like to propose one strategy to make
things better.

#### Islands unto themselves

Being a former biology guy, I’m inclined to look to evolution for the answer
to this problem. Fun fact: evolution _loves_ diversity. In fact, it can’t
happen in the absence of diversity. Random mutations are absolutely critical
for the emergence of life from ooze.

Getting a bit closer to the mechanics, diversity in the population as a whole
can often come from protected sub-populations (sometimes called demes). The
classic example comes from Darwin’s observations of the various species on the
Galápagos Islands that led him to develop his theory of natural selection.

![](https://d262ilb51hltx0.cloudfront.net/max/800/1*X1jwd8WdamrUbiRbcFaPIA.jpe
g)

“Darwin’s finches by Gould” by John Gould (14.Sep.1804–3.Feb.1881) — From
“Voyage of the Beagle” as found on <http://darwin-
online.org.uk/converted/published/1845_Beagle_F14/1845_Beagle_F14_fig07.jpg>];
also online through Biodiversity Heritage Library at
<http://biodiversitylibrary.org/page/2010582>.. Licensed under Public Domain
via Wikimedia Commons — <http://commons.wikimedia.org/wiki/File:Darwin%27s_fin
ches_by_Gould.jpg#mediaviewer/File:Darwin%27s_finches_by_Gould.jpg>

Small populations, which have often gone through some sort of [population
bottleneck](http://en.wikipedia.org/wiki/Population_bottleneck), are less
diverse than the population as a whole, but as they continue to evolve they
can evolve differently than the main population, adding to the overall
diversity of the entire population. By only having to solve the distinct
problems of their habitat, they create potentially novel, unique solutions
that the main population might never have found.

#### Evolving tech teams

Taking the lead from evolutionary biology, I would propose that a powerful
strategy for encouraging diversity in teams is to break them down into
smaller, more autonomous units with local decision-making power.

Recently at [Intent Media](http://intentmedia.com/), we started making some
big changes to our application and organizational structure along these lines.
Part of the motivation was Conway’s law. In its original formulation, Conway’s
law is:

> …organizations which design systems … are constrained to produce designs
which are copies of the communication structures of these organizations.

So, if our application architecture is going to reflect our org chart, and we
don’t want a non-scalable monolithic architecture, then we don’t want a non-
scalable monolithic org chart. We want small, agile, autonomous teams free to
take on all sorts of responsibilities and decisions at the squad level.

It’s definitely early days for us, but I’m optimistic that this will be the
right approach for taking this startup to the next level (i.e. total world
domination). It takes advantage of some of the benefits of the shared
worldview that Levchin wistfully describes, allowing teams to build trust more
effectively. But I also hope that it will create a more welcoming environment
for a more diverse range of team members.

For example, the data engineering squad that I’m on has historically shared a
love of beer, beards, and well-tested functional code. However, as our team
grows, we may have to adapt our micro-culture to accommodate people who don’t
love beer or beards. As we search beyond South of Houston to as far as South
America, we will find individuals who will make great team members but are
different than the people currently on the team. That will mean that our squad
cohesion may now need to be based around a shared love of falafels, lap dogs,
and well-tested functional code. This is a totally feasible adaptation that
will allow us to survive and grow, made all the easier by our relatively small
size.

![](https://d262ilb51hltx0.cloudfront.net/max/800/1*_5KRMmWliDg0HiP7k5iNnA.jpe
g)

Photo from Intent Media

Small teams like ours also mean that another squad can bond over something
like biking around Brooklyn and that doesn’t prevent a non-cyclist from
finding a social group he or she can engage in given the diversity of the
larger technology organization. In technical terms, this allows different
squads to choose Clojure, Ruby, Java, or whatever other tool they think makes
sense. Other big ambitions are to enable a micro-services architecture and
support a true DevOps mindset, where squads have more locally defined
ownership of their applications’ operations.

Moreover, small teams can make more democratic and egalitarian approaches to
decision making easier. I’ve talked about this in some detail [in another
post](https://medium.com/tractable-constraints/many-voices-equally-heard-
ab7feb615808), but the short version is that I firmly believe that in teams
and in societies everyone should have a voice. Small teams, unconferences, and
other egalitarian organizational techniques can create fairer, more productive
groups of people, who solve their problems effectively as a group.

When you’re in a fast moving startup, getting the right people into the
company is crucial. People with the abilities to build a successful company
can be hard to find. So you simply can’t afford to not be a welcoming, open
place for people of all races, genders, and backgrounds. The people who thrive
in fast moving startup environments are the ones who want to connect with
their peers and build something collaboratively. They deeply appreciate the
opportunity to work in diverse teams that help them grow as a professional and
as a person. When recruiting great people like this, I think it can be crucial
to show them small, agile teams where they will get to have a real impact,
regardless of their background, because that’s the sort of opportunity that
they want and deserve.

### Big, hairy problems

I love working in startups and on machine learning problems. In both of the
contexts, you’ll find smart, motivated people who are optimistic about their
chances taking on what are, frankly, big, hairy problems. In machine learning,
we’ve developed approaches that preserve and induce diversity in our models.
This has led to the tremendous success of techniques like [random
forests](http://jmlr.org/papers/v15/delgado14a.html).

In technology organizations, I think that we still have a lot of work to do to
really understand and apply the insights of research into the power of
diversity. I believe that small, autonomous teams are a great tactic for
structuring our organizations in ways that encourage more diversity. Beyond
that, I’m optimistic that we can continue to iterate and find new approaches
to building more diverse tech teams. Moreover, we should. Diversity is
important and worth working for.

* * *

_Much of the discussion above about machine learning is based on the work of
__[Moshe Looks_](http://research.google.com/pubs/author37920.html)_, __[Ben
Goertzel_](http://wp.goertzel.org/)_, and their collaborators on __[the MOSES
application_](http://wiki.opencog.org/w/Meta-
Optimizing_Semantic_Evolutionary_Search)_._
