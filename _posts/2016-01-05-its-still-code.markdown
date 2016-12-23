---
layout: post
title:  "It's Still Code"
date:   2016-01-05
categories: testing
---

This is the second of two blog posts that I'm porting over from my internal blog at work.  I've made minor changes to ensure no trade secrets are exposed (unlikely), but also to target it towards a more general audience.  A little background: in addition to other duties, I am a software tester at work.

<hr>

That’s right: it’s still code.  Automated tests are just code.  Let’s say it another way: as an automated testing person (that’s the title, right?), your job is to **develop software**.  Sure, its goal may be slightly different from what we traditionally define as "development", but in the end we write text files that a computer converts to a sequence of memory reads/writes, CPU instructions, etc.

So here’s a question for you: why aren’t the best practices for writing automated tests **exactly the same** as those for "software development"?  I don’t know, but they clearly aren’t, and I can prove it.  Pick a random developer and ask to take a look at the last project they worked on (if you worked on it too, it doesn’t count).  Now without knowing a blessed thing about what is going on, start opening random files.  I’ll bet you 5-to-1 that it’s **absolutely clear** which ones are written for development and which ones are written for testing (even taking out the assertions).

Sometimes, though, it’s harder to see where this disparity occurs.  Take [Robot Framework](http://robotframework.org/): no developer in their right mind would use that language (yes, it’s a language!) except as an alternative to [Malbolge](https://en.wikipedia.org/wiki/Malbolge) or [Whitespace](https://en.wikipedia.org/wiki/Whitespace_(programming_language)).  Ok, maybe as an alternative to Assembly too.  You code in [TSV files](https://en.wikipedia.org/wiki/Tab-separated_values) (and people complain about the whitespace in Python…).  I can imagine the design meeting now:

Developer1: "Writing a [lexer](https://en.wikipedia.org/wiki/Lexical_analysis) is hard!"

Developer2: "How about we require that you separate all tokens by tabs?"

Product Owner: "What, make them code in TSVs?  Who is going to use that?"

Answer: testers.  Why?  Because apparently automated tests aren’t **_real_** code.  I could go on at some length (and may very well do so in a future post) about how ill-suited Robot is for most testing purposes, but I’ll digress for now.

Instead, let’s take a look at a more reasonable alternative that has some traction around the industry: Cucumber.  If you’re unfamiliar with it, I suggest [checking it out](https://cucumber.io/).  I’ll give a general description here because I think it will help illustrate my point (I’m pulling this directly from the link above).

First, we start by writing the test case in a "high-level" language (English-like):

{% highlight ruby %}
#foo.feature
Given I have entered 50 into the calculator
And I have entered 70 into the calculator
When I press add
Then the result should be 120 on the screen
{% endhighlight %}

The file containing this test case is what we actually execute when we run tests.  Of course, Cucumber doesn’t come pre-loaded with your notions of calculators, add buttons, results, or screens, so we create a way to map this to actual development code using Ruby:

{% highlight ruby %}
#gluecode.rb
Given /I have entered (.*) into the calculator /do |n|
  calculator = Calculator.new
  calculator.push(n.to_i)
end
# More glue code for pressing add and getting results from the screen.
{% endhighlight %}

Now if we run these tests and the developers have done a good job with their Calculator implementation, it passes!  So what did we achieve?

There’s no denying that we wrote a very readable description of the test.  Also, barring any criminal negligence on the part of the maintainers, the English meaning of the test should be true.  Wowsers!  Documentation that is executable and guaranteed to be consistent with the behavior of the software.  Maybe we should all start doing this immediately.

I am, in fact, totally fine with anyone who wants to use this.  Heck, after doing research for this article, there may be some situations where I'll use it myself.  But there is an important point to bear in mind: what you have actually done is added a layer of indirection between the development code and the tests.  In essence, you have wrapped the API of the Calculator into a (hopefully) more human-readable API.  That’s it.  It’s just more code.

It makes me wonder: If this is so great, why don’t we just **develop** code this way instead of only testing it this way?  Seriously, why wouldn’t we?  All you’ve supposedly done is make a better API - easily readable, writable, etc.  If it’s actually a more useful API, just make that the API to begin with.  So why not?  Why wouldn’t your traditional developer want to use this?  We’ll get there in a bit...

According to the [BDD](https://en.wikipedia.org/wiki/Behavior-driven_development) enthusiasts (tangent: why does every slightly different testing philosophy have to have its own acronym?) the big advantage to this "human-friendly" API is that it allows "non-developers" to write and read tests.  These people are supposed to include business analysts and testers.  But this makes me wonder: does it really lower the **coding skills** necessary to write the tests?

This is clearly false if the tester has to write `gluecode.rb`.  All my current tests are just `gluecode.rb` plus some assert statements.  But the common reply is, "No, the developers write `gluecode.rb`, exposing this nice API to the testers who can then just focus on test cases (`foo.feature`)."  I’m all for testers being allowed to focus on test cases (I have a blog post in the works on that), but using this API has a big problem.

It’s a bit tricky to explain, but I’ll do my best.  I think I can best summarize it as being a **very leaky abstraction**.  If you haven’t heard that term before, [read this](http://www.joelonsoftware.com/articles/LeakyAbstractions.html).  Seriously.  Read it.  Joel is a heck of a lot better writer and a heck of a lot smarter than I am, and he really nails the problem of leaky abstractions better than I possibly could (as an aside: read his blogs!  Most of them are old, but the themes are timeless and he’s both fun and educational).  Of course, it’s still up to me to demonstrate that Cucumber gives us a very leaky abstraction.  Here I go!

It’s probably easier to just give an example.  Let’s suppose our tester/business analyst has been given the glue code and decides to write the following tests (this example comes from the fact that I work at a [map company](https://here.com) where we do these kinds of checks)

{% highlight ruby %}
#buildingBuildingOverlap1.feature
Given all the buildings in Winfield, IL
Then no buildings overlap each other
{% endhighlight %}


{% highlight ruby %}
#buildingRoadOverlap1.feature
Given all the buildings in Winfield, IL
And all roads in Winfield, IL
Then no buildings overlap roads
{% endhighlight %}

Great, they pass and everything!  But something happens.  The Winfield, IL data gets corrupted, or the data is no longer legally available to be used outside of the USA (our tests could be running anywhere in the world).  So, they are told to switch to another city.  London it is!  So they start by writing

{% highlight ruby %}
#buildingBuildingOverlap2.feature
Given all the buildings in London, England
Then no buildings overlap each other
{% endhighlight %}

But it breaks.  Careful inspection shows that it’s not the data’s fault.  Of course, we’re supposing that the tester/business analyst doesn’t code, so the problem is handed back to the developers who find that the problem is in `gluecode.rb`.  It loads all the buildings into memory at once!  Well, the developer goes back and reimplements the "all building in city" code (in `gluecode.rb`) to stream the data in a spatially chunked way.  Great, it works!  But now…

{% highlight ruby %}
#buildingRoadOverlap2.feature
Given all the buildings in London, England
And all roads in London, England
Then no buildings overlap roads     
{% endhighlight %}

Uh oh, it breaks.  First, the tester/BA calls the devs and says that they need to give the "all roads in city" code the same chunking treatment.  This is dutifully done, but it still doesn’t work.  Why?  Because the roads and buildings being checked need to be for the same area at the same time, and now we’re in a real pickle.  Needless to say, the "get stuff in city" abstractions let the data access implementation details leak through.

What’s the takeaway here?  You were writing code, and hey, you had to solve coding problems.  Unfortunately, the level of abstraction in the code was so high, that you could almost forget you were trying to **tell a computer how to do things** (also known as programming).  This very high-level, and necessarily leaky, abstraction is why no developer would want to use this API.

I don’t want to make this post much longer, but I want to point out that this realization (that tests are still code) applies more generally.  So next time you find yourself tempted to string together a bunch of Bash scripts, DLLs, regular expressions, and text files in "well-known" locations: ask yourself, would this be OK if I were writing development code?

My manager likes to remind me from time to time that criticism is easy, but without an alternative proposal, it’s not very useful.  So here’s my proposal:

**@Automated Testers:** Think of yourselves as developers who just focus on slightly different problems.  Learn programming like your developer colleagues.  That means knowing and implementing concepts like data structures, algorithms, loose coupling, modularity, etc.  Write your tests in the language the development code is written in.  Do this so that...

**@Traditional Developers:** Review the testing code.  Critique it in the same way you critique any other code going into the project.  It should meet the standards your team has established.  Focus especially on readability, documentation, and maintainability.
