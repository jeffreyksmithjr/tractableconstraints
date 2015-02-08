## A Cladistics of Mistakes

#### Classifying model failure modes

* * *

Building real-world machine learning systems has a number of unique
challenges. Unlike the related academic implementations, real-world modeling
systems often make money when they do what they’re supposed to and lose money
when they do not. The latter scenario is the focus of this post: how modeling
code can fail.

I propose that modeling code can fail:

  * as software
  * as a model
  * by association

While I’ll certainly draw from my personal experience, I’ve tried to not just
record all of the bugs I’ve ever seen. Instead, I’ve tried to highlight
classes of errors and generally useful strategies. My hope is to propose some
worthwhile suggestions on where you might want to spend your time, when you
decide you want to make your modeling code safer.

### Failing as software

This is the easiest sort of failure to understand. It’s common to all sorts of
software, not just data science applications, which means that most
organizations are already organized to address this risk. This is at the heart
of most QA group’s mandate: make sure the software doesn’t crash in
production. Data science/machine learning groups have the same need for this
function as any other group within a software development organization. Rather
than try to summarize this large and important portion of the software
development function, I’m going to point you to the best book I’ve read on the
topic: [Agile Testing](http://lisacrispin.com/agile-testing-book-is-now-out/).

However, I do think that it’s worth calling out some of the characteristics of
modeling applications that should guide their testing (automated and manual).
The first good news about testing a modeling application is that it often has
far less branching logic than, say, a GUI application. It’s usually command
line software executed in a known, in-house environment, called with roughly
the same arguments on some sort of periodic basis. It should run from the same
starting point to the same ending point in about the same amount of time for
every single execution. As a testing challenge, modeling code looks pretty
damn easy from this perspective.

But, of course, it’s not so easy. The one thing that is guaranteed to change
in modeling code is the data. A junior QA engineer may not understand the why
and how of this issue, and so I think this is a crucial issue to highlight
when people start testing modeling code. Why does the data change all the
time?

> If the data didn’t change, we wouldn’t need to model it all the time.

> We would just model it once and then move on to harder problems.

To be explicit, the data is going to change, because the real world of our
problem domain is in some sense dynamic. This is best understood by thinking
of the converse situation.

Think back to high school physics. Your teacher was able to confidently and
accurately tell you that force equals mass times acceleration. Maybe he or she
dropped an apple or just told you the gist of the thing; it doesn’t matter.
I’m sure your teacher was dead on. We have more than just an approximate
understanding of the relationship. When it comes to force, mass, and
acceleration, we’ve got that one down to an arbitrary level of precision.
There’s no need to either capture more data or to continue to evaluate the
model for potential improvements.

Contrast that with the sorts of tasks we’re usually charged with when
constructing modeling applications. For one thing, our model isn’t complete;
it’s approximate. It describes _a part_ of the relationship of our inputs to
our outputs. More precisely, it captures part of the relationship of a single
set of inputs to a single set of outputs (old ones, in fact). The data that
this model is going to be used on in production is, by definition, not found
in the testing set. It does not exist yet.

#### Test plan of attack

The specific software failure issue that this brings up is that varying inputs
have the potential to produce radically different outcomes. Boundary testing
is a great place to start to start to build up some safety measures to protect
your application from the unforeseen effects of dynamic data inputs. Even
terribly sophisticated, super impressive modeling code written by people who
know all the math in the world can easily be thwarted by something as simple
as an input value being zero or negative.

It’s also worth calling out that outright failure (i.e. a crash) is just one
way that modeling code can suffer from a software failure. Depending on the
application, it may be more likely that a job run very quickly or even
indefinitely, requiring a fairly clear understanding of what a successful
execution looks like at several levels. One strategy that I’ve seen used to
good effect in this area is to maintain golden datasets, inputs that represent
some sort of well understood situation within the organization. This can allow
for very easy but powerful smoke or canary tests. The test expectation can be
something like, “If this job ever takes over an hour, it’s almost impossible
that we’ll be in compliance with our contractual SLA.” The key, in my opinion,
is for the data being used in these sets to be so frequently used and
referenced as to represent a sort of organizational shorthand for some aspect
of the larger mission. This allows people to understand the success and
failure of a modeling application that otherwise might be treated as
mysterious black box, best not commented upon for better or worse.

Ultimately, I think this is the hardest issue with modeling systems from a
software quality perspective, finding a way to reason about the black box. A
successful QA strategy will almost certainly have to involve working with
development to make the opaque transparent, the implicit explicit. It’s a
challenge for data engineers to develop the functionality that will make it
clear whether or not such a complex and variable system is working as
intended. Being easily testable is rarely the priority when kicking off a
major modeling system development project, given the other challenges being
taken on. But considering how such a complex application could and should be
tested, as early in the development process as possible, can absolutely
improve the design of a modeling application. A successful modeling system
will continue to be developed for years to come, meaning many, many cycles of
development, QA, and deployment. The amortized costs of building in validation
of the modeling system as a piece of software will easily pay for itself over
time.

### Failing as a model

If you’re from more of a data science background than a software engineering
background, you’re likely to think of model failure in an entirely different
way. You may have nodded your head at some of the points in the previous
section, but you were probably wondering about the model as a model. It has
semantics, it was supposed to optimize a particular objective function, its
performance relative to the expectation can and should be measured.

Much like the discussion software testing, we have found ourselves solidly in
the middle of a huge professional and academic domain. A blog post isn’t going
to be enough to cover all that you might want to consider, so let me break
down the topic in a different context than my usual bailiwick of tech
startups.

#### Taking and making money

Consider a financial trading organization. In such organizations, quants (what
data scientists were called when they had to wear suits) develop models. Those
models are then let loose on one of the most dangerous decision making
problems around: using a little bit of money to risk a lot more money. This
has been known to be [a difficult process to get
right](http://en.wikipedia.org/wiki/Financial_crisis_of_2007%E2%80%9308). What
do financial organizations typically do to try to keep their models from
putting the company out of business?

At an organizational level, there are usually some variant of model validation
and risk functions that exist to prevent various sorts of problems. Some of
the tasks that they do are in fact regulatory requirements. One might think
that such process formality and organizational commitment would result in only
safe and well-understood models making it into production, but history has
shown that [this simply isn’t the
case](http://en.wikipedia.org/wiki/2010_Flash_Crash). All sorts of problems
occur with trading strategies (read models) in use in production, even if they
usually don’t make the news. These are models that were typically optimized to
make money and they do the opposite. From a model performance perspective,
that’s about as bad as it can get.

#### Modeling success

So how do models fail as models and how can we prevent our models from failing
in the same way?

At a base level, it’s safe to say that any data science/machine learning group
can find themselves in a development processes that leads to
[overfitting](http://en.wikipedia.org/wiki/Overfitting). My suggestion above
about golden datasets certainly contains that risk. Whenever you give any
dataset or data point disproportionate attention, you’ll likely find yourself
going down a road that can lead to overfitting. But the risk of overfitting
can come in much subtler forms. It can be a major client with specific
business rules that end up getting embedded into your application in subtle
and unspoken ways.

I think that an intellectually honest strategy to prevent pervasive
overfitting can’t begin with technological solutions. At it’s heart, the set
of decisions that lead to overfitting have to do with what we call valid
inputs, how arbitrary parameters are determined and where they live, and so
on. Social processes within the group lead to these decisions, and only in the
social function of the data scientists, engineers, product managers, etc. can
these challenges be addressed.

That’s not to say that I see no benefit in purely methodological approaches.
There’s obviously an enormous amount that you can do within your model
research and development to ensure that your model has all sorts of properties
that make it safer for your use case. To take just one example, I think that
[the research around using ensemble
models](http://dl.acm.org/citation.cfm?id=956778) to mitigate the consequences
of [concept drift](http://en.wikipedia.org/wiki/Concept_drift) is really
exciting. Such an approach seems like a totally valid and worthwhile priority
for a data science team to allocate real time and effort towards exploring
building into their system. Stable models in the presence of concept drift
could be hugely useful to your organization.

#### Culture

Jack Welch [has been known to
say](http://www.forbes.com/sites/stevedenning/2012/04/26/jack-welch-ge-the-
corporate-practice-of-public-hangings/):

> Culture drives great results.

The corollary is that bad culture drives awful results. Take, for example, the
case of [the infamous London Whale](http://www.bloomberg.com/quicktake/the-
london-whale/). Some might read it as a story of a single, rogue alpha male
with an inappropriately large line of credit for the world’s largest casino. I
think the real story is one of an organization that didn’t care about the
analytical processes used to come to financial decisions, that didn’t care
about staffing and empowering the people who were in charge of safety and not
revenue, and that didn’t care about the quality or execution of its tools to
assess risk.

Put in its positive form, people in your organization need to care about the
consequences of bad models. Building out tools and processes to maintain
stable, safe models requires investment and prioritization. In any group
working on time series data, I would propose that investment around preventing
[data leakage](https://www.kaggle.com/wiki/Leakage) could make a great first
project. It has the advantage of being a somewhat tractable problem that can
be addressed through some well thought out data infrastructure approaches
while still being a very real and important problem.

Whatever the scope of tooling put in place to address the potential ways a
model can fail as a model, I would still like to think of these as funny-
sounding cousins of integration or acceptance tests. There’s no reason that
the tooling around assessing a model’s feature utilization can’t be included
in an automated test suite, executed as part of continuous integration,
organizationally visible. I fully appreciate that getting to that point is
much harder than it sounds for modeling applications, but I think that it’s a
journey with taking.

### Failing by association

This category of failure is hardest to characterize, which is why I left it
for last. It can be the most amorphous, but it can also be the most important
to focus on. Moreover, where the natural owners of the first two types of
failures are QA and data scientists, respectively, this class of failure is
logically something that should be the primary concern of a data engineer. So
now that we’re firmly back on my territory, what exactly does it mean for a
model to fail by association?

My conception of the idea is that a model fails by association when some other
component of the overall modeling _system_ fails. At a first glance, this
might be confused with my first class of errors, failure of modeling code as a
software application. The distinction I’m trying to make is between the model
itself and the system as a whole. Machine learning code can be the absolutely
critical heart of a system, but it’s rarely the _whole_ system.

#### A bug not a feature

The closest subsystem to the actual modeling code is the feature generation
code. This is the code that takes raw inputs of some sort and produces
semantically meaningful derived feature values to provide to the modeling
code. Although feature engineering is not a huge focus of most academic
courses on data mining or machine learning, it can be a substantial fraction
of the work content for a professional data scientist or data engineer. When
feature engineering is discussed in academic contexts, it’s usually in a
fairly abstract manner that focuses on the mathematics of some transform (e.g.
normalization).

The problems that can come up in feature engineering can be far more
pedestrian than the literature might lead you to assume. Sometimes the feature
is nominally being extracted (also sometimes referred to as a signal being
generated), but it’s suffering from some very basic failure. Here are a few
brief scenarios that are entirely plausible, in my opinion. Most of them focus
on the issues that can crop up with the feature extractor, the implemented
software which performs the feature extraction/signal generation. This is
because this lowly component of the application is where the rubber actually
hits the road with a lot of machine learning systems, where things go from
concepts to code.

**The inputs are incomplete or corrupt, leading to a garbage in, garbage out scenario.** The occurrence of this sort of failure is just so much more common than most people would believe before they do data-intensive software development. Redundant sanitization or at least verification of valid inputs (once on the original data acquisition and again on ingest into the modeling pipeline) can be a totally worthwhile addition. Rather than being gold-plating, addition layers of safety on both sides of the API, even when you are implementing both sides, can do a lot to capture what is really well-formed inputs, from the model’s perspective.

**The extractor fails in some intermediate step and falls back to a default or neutral value.** Such degradation in cases where the feature can not be successfully extracted may be a desired and useful component of the functionality. But if the rate at which it’s occurring is not exposed at some high level, all values could be defaults, likely leading to a pretty poor model.

**The extractor was never implemented according to the designed semantics.** Again, you might find this scenario implausible, so if you do, I’d suggest the following experiment. Get a data scientist, engineer, and product manager into a room and have them each describe how a given feature is actually derived. In my experience, 100% concordance should be a fairly rare occurrence. Obviously there’s a variant of this problem where the extractor was implemented correctly, but only for inputs in a certain domain. An even subtler version of this problem can crop up where the same semantics have been implemented differently in different extractors. Well structured code with an emphasis on code reuse and clear conventions around common functionality can do a lot to prevent this issue from creeping into the application.

**The feature set is wrong. **Depending on the design of the application, this could be due to how the feature extractors were called, how their inputs were prepared, or other aspects of the environment. This is very likely to be a silent failure, making it all the harder to find. Without functionality designed to make this information explicit, the feature set used in model, during learning or evaluation, might be very difficult to impossible to assess. Focusing on ways to reliably and transparently compose feature sets is a worthwhile priority for a data engineering function. The failures it causes are subtle and expensive to find, and the sorts of design decisions that come out of a prevention strategy can lead to better, more comprehensible code.

#### Coupled to a failure

Beyond feature-based failures of the related subsystems, there’s still an
exciting world of all sorts of other ways that the supporting software can
fail to provide the model with what it provides. One of the most vivid
examples of a software failure in recent history is [the collapse of Knight
Capital](http://dougseven.com/2014/04/17/knightmare-a-devops-cautionary-
tale/). Essentially, an overly manual deployment failed, bringing down a huge
trading with enormous losses. Some have focused on this episode from the
perspective of DevOps, which is certainly valid, but I’d like to highlight the
perspective it provides on the extent of real-world intra-system coupling.
This single botched deployment had such a huge impact in part because the
malfunctioning system interacted with a huge range of external systems that
took automated action based on this rogue application. A similar phenomenon
was observed in [the 2010 Flash
Crash](http://en.wikipedia.org/wiki/2010_Flash_Crash). Applications _across
different, competing companies _reacted to each other’s behavior in
unpredictable and extremely damaging ways.

The danger of this sort of failure due to tight external coupling is not
unique to programmatic trading. Most of the failures described in the section
above on features could easily originate outside your organization. Many
technological organizations are built around hitting an external API for this
piece of data, querying a hosted service for that piece of internal data, and
so on. It’s not hard to see how an issue in one of those external services
could creep into your modeling application.

A similar point could be made about the issues of concept drift and data
leakage, discussed in the section of models failing as models. In the case of
concept drift, the outside world is literally changing in some way,
potentially invalidating the assumptions your model was built upon. That
outside world may be another system, even one feeding back into your system in
the same way that low-latency trading algorithms have been known to do.
Designing safety mechanisms designed to address problems like these is
definitely challenging, and I can’t claim any personal experience. That said,
I do think that much of the basic sanity checks on the data, the model, and
the larger system that I’ve suggested would go a long way to putting you in a
better place, should you find your system interacting with a rogue external
system.

* * *

A machine learning system is a very unique application to implement, no matter
what your role or background is.

  * From a QA perspective, it’s unusually and unpredictably sensitive to input data, while at the same time being inordinately opaque.
  * Performing data science in a professional setting can require a different set of techniques and priorities than might be used to publish a paper.
  * Engineering a system this complex requires thinking about an incredibly broad array of related systems and their potential interactions.

Looking back on all of the issues that I’ve tried to characterize, I’m happy
to see many things which have realistic, affordable solutions. None of them
involve curing cancer or rewriting Linux in Haskell; they just require a solid
focus on the distinct challenges of implementing machine learning systems and
a motivated team.
