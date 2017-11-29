---
layout: post
title:  "It's Our Fault"
date:   2017-11-28
categories: morality
---

So here we are.  We've got [Congressional hearings about election tampering](https://techcrunch.com/2017/10/31/senate-judiciary-russia-hearing-facebook-google-twitter/), net neutrality is [all but dead](https://www.snopes.com/2017/11/28/activists-prepare-to-rally-to-save-net-neutrality/), and your personal data is [routinely grabbed by websites and sold without your knowledge](https://www.neustadt.fr/essays/against-a-user-hostile-web/).  Not only that, but a brief visit to [Hacker News](https://news.ycombinator.com/) will flood you with doom and gloom opinion pieces about how the web is being killed by Google/Facebook gobbling up all of the traffic and gatekeeping content.  Heck even the [W3C](https://www.w3.org/) is [endorsing Digital Rights Management](https://www.eff.org/deeplinks/2017/10/drms-dead-canary-how-we-just-lost-web-what-we-learned-it-and-what-we-need-do-next).  Oh yeah, and ISPs are trying to turn the internet into a series of tiered packages of content bundles.  "Here's your Google/Facebook package for $49.99/month.  If you want Wikipedia too that'll be an extra $7.50/month."  And let's not even get started on what [some governments are up to](http://www.wired.co.uk/article/chinese-government-social-credit-score-privacy-invasion).

I could go on and on, but the point is that there is something fishy going on in the tech industry.  Like I said, you don't have to look hard to be a little alarmed or disheartened by the "progress" we've made over the last 20 years.

Think I'm just another old-timer whining about the good-old days? Nope, I've only been in tech for 6 years. Think it's corporate greed or just the natural progression of the industry? Well, here's the thing: **we write the code**. In the end, every shady data grab, every hidden sale of personal information, every wall that's placed between the public and information is code written by a developer.  That means us.  **We did this**.

Google isn't gobbling up and monetizing your personal data, Facebook isn't killing the idea of a website -- we are.

Certain professions have a code of conduct: doctors take the Hippocratic oath, lawyers are governed by the Bar.  One thing these professions share, and the reason they need these ethics, is that both the opportunities for and consequences of misuse are so high.  I would say it's self-evident that software development is now in a similar position.  Do I think that we *need* a formal body like that for programming?  That's a topic for a different post, but I'm inclined to say no: this post has much more modest goals.  How about this: if you don't approve of the product you're working on or your company's business model, work someplace else.  You don't have to change the world, but if you have moral objections to what you're working on, quit.  What's more important, your conscience or your company? There are tons of companies that provide positive value to society and still pay well.  Unemployment in our field is low, and should remain low for many years. You have the option to work someplace better, so why not take it?

We developers live in exciting times.  The technology is cool.  The problems are difficult.  The solutions are novel.  You have the opportunity to be the first person to do this thing you're working on.  As an industry we have been captivated by what we **can** do, and as people have lost sight of what we **should** do.

So one thing we can do is change the ethics of how and what we code; but there's another opportunity: we can educate.  Just as medicine and law are too complex for those who don't spend their careers pursuing them, so is technology.  And just as doctors and lawyers are expected to be ambassadors of their fields, giving advice, dispelling myths, and championing causes, so should we.

You probably have a decent idea of what Facebook is doing with your data, but your neighbor might not.  Does your brother know that the YouTube videos his children are watching are procedurally-generated to be similar to other popular videos, whether they are [age-appropriate or not](https://medium.com/@jamesbridle/something-is-wrong-on-the-internet-c39c471271d2)?  Does your mom know how much of her browsing history her favorite news site is selling to third parties?

Getting a bunch of programmers to agree on a specific set of ethical rules sounds like a fruitless proposition to me.  Just think of trying to pass a set of coding best practices and multiply the effort by a billion.  I'm not going to try to convince you that what follows is complete, universally true, or always applicable.  My goal is just to motivate you to establish your own ethics and apply them to your work.  Here's a set of questions I think we should be asking ourselves:

* If you are selling your software for cash, do you also monetize the users?  Examples: ads, selling data, etc.

* Is your software limiting a user's freedom?  Examples: limiting their freedom to express their opinions, use other software they might want, be anonymous, access information, etc.

* Are your users giving [**informed consent**](https://en.wikipedia.org/wiki/Informed_consent) to what you are doing?  This is a post in and of itself, but in short, do your users really understand the consequences of using your software?  Does your code do things like track them even when the application isn't open and visible to them?

* When designing your product, is the biggest concern the amount of time/interaction a user has with the software or is it what value the user will gain from it?  Are you thinking of a user as a means or an end?

* Similar to above, what value are users getting from your software?  Does it save them time or money?  Does it help them do their job better?  Are they learning something?  Are they having fun?

* Are your security policies commensurate with the type and amount of personal data you store?

While it may be difficult for all of us to agree on specifics, I believe that most of us can agree on broad themes.  Mull them over, tweak them, invent your own, I don't much care at this point.

Before I finish, I'd like to add just one more small point.  Try not to think in terms of what is simply legal, or what "isn't so bad", but rather try to think of this in terms of what is actually good.  You don't have to save the world, but ask yourself, when you get that big `git blame` in the sky what would your diff look like?
