# Oh. My. Blog.

### My first world (data) problem

* * *

I have a small problem with my current blogging workflow. It’s existentially
trivial, but I’d like to dig into a bit, as an excuse to talk a bit about some
of my favorite ideas from data engineering and databases. It’s my firm belief
that computer science has a number of really useful insights about [life, the
universe, and
everything](http://en.wikipedia.org/wiki/Life,_the_Universe_and_Everything),
but these [insights are often hidden by their context](http://toromon.com
/consistent-state.html).

In this post, I’m not going to try to solve everything, but I’d like to walk
through my current difficulties in how I blog, after laying a bit of
groundwork first.

## Lambda- the ultimate?

There is an idea discussed a fair bit in data engineering circles, called [the
Lambda Architecture](http://lambda-architecture.net/). It is meant as a sort
of solution to early problems in designing big data applications. One of the
most commonly accepted elements of the Lambda Architecture are that data is
inherently immutable and should be modeled as such.

* * *

![](https://d262ilb51hltx0.cloudfront.net/max/2000/1*Xfh8pv3PCMIQHr_qOEAqMw.jp
eg)

So, if our data is immutable, all operations, edits and removals (updates and
deletes in database lingo) are just new records added to the datastore. The
term for this property is append-only, which I like to think of as writing in
pen on a new page. This is, in fact, how I write paper notes, always using pen
and always turning to a new page for any revisions, instead of attempting to
mark up existing notes. Using this sort of approach encourages you to think of
all writing as a log of a stream of thoughts and actions, not their final
derived presentation (a view or materialized view).

Immutable data is a really fascinating concept, one I let rattle around in my
head a fair bit. It’s a big part of the appeal of Clojure’s use in modern data
processing systems. Working on mostly functional code that uses immutability
by default can offer a great organizing principle that helps you structure
your code. I think that the Clojure’s approach to types [has its
downsides](http://toromon.com/pointy-tools.html), but on the whole, there is a
lot of merit in modeling data according to this paradigm. One could certainly
argue that mutability simply does not scale, so big data intrinsically means
immutable (big) data. I think that immutability and other functional
programming concepts are tremendously important approaches to the problems
that face software engineers today. If you have an interest in data
engineering, you should be at least trying to understand functional
programming is all about, even if it’s purely [for careerist
reasons](http://toromon.com/fp-for-food.html).

* * *

## Independent data

Once you’ve made this sort of mental reorientation, it’s much clearer that
there is not a single constant presentation form of the source data. Your
notes could be presented in a number of forms: a blog post, a presentation, a
book, etc.

This all builds on the related concepts of [representation independence and
data abstraction](http://dl.acm.org/citation.cfm?id=512669). Think about
changing the theme of a PowerPoint or Keynote presentation. Obviously, there
is something underneath that is your real presentation, with the theming being
endlessly changeable.

[One of the most technically interesting startups](http://www.ingenuity.com/)
I’ve had the opportunity to work at put a lot of effort and investment into
building systems that structured some of the hairiest data around: the entire
molecular interaction graph. The solution at that company was to use
[ontologies](http://en.wikipedia.org/wiki/Ontology_%28information_science%29),
to represent a substantial fraction of all human knowledge about the science
of life. Tricky stuff, no doubt. If we could do something useful with
notoriously difficult biological data, surely there’s some way to make forward
progress with my little blogging problem.

## Blogflows

Originally, when I started blogging on [my own site](http://toromon.com/),
wrote all of my posts in
[reStructuredText](http://docutils.sourceforge.net/rst.html) and then used
[Pelican](http://blog.getpelican.com/) to process this source data into a
static website view of that data. The true source, immutable data was tracked
in version control, Mercurial specifically. Even there it was possible to
create more derived views, so I created an exported form of one of my
Mercurial repos as a Git repo, hosted on GitHub, instead of BitBucket. This
allowed me to go back to any point in time on any element of my work and
create new derived forms of that data, as I wished. This mental model of my
blog posts, as data commits to a Mercurial repo, was very easy to internalize
and allowed me to flesh out the other elements of the whole “blogging about
code” project. Version control systems are some of my favorite applications as
a developer, and [Mercurial is one of my
favorites](http://toromon.com/tag/mercurial.html).

The reason I stopped using this workflow was the composition interface. I
ended up writing my posts in reST using PyCharm, which was great for
maintaining a sort of representational independence but awful for helping me
visualize the post as it evolved. Yes, I could just rebuild my site on my
local machine and see my changes, but it ended up ultimately feeling like
sculpting via remote-control robot.

So I switched to writing here on Medium, almost entirely for the composition
experience. I can hear all of my vi and emacs using friends groaning that I
couldn’t handle a little bit of interface difficulty in my editor. But I think
this is a more serious issue than people give it credit to be. My concern
basically comes down to how the tool affects my [transcription
fluency](http://scholar.google.com/scholar?q=transcription+fluency). If you’ve
not come across this idea before, the research (as I understand it) points to
the speed and ease with which a person can transcribe their thoughts having a
huge impact on how well they can learn and grow. Here’s [a great summary of
the research](https://medium.com/message/the-joy-of-typing-fd8d091ab8ef), on
Medium.

## [Insert solution here]

What I wish this blog post was is an announcement of my new open source webapp
that solves this problem. It’s not. I couldn’t dream of writing a document
composition interface as beautiful and useful as Medium’s. So, instead, I’m
going to describe my wishlist of tools. My hope is that I can get some
feedback on how 80% of what I want can already be done. If I can get that far,
then I may be so bold as to take a crack at the remaining 20%.

### Composition

This is the killer part. Medium’s editor is incredibly useful. There’s nothing
even close, so far as I can tell. Ghost blogs approach the beauty of the
output, but the composition is back to being done in Markdown. But maybe there
is some awesome open source blog post editor out there. Who knows? If you do,
seriously, tell [me on Twitter](https://twitter.com/jeffksmithjr).

An interesting workaround might be to simply continue to use Medium as my
editor and then scrape the derived pages. Then, the HTML could simply be
translated to some representation independent format (like Markdown or reST),
afterwards. This sounds hacky, but perhaps doable.

Using Medium as my primary composition interface would be way less troubling
if Medium, like Twitter before it, had an API. If there was an API, then I (or
any other interested developer) could just suck back out the necessary post
data for use in other contexts. Am I unreasonably optimistic to wish that this
will some day be the case? Perhaps, but I hope not.

### Publishing

Once I have my data (blog posts) in a representation independent format, I
want to be able to publish derived versions (pretty web pages) in multiple
formats. This is pretty easy on my personal domain,
[toromon.com](http://toromon.com/). I have been using Pelican there, but it
would be relatively trivial to switch to some other static site generator.
Personally, I find Pelican to be a solid platform that’s very easy to use and
extend, so I’m not inclined to switch anytime soon. But I absolutely want to
maintain the ability to do so.

### Orchestration, etc.

Once I’ve gotten the above working as I’d like for my final workflow to go
something like this:

  1. Write the post.
  2. Translate to a representation independent format.
  3. Commit that data to source control and push to remote mirrors.
  4. Produce the derived views: my personal blog, Medium, etc.

The glue code to connect all of this seems well within my reach, so I hope to
be able to pull all of this together and then publish my solution, similar to
[my previous blog workflow](http://toromon.com/mirroring-to-git.html).
