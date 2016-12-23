---
layout: post
title:  "As a Tester, I... (pt. 3): Give Me Objects or Give Me Death"
date:   2016-01-21
categories: testing
---

Here’s the third and final installment of a three-part series.  If you didn’t read the previous posts, check out [part one]({{ site.baseurl }}{% link _posts/2016-01-19-as-a-tester-i-pt1.markdown %}) and
[part two]({{ site.baseurl }}{% link _posts/2016-01-20-as-a-tester-i-pt2.markdown %}).
<hr>
In the last two posts we’ve seen that the tester is the [first user]({{ site.baseurl }}{% link _posts/2016-01-19-as-a-tester-i-pt1.markdown %}) and that [composing/chaining executables is evil]({{ site.baseurl }}{% link _posts/2016-01-20-as-a-tester-i-pt2.markdown %}).  Now it’s time to bring these two ideas together and form a solution.  I think I’m onto something.  Something that has probably been talked about to death, but I’ve never heard of.  It’s probably got a slick acronym too (all good testing terminology is acronyms).

<p>For the purposes of this post, I’m going to use a web service (and in particular a REST service) as my example of an executable.  I’m doing this not because of any particular properties of web services, but rather because I’m familiar with them and they demonstrate my point very well.</p>

<p>The idea I’m going for in this post is that most executables aren’t really executables.  Web services, for example, almost always need to be interacted with programmatically.  If the service is written as an executable, it needs to be launched via interaction with the operating system, probably by writing a script.  Suppose I’m the tester of MyService (in other words, the first user of MyService), and I want to test that a user can put in a bunch of log messages and then query by the latest date.  My code will look something like this:</p>

{% highlight ruby %}
#In test_query_by_latest_date.py
pull down zip file
unzip
overwrite a bunch of fields in myservice.config
run launch.sh
do a jillion one-off checks to see if it’s where I think it is and running ok
PUT log messages
GET latest
do regex magic on the response and check to see if it’s the one it’s supposed to be
tear down
do a jillion more checks to see if it’s actually gone
{% endhighlight %}

and that’s in the nice case where there’s only one config and one entry point (`launch.sh`).  As you know, it’s often a lot more complicated than that.

The problem here is that we are composing executables, so the process is subject to the same difficulties discussed in the last post.  Where do I get the zip file?  Where is `myservice.config`?   What other executables does `launch.sh` require?  How do I programmatically overwrite fields in `myservice.config`? How do I programmatically check whether the service is up and running ok? How can I be sure that I’ve torn the service down completely?  In other words, what are the pre/post-conditions for a valid, healthy MyService?

<p>Compare the Python script above with the example below, where I have a MyService object whose constructor hides deployment and whose client library hides method implementation details (you are writing a Java client for your webservices, right?).</p>

{% highlight java %}
// In MyServiceTest.java
import com.typesafe.config;
// other imports

Config conf = ConfigFactory.load();
MyService service = MyServiceBuilder.withConfiguration(conf).build();
service.start();
MyServiceClient client = service.getClient();
client.putAll(logMessages);
assertEquals(someMessage, client.getLatest());
service.shutdown();
{% endhighlight %}

<p>While executables are hard to reason about in groups, objects are much simpler.  What’s easier to work with, a bunch of executables communicating through the OS throwing strings around and parsing them with regex, or sets of objects, all in the same JVM?  I don’t need to know where a zip file is, just the name of the library, which I use to import a jar using a standard build system.  I don’t need to know where myservice.conf is, it came with the jar and was loaded via ConfigFactory.load().   Any other executables needed to launch the service also came with the jar.  I programmatically overwrite fields in the config via API calls, rather than by parsing strings in a config file.  Checking that the service is up and running ok is the job of the constructor of MyService or the start method on MyService -- either way, it’s not my concern, it would be covered by a separate unit test checking whether those things work properly -- and the same thing goes for checking that the teardown process was effective.</p>

This end-to-end test of myService now operates like a unit test -- we’ve just  elevated the level of abstraction for what a  "unit" is.

<p>Making an entire MyService a &ldquo;unit&rdquo; gives you the same advantages objects always do:  encapsulation, modularity, composability, etc.  We don’t need to know about the dependencies; we can make API calls rather than parse strings; we can rest assured that the start and stop functionality works properly because it’s been unit-tested elsewhere.</p>

<p>(On a side note, I actually think this is a really good design question: why do we use objects at all?  Anyone who uses OO languages should be able to answer this.  If you’re unsure, I suggest reading Bertrand Meyer’s <a href="http://www.amazon.com/Object-Oriented-Software-Construction-CD-ROM-Edition/dp/0136291554">Object-Oriented Software Construction</a>.)</p>

<p>Whatever you may think, here’s my reason for wanting a MyService class:</p>

<blockquote><i>As a tester, I want objects that are at the level of abstraction I am testing.</i></blockquote>

<p>Or simply substitute &ldquo;test&rdquo; with &ldquo;use&rdquo; for an equally valid point.  At the risk of making this post too long, I’m going to do a quick summary contrasting the two approaches:</p>

<ul>
  <li>Instead of knowing where zip files are located, I pull in a library using my standard build system.</li>
  <li>Instead of knowing how to mess with configs, I have a constructor or builder.</li>
  <li>Instead of running a launch script, I have the constructor.</li>
  <li>Instead of doing checks to see if I have a valid service, unit tests on the constructor/builder ensure that if it didn’t blow up, the service is valid.</li>
  <li>Instead of raw REST I have methods.</li>
  <li>Instead of processes dying I have exceptions.</li>
  <li>Instead of worrying about cleaning up after the service, I just call the unit-tested shutdown method.</li>
</ul>

<p>And this is just the tip of the iceberg.  Think of how much easier it will be for future developers to use your code: they can just import a library!  But how is this done?  Actually, it isn’t that hard.  In fact, my example above comes from my experiences with <a href="http://www.splunk.com/">Splunk</a> and <a href="https://www.elastic.co/">Elasticsearch</a>.  Splunk is an executable (boo!), while I can create an Elasticsearch cluster object directly from code (hooray!).  In addition, there are libraries like <a href="http://www.eclipse.org/jetty/">Jetty</a> and <a href="http://spray.io/">Spray</a> that help you design your services this way.</p>

<p>This is the end of my three-part series.  I hope you enjoyed it, and as always, please leave comments if you disagree.  I’m very passionate about this subject and would love to learn what you think!</p>

<p><i>Even more than usual, I have to thank Carrie for helping edit this series of posts and getting me to fully understand what I was thinking.</i></p>
