# Stupid Engineering Tricks

### Ignoring scalability and scraping myself

* * *

I’m a bit of a contrarian, even when it comes to engineering. Though we might
pride ourselves on our intellectual independence, we engineers can be just as
driven by the herd as anyone else. How else did we all end up writing Java for
a living? So, I think it’s important to really highlight when you believe in a
different engineering approach than the norm, even when the issue is trivial.
Tunnel vision is a real danger in engineering large systems and can lead to
tons of waste.

In this post, I want to get back to a small problem of mine but then build up
to a more lengthy discussion of a more difficult one. My goal is to share a
bit of my perspective on why the engineer’s instinct to automate and optimize
shouldn’t always be listened to.

## Composition

In [my previous post on my blog workflow](https://medium.com/data-
engineering/42e5e059d240) I described my thoughts around how I’d like some of
my personal data to be managed, specifically my blog posts. To recap, what I
want my blogging workflow to look like is something like this:

  1. Write the post.
  2. Translate to a representation independent format.
  3. Commit that data to source control and push to remote mirrors.
  4. Produce the derived views: primarily my personal blog.

The astute reader who knows something about [static site
generators](https://www.staticgen.com/) might be scratching their head at why
I’m making this problem so hard. After all, most static site generators allow
you to have this workflow:

  1. Write the post in a representation independent format (Markdown).
  2. Commit that data to source control and push to remote mirrors.
  3. Produce the derived views: my personal blog, Medium, etc.

It’s one less step, and it’s the default workflow for all of these tools. If I
want to see the effects of my changes, the final renderings of my posts, I can
just keep a browser tab open which will show me the pretty HTML version of my
markup language post. What’s my problem with that?

That’s certainly an acceptable approach, depending on your personal tastes. I
was using that workflow [for a while](http://toromon.com/tag/pelican.html),
but I moved away from it very intentionally. The WYSIWYG editor on Medium has
been a joy to use since the launch of the site, everything that it [was
promised to be](https://medium.com/about/writing-in-medium-df8eac9f4a5e).
There’s even reasonably active [open source
clones](https://github.com/daviferreira/medium-editor) of it, and I’m
optimistic that open source world will someday be able to produce a truly
equivalent application for composition.

The closest equivalents I can find that still work with static site generators
and store post data as reST or Markdown are [Prose](http://prose.io/) and
[Pagoda](https://github.com/alagu/pagoda). In both, you’re still writing in
Markdown and seeing the results just a bit easier. That’s fine for a lot of
people, but it doesn’t have the fluidity and ease of Medium. As I went through
in the previous post, I believe that I benefit from trying to optimize for
[transcription fluency](https://medium.com/message/the-joy-of-typing-
fd8d091ab8ef). With a great editor, I am a faster and, thus, better writer. I
recognize that some people blog in Markdown for that exact reason: they are
fast and fluid in Markdown. For me, that’s simply not the case. I’ve found
myself won over by the argument that beautiful typography and perfect
representations of my text will allow me to reason more clearly about what I’m
writing. It absolutely means that I’m going to be in for more hassle than the
serious static site bloggers, but I’m onboard with that.

## Extraction

Beyond the compositional experience, I have another reason for harping on what
is, admittedly a total [first world problem](http://first-world-
problems.com/), and that reason is why I’m discussing this issue in the
context of a data engineering collection. I have some experience of the power
and pain of extracting valuable data from its messy context.

### The Facts of Life

As I described in [the previous post](https://medium.com/data-
engineering/42e5e059d240), I used to work at [Ingenuity
Systems](http://www.ingenuity.com/), a startup that built applications on top
of some of the most important knowledge the human race has ever produced: [the
molecular interaction graph](http://en.wikipedia.org/wiki/Interactome). The
utility of such an application is not hard to understand, even if the
terminology is a bit imposing. Having a way to dynamically explore biological
experiment results in the context of every other molecular interaction known
from previous research is an amazing tool to add to the researcher’s toolbox.

So, obviously, this sounds like a valuable application, but having utility is
not all that’s required to get things like funding, paying customers, and [a
successful acquisition](http://www.genomeweb.com/informatics/qiagen-buys-
genomic-data-analysis-firm-ingenuity-systems-105m). There must be some hard
work in there somewhere, otherwise people would just build their own or grab
[some open source software](http://www.cytoscape.org/) that’s good enough. In
this case, the hard work was our commitment to [doing things that didn’t
scale](http://paulgraham.com/ds.html).

You see, important biological facts are not all already encoded in nice
databases. Many of them are in books or papers. When they are in databases,
they are in many different databases from different sources, focused on
different sub-domains. The life sciences have one of the hardest data
integration problems around. Where you want to wind up is with some nice clean
representation independent encoding of some molecular interaction like, “MDM2
binds to TP53.” But it rarely can just be downloaded as such. Instead,
researchers write papers where they discuss all sorts of details that might
point to, but not prove, such a conclusion.

Moreover, the breadth and amount of data keeps increasing at a mind boggling
pace. Even by software standards, the pace of progress in life sciences data
production is fast. When I was at [Ion
Torrent](http://www.genomeweb.com/sequencing/life-technologies-acquire-ion-
torrent-725m), we would often talk about bringing Moore’s law to genome
sequencing, which was kind of ironic, since we were already beating Moore’s
law, as an industry.

![](https://d262ilb51hltx0.cloudfront.net/max/800/1*WshOo4Cw0MPrS68NIQA3JA.jpe
g)

<http://www.genome.gov/sequencingcosts/>

In the face of that blizzard of progress, Ingenuity bravely chose to do some
very manual, labor-intensive stuff. Biologists would read research and encode
the facts in them as data, into a proprietary ontology. Talk about not
scaling! If you wanted to double your throughput, you would need to hire at
least twice as many biologists if not more, given the learning curve involved
in such an esoteric job.

This sounds like a recipe for failure, but it turned out to be a recipe for
success due in no small part to it sounding like a really tough chore. Your
customers definitely don’t want to do the work themselves, unless they have a
comparable scale. And even then, why would they, when you’ve already done it
for them? This sort of non-scaling labor also serves as a nice moat against
new competitors. Even if they’re willing to take on the task, they’ll start
off well behind you in a long task with the only way of catching up being to
hire even more people than you have.

You might think that such a human-powered approach leaves you vulnerable to
disruption from some more technologically enabled approach, such as natural
language processing. It’s a fair point. NLP definitely has some utility in
this domain, but there are real problems as well. Interaction fact data is
already very, very noisy, and machine-driven fact extraction may compound this
problem in ways that leave the resulting graph unusably inaccurate. Moreover,
a biologists weighting function for the value of particular nodes and edges on
the graph can be idiosyncratic, complex, and totally unforgiving. As you might
imagine, scientists tend to entirely disregard any source of “knowledge” that
completely blows some very basic fact, which is a danger NLP-based approaches
will constantly leave you exposed to. Again, NLP definitely has a role to play
in biological research, but machine doesn’t always triumph over man to make
the better business.

### Beyond Biotech

Choosing the approach that doesn’t necessarily scale has examples in machine
learning as well. Most machine learning/data science groups are spending a lot
of time thinking about how to build modeling systems at scale using some sort
of distributed system. This is definitely something we’ve worked on at Intent
Media. Our implementation of [ADMM for
Hadoop](http://tech.intentmedia.com/post/68173521153/distributed-
classification-with-admm) came out of that work, but that’s not to say that
ever modeling problem requires Hadoop or Spark. Many of my suggestions for
doing [machine learning at hackathons](https://medium.com/data-engineering
/modeling-madly-8b2c72eb52be) have relevance outside that narrow context. In
particular, there’s still all sorts of use cases in which a model learned on a
single machine instead of a distributed system would be entirely sufficient
for the purpose. When you can find those use cases, it can be a huge win for
your team or application, because you typically wind up with something that is
simpler, easier to reason about, and more readily replaced, should the need
arise.

Another place to see this phenomenon is the incredible examples of design in
technology products. An incredible but singular designer is precisely the sort
of non-scalable resource that the engineer wants to find a way around, but
clearly such people are at the heart of all sorts of recent technology
successes. If you look at where so much of the value in say the Nest or Beats
acquisitions originates, much of it comes from people developing amazing
product visions that become compellingly designed products. Is finding a bunch
of people like that challenging? Sure. But there is often no substitute for
the unique contribution of a talented professional. There shouldn’t be.

### Mirror Blogiverse

Let’s descend from this discussion of biological fact extraction back to my
little blogging problem. Focusing on Step 2 from my list above, I need someway
to get the meat back out of my Medium sandwich. That is, I need to scrape my
own posts and toss out all of the extraneous crap. This sounds like a common
enough problem; there should be something on GitHub that does that, right?

Sorta. One fairly powerful tool you could use for a job like this is
[Pandoc](http://johnmacfarlane.net/pandoc/index.html). In my testing, I
couldn’t figure out how to get sufficiently clean results from it. It’s
probably possible. Pandoc is written in Haskell, so it could probably do your
taxes or solve global warming. I just couldn’t figure out how to tell it what
I wanted. Instead, I found a fair bit of success with an old script of Aaron
Swartz’s [html2text](https://github.com/aaronsw/html2text). It’s small,
comprehensible, and very purposeful. A Python script written by [a tragic
technology hero](https://medium.com/tractable-constraints/free-to-be-
1e549cd94f97)? How could I go wrong?

There was one more wrinkle I ran into. You see all of that other stuff on the
page that’s not this blog post? That’s going to come in to, if I just point
the script at the public URL of a post. The nicest workaround I’ve found (that
doesn’t involve writing a Medium specific parser, ugh) is to use the Export
content feature within my Medium settings. It produces a plainer HTML export
of all of my pages, leaving very little to clean up before feeding the
Markdown file to Pelican for posting on my blog. Obviously, I have some things
to work out, but feel free to check out [this test post](http://toromon.com
/oh-my-blog.html) on my personal blog.

* * *

Scalability is a totally valid engineering goal, one that I think about a fair
bit in my job. But it’s not everything. When it comes to succeeding as a
startup, producing a valuable product that enough people demand for a high
enough price is everything. So many other things have to be secondary. If it
takes a bit of manual work, I think that there’s lots of reasons to be fine
with that, as long as the motivations are clear. This situation is probably
worse if you’re living on the bleeding edge using things like Spark, Cascalog,
and Vert.X. You’ll need to dive into building out solutions that may not
survive the next doubling in your product’s volume. But if you do hit that
inflection point in adoption, well, that’s what they call a good problem to
have.

My point is simply that we, as engineers, should have some perspective on the
system as a whole. Sometimes that system is, in fact, a whole startup with
people doing things that don’t scale, like talking to customers, staying up
all night fixing database problems week after week, and so on. Sometimes, we
need to attack these as the clearly automatable problems that they are. But
sometimes, it’s worth everyone’s time to just do the manual work.
