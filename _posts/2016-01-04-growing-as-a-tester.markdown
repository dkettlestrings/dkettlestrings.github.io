---
layout: post
title:  "Growing as a Tester"
date:   2016-01-04
categories: testing
---

This is the first of several blog posts that I'm porting over from my internal blog at work.  I've made minor changes to ensure no trade secrets are exposed (unlikely), but also to target it towards a more general audience.  A little background: in addition to other duties, I am a software tester at work.

<hr>

I’ve been kicking an idea around in my head recently: how can I grow as a tester?  Obviously, just the raw accumulation of experience is helpful, but what about beyond that?  I started looking around for resources, and this journey has revealed some interesting insights into the profession of software testing.

Possible vectors of approach:
* Blogs/ articles
* Books
* Coworkers (fellow testers)

I started by doing what you’d expect -- I Googled it.  Let’s just say that most of the results I found were less than enlightening.  Mostly they were filled with fuzzy exhortations to &ldquo;learn to prioritize&rdquo;, &ldquo;develop communication skills&rdquo;, or commit similar platitudes.  Conspicuous by its superiority is Google’s own <a href="http://googletesting.blogspot.com/">testing blog</a>.  I suggest the &ldquo;Testing on the Toilet&rdquo; series: nice, bite-sized nuggets of digested testing experience (see what I did there?).  But seriously, if you can point me at an actually interesting testing blog, I’ll kiss you.

<p>And Stackoverflow?  There are some decent gems in there, but the emphasis is truly on developers (duh).  There is a <a href="http://sqa.stackexchange.com/">stackexchange for software QA</a>, but as of now, the content seems pretty thin.  Maybe it will just take a few years to build up and be great.  Here’s hoping.</p>

<p> Maybe this is all a bit unfair; there are interesting testing articles out there, but they are comparatively sparse.  &ldquo;Compared to what?&rdquo; you rightfully point out: compared to good software development articles.  Why the discrepancy?  We’ll get back to that later.</p>

<p>Books?  Hah.  I’m not going to buy a book, what are you, crazy?</p>

<p>So what about your coworkers?  Ideally, you learn best by interacting with people better than you at your job: from code-reviews to hallway conversations, the most immediate and relevant learning comes from the masters of the craft, elbow-to-elbow with you in the trenches.</p>

<p>Let’s step aside and look at a seemingly unrelated topic for a moment: Agile Software Development (cue the trumpets).  First off, this article is not about what is and what is not &ldquo;Agile.&rdquo;  Frankly, the ensuing theological arguments bore me.  With that out of the way, here are a few principles usually put forth as suitably agile:</p>

<ul>
  <li>Teams should be as &ldquo;vertical&rdquo; as possible.  That is, a single team should, as much as possible, be responsible for a product from inception through design, implementation, testing, deployment, and finally to customer feedback.</li>
  <li>Teams should be small.  I’ll save you the Googling, but somewhere around 8 seems to be the maximum sanctioned size.</li>
</ul>

<p>As a consequence of these two precepts, in practice most teams have a single tester.  So who is the coworker that I’m supposed to be learning from?  Clearly no one on my team.  My best bet is either to ask a patient developer whose opinions on testing are trustworthy, or seek out a tester on another team.  But which tester?</p>

<p>Software development is, by its nature, a very sociable activity.  Devs are always sharing code, interacting with each other’s services, using frameworks developed elsewhere, and generally having a grand time throwing software at each other.  Not so much for the tester.  Testers may include shared code, call services, and use frameworks, but they rarely ever interact with someone else’s tests.  Tests are a dead-end.</p>

<hr>
<p><strong>Clarification: </strong>Apparently this sounds like I’m saying that testing as a job is a dead-end.  I hope not!  What I mean is that tests/ test results are never consumed in any meaningful way.  If tests pass, the build/deployment proceeds.  If they fail, I (the same person that wrote the tests), look into it and perhaps file a bug.  This warrants another post; it lies at the heart of the difference between testers and developers.</p>
<hr>

<p>As a result, I can list off at least a dozen absolutely top-notch devs at work, but I have only vague notions as to the skills of most of the testers that sit mere feet from me.  It’s weird to think that I can’t answer the question, &ldquo;who are the best testers in your organization?&rdquo;  This lack of visibility doesn’t simply slow professional growth: it encourages laziness, apathy, and stagnation.</p>

<p>So the interaction between testers doesn’t arise naturally in the course of work, but I can still pin down a fellow tester in the hallway, right?  I can (and occasionally do), but even if the other tester happens to know about my problem, and they also happen to know how to solve it, this solution simply doesn’t scale.</p>

<p>So what’s to be done?  I see no way to make tester-tester interaction a natural part of software development.  The options, as I see them are between</p>

<ol>
  <li>Dedicated testing teams</li>
  <li>A Testing Community of Practice</li>
  <li>Apprenticeship</li>
</ol>

<p>#1 is a no-go.  The vertical team structure simply has far too many benefits. Having worked as a tester both within a vertical team as well as on a dedicated testing team, I can say without qualification that testing within a vertical team is far more effective.  Why?  That may be worth a post of its own, but some highlights are that the tests are more relevant, up-to-date, and effective.  Also, removing an external dependency to release is reason enough as far as I’m concerned.</p>

<p>#2 seems promising on the surface.  For those of you not in the know, a Community of Practice is a name for a semi-formal organization of people who do the same job.  You create a horizontal organization where people doing a similar job can gather, share experiences, and hone their craft.  Perhaps it’s implemented as a series of brown bag talks, big monthly meetings, off-site retreats, or whatever.  The idea is that it’s an organization built around people doing the same job, not around a product.</p>

<p>Actually, I really like this idea.  It allows you to keep the efficiencies of a vertical team’s lack of dependencies while incorporating some of the economy of scale inherent in teams of specialists.</p>

<p>Here’s the problem: I have no idea how to actually implement this in practice.  It seems dangerously similar to trying to mandate corporate culture.  In the end, your manager judges you on your contributions to your actual scrum (project) team, not your involvement in some touchy-feely Agiley community of practice.  Maybe I simply lack imagination, or I haven’t read enough about this topic, but to me, this requires proper incentivization of managers to encourage testers to be meaningfully involved and a professional culture amongst testers that values learning, improvement, and passion for the craft.</p>

<p>These are tall orders indeed.</p>

<p>#3, or some similar form, makes the rounds on software development practices.  It’s a time-honored notion, harkening back to at least The Mythical Man Month.  The idea is basically that as a new employee, you are put under the supervision of an ostensibly more experienced and qualified coworker who will help you learn and grow in your job.  This too is a great idea, but one I have rarely seen implemented.  Really, it suffers from the same problems as a community of practice.  You need to change the culture, and there is no realistic means of doing that except from the top down.</p>

<p>So perhaps a community of practice or mentoring/apprenticeship might work, but you’re going to need buy-in from top to bottom to get that kind of a cultural change.  It seems unlikely.  But whenever you seem trapped in a problem like this, I’ve found a good way to get yourself out is to question your assumptions.  In this case, that testing is a dead-end.  What would be the most natural way for testers to interact with each other’s tests?  Obviously, to run them.  But whose tests would I run?  Well, as a part of my job as a tester, whenever my team makes a change that might break customer’s code, I should run their tests!  Well, now that I say it that way, it’s pretty obvious.</p>

<p>The ability for me to build and run the tests of a dependent project using my latest version requires work.  The requirements are pretty much the same as Continuous Integration/Continuous Delivery.  It requires a great many things: using a standard build process, removing implicit dependencies for building and testing, etc.  But the payoff for me as tester would be that I would start interacting with other testers’ code and having dialogues with them concerning what they are testing, how they are testing it, and where gaps are.</p>
