---
layout: post
title:  "As a Tester, I... (pt. 2): Chain Chain Chain"
date:   2016-01-20
categories: testing
---

Here’s the second installment of a three-part series.  If you didn’t read the last one, check out [part one]({{ site.baseurl }}{% link _posts/2016-01-19-as-a-tester-i-pt1.markdown %})

<hr>
<p>This post is where the rubber really starts meeting the road.  It’s a bit longer and more technical, but it lies at the heart of this series of posts.  We’ll be talking about executables: what they are, how they are used, and consequently, how they are tested.</p>

<p>Let’s start by defining what I mean by an &ldquo;executable.&rdquo;  I’m not sure if this covers the full generality of the term, but I’m referring to the following:</p>

<blockquote><i>An executable is an independently runnable piece of code consisting of one or more processes, which is invoked and managed by the operating system.</i></blockquote>

<p>Well, that’s a mouthful.  As usual, it’s just as instructive to see a list of examples:</p>

<ul>
  <li>Some random Java class without a &ldquo;main&rdquo; method: This is not an executable.  While its methods may be executed, it is invoked and managed by the JVM.</li>
  <li>A Java class with a &ldquo;main&rdquo; method: This is an executable, so long as we also assume the proper jarring, manifest file, or command line arguments to &ldquo;java -jar&rdquo;.</li>
  <li>A Python script: This is an executable.  Similar to the example above, it requires some hashbang thingie or running &ldquo;python some_script.py&rdquo;.</li>
  <li>Linux commands like &ldquo;ls&rdquo;, &ldquo;awk&rdquo;, &ldquo;pwd&rdquo;, &ldquo;vi&rdquo;, etc.: These are executables too.</li>
  <li>Bash scripts: These are executables too.</li>
  <li>Standalone programs like Gimp, Excel, Maya, etc.: Again, executables.</li>
</ul>

<p>The most important aspect of this definition is that the interface of an executable is the operating system.  For ingress, you have command line options, config files, etc.  For egress you have standard out, files, a process now listening on a port, etc.  In other words, the interface for an executable is any operation allowed by the OS.</p>

<p>This is fine for a human user.  You run the code (according to documentation of course) and check out the results: reading standard out, opening a file, or clicking on that shiny new window that opened.  But what if your user is not a fleshy human, but another piece of software (like an automated test)?</p>

<p>As any experienced tester will tell you, writing automated tests for an executable is tricky business.  Why?  Because it can do <strong>ANYTHING</strong>.  There are essentially no meaningful guarantees you can make without trying it out first.  Do the results get printed to standard out?  Do they get written to a file?  How many?  Where?  What is the format?  What information will be present?  Do I have to click on some buttons?  You can read the documentation, but I think we all know how helpful that is during active development (heck, you’re lucky if there are docs at all).  As any good tester knows, your tests are the only <strong>real</strong> documentation.</p>

<p>So as a tester, what do you do?  Well, you create <strong>another</strong> executable, one that runs the original executable, and checks the results.  This entails making sure the files that are supposed to be there are actually there (and no others), parsing standard out with regex, automatically clicking on buttons using <a href="http://www.seleniumhq.org/">Selenium</a>, etc.  It can be done.</p>

<p>If this executable really is the end of the line, if our customers will only be fleshy humans, I guess this is good enough.  Sure, it isn’t great for the testers, and we may have to resort to manual testing, but we can manage.</p>

<p>So we have some great executable (or application if you prefer), but now we want to build another one - one that uses the functionality of the first.  This is where it really starts going to hell.</p>

<ol>
  <li>The developers of the new executable have to do the same work that the tester did for setting up automated tests of the first executable.</li>
  <li>The tester has yet another executable to try to test.</li>
  <li>The tester needs to test the shared behavior of the two (integration tests).</li>
</ol>

<p>For #1, the developers want to programmatically use the first executable in their new one, just as the tester wanted to programmatically use it in his/her test.  As such, the same lack of guarantees will plague development of the new executable as much as it plagued the tester.</p>

<p>For #2, tough luck, I guess.</p>

<p>For #3, the tester really has their work cut out for them.  Resource contention alone is enough to cause fits.  Are they trying to read/write the same file?  Are they both printing to standard out, possibly invalidating your fragile regexes?  Are they executing sequentially or in parallel?  Is the second executable accounting for all the possible effects of the first?  What if you run the first one, then the second?  What about the other way?  At this point, the tester just needs to get into the code to figure out how to test the shared behavior of the two executables.</p>

<p>Now, if the number of executables is very small, the system they run on very well-defined, and the development between the executables very well-coordinated, you can make this work.  It won’t be easy, and I would be looking for another job, but it can be done.  Barely.</p>

<p>This is possible if you’re working on a videogame or embedded software (see <a href="http://www.joelonsoftware.com/articles/FiveWorlds.html">this</a>), but if you’re building software to be used by other software (services, platforms, frameworks, etc.), it simply isn’t going to scale to the size and lifespan of the software you need.  I would like to highlight my point in the following unambiguous terms:</p>

<blockquote><i>Composing (e.g. chaining) executables is evil and should be avoided at all costs.</i></blockquote>

<blockquote><strong>Disclaimer</strong>: You might rightfully point out that the GNU/Linux command line utilities are just a bunch of executables, and they work just fine.  That’s true, but do you have any idea how many developer-years have gone into it?  Also, having tens of thousands of user-developers filing bug reports for the last few decades doesn’t hurt either.  Needless to say, this isn’t an option for most software.</blockquote>

<p>So where does this leave us?  As I’ve said before, I like to offer solutions to problems as opposed to just pointing them out.  Patience - we’re getting there.  The next post will have what you want.  Hope to see you there!</p>
