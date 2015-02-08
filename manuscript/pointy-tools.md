##  Pointy Tools

After spending a bit of time blogging on Medium, I thought that I would return
to this venue for a post on something ever so slightly more technical. In
particular, I want to discuss my love-hate relationship with pointy tools.

### demo

Are you on a Mac right now? You are? Great. Let me show you something awesome.
Open your terminal. You don't know what that is? No biggee. It's just an app.
It comes baked into OSX, so you can just open it up. Okay, now type this and
hit enter:



    rm -rf /


* * *

OMG, WTF, right? If anyone did that, they would be seriously screwed up.
That's a problem. But of course, it's a solved problem. Sorta.

I bring up that old rm rf chestnut for a reason. There is a community of
people who are dangerously in love with pointy tools like Unix file deletion.
Who are these nefarious souls? Highly competent professional programmers,
mostly.

### git pushiness

My immense distaste for Git (and preference for [alternative
tools](http://toromon.com/tag/mercurial.html) is reasonably well documented.
That said, I've been making a living at shops that use Git for some time now.
It's a necessary evil, but make no mistake, it's still evil. While I think its
immense learning curve and awful interface are the most common problems that I
have to face on a day to day basis, they're far from the only ones. How about
this totally reasonable mistake?



    git push -f origin master


In case you're not super clear on this particular clusterfuck, someone just
forcibly rewrote the history of your canonical repo. Why would someone do
something so obviously sociopathic? Well, one reason is that this is a totally
normal command:



    git push -f origin feature_branch


Got that?

Force push to feature branches? Do it all the time.

Force push to master? War crime.

If you're not feeling enough of a burn, I encourage you to check out [Steve
Bennett's blog](http://steveko.wordpress.com/2012/02/24/10-things-i-hate-
about-git/) for a more thorough discussion of the pain of Git.

Git is very much in line with the Unix philosophy. It's meant to be a pointy
tool, only suitable for use by super humans like Linus Torvalds and Ken
Ritchie. It's not like there's an absolutely essential social network built
around this tool or anything.

### dynamic indeterminacy

If this were just Git or even just Unix, then I truly wouldn't care. But it's
not just these specific contexts. The issue of when to use pointy tools comes
up all of the time.

A common occurrence is something like a discussion of dynamic versus static
type. Proponents of dynamic type are always eager to point to tests as the
reason why they don't need to know the types of their variables before
runtime. I have a fair bit of enthusiasm for [a particular dynamic
language](http://toromon.com/tag/python.html) , but I really don't get this
point. Type inference is a godsend, but not being able to verify object types
at compile time is just a limitation.

### better blogging

To give one last example of the problems that a preference for pointy tools
can cause, let's look at blogging. The technical setup for this blog is almost
baroque in its complexity. I [started](http://toromon.com/a-first-effort.html)
this blog explicitly with the purpose of focusing on things like
[AWS](http://toromon.com/tag/aws.html),
[Mercurial](http://toromon.com/tag/mercurial.html), and the
[challenges](http://toromon.com/tag/git.html) of efficiently and effectively
discussing the work of software development.

As part of that effort, I mucked about a fair bit with [some neat open source
projects](http://toromon.com/tag/pelican.html) , but I also spent a lot of
time working on the tooling and not working on the content. Part of this is by
design, but part of that is me just missing the point. A blog is meant to be
any easy and cheap way of sharing your thoughts with the world.

My choice of technologies has definitely influence how, when, and how often I
write here. When I recently looked at this critically, I was not convinced
that I was coming out ahead of the numerous alternatives.
[Ghost](https://ghost.org/) looks beautiful. For a more commercial endeavor, I
wouldn't hesitate to throw this blog (and a bunch of other stuff) into
[Squarespace](http://www.squarespace.com/).

For various reasons, I decided to [try blogging on
Medium](https://medium.com/@jeffksmithjr). So far, it's been great. The baked
in analytics are more beautiful than the Google Analytics that I use on this
site and, of course, took no effort from me to setup. The social traffic has
been a nice bonus, without the issues of spam comment moderation from the dark
old days of Wordpress.

But the number one reason that I'm using Medium is that it allows me to just
focus on the important part of the task: composing new, interesting blog
posts. That's all that matters for this particular activity, and Medium does a
great job of stripping away all of the other stuff that can get in the way.

I don't mean this as any sort of criticism of
[Pelican](http://docs.getpelican.com/en/3.2/). It's a great project. It does a
great job of building something that is _along some dimensions_ vastly simpler
than the alternatives. But at the moment, I find myself interested in building
[different sorts of software](https://medium.com/@jeffksmithjr/40bf118a2845)
than little tweaks to my blogging workflow. Even then, though, I'm still
considering posting to this site as well, for the sole reason that code syntax
highlighting is not considered a core feature of most blogging platforms.

### rounder points

Don't get me wrong: I love Unix and the wild, hairy world of thinly-documented
open source software. I just think that we as developers learn intrinsically
hostile tools like vi and then make the mistaken conclusion that everyone
should have to go through the same level of difficulty to get anything of use
done. Emphasizing difficult and dangerous tools just strikes me as deeply
wrong in an age of powerful APIs, trivial but profitable apps, and rapid
iteration. Hell, you can even get [dev null as a service](http://devnull-
as-a-service.com/) these days. Anything is possible!

Now, if you'll excuse me, I need to spend the next four hours explaining to my
Scala compiler why my program is valid.
