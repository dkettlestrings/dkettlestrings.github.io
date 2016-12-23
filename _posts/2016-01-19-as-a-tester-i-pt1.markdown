---
layout: post
title:  "As a Tester, I... (pt. 1): The First User"
date:   2016-01-19
categories: testing
---

<p><i>I am working on a really big idea, but with Carrie’s help, we decided it was simply too much for a single post.  So here is part 1 of what should be at least a 3-part series.</i></p>
<hr>
<p>&ldquo;The tester is the first user.&rdquo;  It seems like an innocuous enough statement - the tester is the first person to fire up your new application, use your new library, etc.  Perhaps you’ve never heard it phrased in quite this way, but I’m sure you see the obviousness of it.  But what are the implications of this simple idea?</p>

<p>First, let’s think about why we employ testers at all.  It’s simple: you want to pay a user to help you address all of the issues before you turn it over to users that PAY YOU.  So a tester is just a proxy for a paying customer.  That sounds an awful lot like a Product Owner…</p>

<p>The implication is clear: in order for a tester to be successful, they must serve two purposes:</p>
<ul>
  <li>be a reasonable proxy for a paying customer</li>
  <li>be technically savvy enough to help the developers address any issues they find</li>
</ul>

<p>So wait, how am I not describing a PO?  The way I see it, there are some subtle differences.  The tester represents an actual technical user of your software, while the PO represents the customer of your software.  Perhaps an example would help.</p>

<p>Suppose your team developed <a href="http://www.autodesk.com/products/maya/overview-dts?s_tnt=69290:1:0">Maya</a> (a 3D modeling tool).  The PO would represent a videogame company like EA.  They are looking to switch modeling tools, but it has to have features A, B, C, etc. where A, B, and C are high-level and possibly ambiguous.  It might have to &ldquo;work in the cloud&rdquo; or interact with an existing toolchain.  On the other hand, the tester represents the actual 3D modeler at EA who has to actually <strong>use</strong> the tool.  The tester is making sure that the tool is actually usable and does what it claims.  In this example, you can see that while the roles are similar, the difference between the two is clear.</p>

<p>Let’s try another example: suppose your team is writing a library, a web service, or a database.  In other words, your team is writing software that is intended to be used by other developers.  By the reasoning above, your tester should be representing a developer using your software.  As such, they should be building tiny reference applications (tests) that demonstrate the behavior of the software.  While the PO might still have to concern themselves with fuzzy high-level requirements, since the product is designed for developers, it is very likely that many of the requirements are quite technical.</p>

<p>In this situation, it becomes almost impossible to tell the difference between the tester and the PO.  How would the PO know that the customer requirements are met?  By using the product, of course.  But all of the use cases involve writing code (the end users are developers).  There is still a difference between tester and PO, but mostly it revolves around who goes to the boring meetings and presents PowerPoint slides.  I think this is why I enjoyed my time as a dual-threat &ldquo;PO/tester&rdquo; so much: it just seemed like a natural fit.</p>

<p>Enough of the similarities and differences between POs and testers.  I just wanted to clarify (or perhaps confuse) the relationship between users, testers, and POs.</p>

<p>So we agree that the tester serves as a proxy for the actual users of your product.  If the users are interacting with your software manually, then manual testing is probably the way to go (although any automation you can write is helpful).  If the users are writing code against your software, then automated testing is necessary.</p>

<p>But in either case, the tester gets to use it first, and they <strong>must</strong> understand how the paying customers use it and test accordingly.  Here’s the big takeaway from this entire line of reasoning:</p>

<blockquote><i>If your code is hard to test, then it is hard to use.</i></blockquote>

<p>That’s right, if writing tests takes a long time and is difficult to get stable, then guess what the end users experience?  Actually, we can derive yet a further consequence:</p>

<blockquote><i>As a tester, I know best how usable your software is.</i></blockquote>

<p>This puts a lot more power and responsibility in the hands of a tester.  If the tester says, &ldquo;This code is a real pain to work with,&rdquo; then that should be a huge red flag to the PO and the rest of the team.  Maybe it’s time to stop adding new features and make sure what you’re writing is actually good, because if your tester doesn’t like it, the users won’t either.</p>
