#  Programming Functionally (for food)

One of my main goals when finding a [job](http://toromon.com/why-im.html) [in
New York tech](http://toromon.com/new-new-york.html) was to actually get a
chance to program in a functional style, as part of my job. I've gotten a
chance to dabble with FP in jobs before, but before my current role, I had
never been at a place that considered FP a core part of its technological
practice. Having found such a place and spent a few months writing some code,
I wanted to give my (obviously extremely limited) perspective on FP in real
life, but I realized that there is a zeroth topic to address: what languages
are people actually writing functional code in?

## languages

I think the intersection of programming language enthusiasts and FP
enthusiasts is absurdly large. So when talking about with developers, I find
that the conversation quickly turns to specific languages.

### tree branches

Within the FP tradition, there are really two major branches. The oldest is,
of course, the Lisp branch. It wears its mathematical roots on its sleeve and
buys parentheses by the truckload. The slightly younger branch is the ML
branch. With its less radical syntax, I feel like its connection to the
mainstream of production languages is more apparent and less contentious.

But notice that I'm talking about the family trees here, and not specific
languages. If your focus is, like mine was, to find a job writing functional
code _and_ getting paid for it, then the list of actual languages is down to
basically two, in my opinion. Sound hard to believe? Here's my reasoning.

### popularity

Let's look through some data to get a feel for where you might actually be
able to put your knowledge of immutability and referential transparency to
use. A fair, but admittedly very imperfect, place to start is the [RedMonk
rankings](http://redmonk.com/sogrady/2014/01/22/language-rankings-1-14/). It
uses Github and StackOverflow data to get some idea of language popularity. I
think that these data sources are going to skew quite heavily towards what
people _want_ to use, not necessarily what the get to use on the job. That
said, here's the FP subset of the list.

>   13. Scala

>   14. Haskell

>   17. Clojure

I have one issue with this ranking, but it doesn't seem to mismatch my
intuition about people's tastes, so let's leave it at that for the moment.

How about another, more career focused ranking from the guys at
[CodeEval](http://blog.codeeval.com/codeevalblog/2014). Its list comes out to
something like this:

>   11. Haskell

>   12. Scala

>   14. Clojure

This is basically the same list, so that's good. We're starting to see some
concordance, but I still smell something fishy. Let's do something more adhoc.

To check for real, legitimate employer interest in these languages, I dropped
them into the [Careers 2.0](http://careers.stackoverflow.com/), the
StackOverflow jobs site. I've often felt like this site is a good bellweather
for which way the programming job market is going. Heck, you can even apply
for [my job](http://careers.stackoverflow.com/jobs/44335/data-engineer-intent-
media) on it (and you totally should, if you think you're up for the
challenge).

Here's the data I found:

Language Jobs

Scala

86

Clojure

24

Haskell

17

F#

10

This data has an interesting magnitude insight. Scala sure looks like a
mainstream language, based on this. Interestingly, I think that this data also
holds the answer to what's going on with Haskell. If you look into the jobs,
almost none of them are jobs where you _write_ Haskell code. Do you want to
know my theory for why this is?

> Employers want people smart enough to write Haskell, who are willing to
write something more practical.

I don't mean this is as any sort of knock against Haskell. I love Haskell and
think every good developer should study it. In fact, when I interviewed for my
current position, they asked me about my views on Haskell, because I had
mentioned it on this blog and, likely, because it was a good sign about my
passion for programming.

Those 17 jobs listing Haskell, some are actually Scala jobs, with many of the
rest coming from Jane Street, which is actually a pure OCaml shop (they're
also the source of those F#-tagged job posts as well).

## my point

So what was my point in going through all of that? Well, I wanted to draw a
reasonably bright line between those languages worthy of your study and those
languages that you might use to pay your rent. I am thrilled that I get to use
Clojure on a daily basis and still pretty damn happy that other people get to
use Scala to pay their rent. That's awesome.

I also really think that, if you have the time, you should totally study
Haskell, SML, Common LISP, hell, even Oz and Erlang. They're worth it.

_But_, if you really want to write functional code for a living, ideally ASAP,
well, then, I have only one piece of advice for you.

> Look to the JVM, young dev.

I think it's pretty clear, if you spend enough time looking into it, making a
living writing functional code is all about the JVM ecosystem. It's not hard
to figure out why:

>   * the huge investment in enterprise Java companies have made

>   * the Hadoop ecosystem (including spiritually related projects like Spark)

>   * the Java escape hatch, particularly when it comes to libraries

>   * the track record of the JVM and the knowledge many people have of its
internals

Those are good reasons, which is why your future boss has likely decided to
make the pragmatic choice, to use a functional language hosted on the JVM.

This narrow range of choices may seem artificially constrained to some, and it
is to a certain extent. But the upside is that people actually get to use
techniques like laziness, immutability by default, functional data structures,
and so on. It's too bad that there isn't a more ML-ish option available, with
Scala being a bit more of Java + ML, rather than ML on the JVM. But for
hardcore ML enthusiasts, there's always a few F# jobs and perhaps even the
occasional real Haskell gig. It's still great news for those of us excited to
do FP for a living and not just for fun.

I'm personally thrilled to have the opportunity to work with functional (and
logic!) programming for a living. I think the reality for most tech
organizations is that we're currently in a state of transition. We don't want
the next 20 years of software development to be about imperative OOP, but
there's a real need to work with what we've got to find a way forward. The JVM
functional languages are trying to do just that, and Cthulhu bless them for
it.
