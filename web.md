```
The World Wide Web (WWW or simply the Web) is an information system that enables content sharing over the Internet through user-friendly ways meant to appeal to users beyond IT specialists and hobbyists.
```
via [Wikipedia: World Wide Web](https://en.wikipedia.org/wiki/World_Wide_Web)

## Introduction
The Web was invented by English computer scientist Tim Berners-Lee in the late 1980s. It was a *significant* innovation in the state-of-the-art and heavily contributed to the wide-spread propagation of computer use in the late 20th century and early 21st century

The primary advantage that the Web offered over the Internet was its **ease of adoption** and **accessibility**. In fact, during its development (which continues today), these properties have consistently been prioritized over others (e.g. network performance). The principles underpinning the original design of the Web also underpin the development of software it serves.

This chapter explores some of the key design decisions that define the Web, explains its basic architecture, and introduces rudamentary concepts of modern Web development (i.e. any software development that involves serving content over the Web).

### Note on Wikipedia, technical terminology, and precision
Wikipedia is a *fantastic* resource for introductions to technical concepts. I've spent dozens if not over a hundred hours reading through Wikipedia articles since I graduated high school.

You should strive to be as precise as possible as you learn and use technical terms. Technical terms have **concrete** meanings. Applying them slightly incorrectly (that is, imprecisely) can lead to misunderstanding and miscommunication.

Ironically, I'm relatively imprecise in this guide. If I were writing this for a technically advanced audience (e.g. a group of professional software engineers specialized in this specific domain), I'd work a lot harder to use terminology precisely so that my own ideas and knowledge gaps were as clear as possible. The reality is that **being more precise intrinsically means communicating more information**. [1] (And for a beginner's guide to the Web, there is such a thing as too much information-- in other words, too much precision.)

You've already learned that fact if you ever studied significant figures in science. The notation `5` communicates less information than the notation `5.0`, even though the two values are mathemtically equal. `5.0` is more precise than `5`.

And just like _appropriate_ precision can improve the clarity of your communication, it can also improve the clarity of your _thinking_. If your brain deeply understands precise definitions for technical terms, you're able to use them to reason precisely. Reasoning with precise terms that represent abstract concepts is faster than reasoning about the abstract concepts themselves. Terms (i.e. names for things) are cognitive short-cuts that allow our brains to abstract (yes, like [abstraction](https://en.wikipedia.org/wiki/Abstraction)) away complexity and simplify our thought processes.

An anesthesiologist might think:
```
"Well, the patient's history of severe aortic stenosis necessitates a lower dose of propofol to maintain hemodynamic stability and avoid precipitating a critical decrease in cardiac output during induction."
```
We can easily observe two properties. First, the anesthesiologist is clearly leveraging their precise knowledge about severe aortic stenosis, propofol, hemodynamics, cardiac output, and induction to do some _high level_ reasoning about an _extraordinarily_ complex system (the human cardiovascular system). Second, the terms being mapped onto concrete meanings allows the anesthesiologist to reason about the _properties_ of abstract ideas. "Ah yes, severe aortic stenosis comes with properties A, B, and C. Propery C may interact with Property D of propofol to create hemodynamic instability which has properties... blah, blah, blah."

(I have no idea if an anesthesiologist would say that. Gemini generated it for me. In fact, that might illustrate my point. Perhaps a _true_ anesthesiologist would recognize some imprecisions in Gemini's statement that indicate a serious lack of medical understanding. Or, Gemini is just a legit anesthesiologist.)

If the terms you use to problem solve are sloppily defined, so will be your solutions. Focus on learning technical terms precisely and deeply understanding the properties of the concepts they name. Clicking on Wikipedia articles and reading at least the first paragraph of new terms is a great way to develop this type of knowledge. At first you'll be overwhelmed. The first paragraph of the page for term X references terms W, Y, and Z that you don't know either. And their pages all link to even more terms you dont know. Just keep chipping away at it, and you'll eventually start clicking on Wikipedia pages where you _do_ know most of the terms in the introductory paragraph. If your understanding of those terms is precise, those moments will be as simple as, "Oh, ok got it."

## Principles of the Web
(Disclaimer: This section is heavily inspired by course content from Noah Mendelsohn's ["Internet-scale Distributed Systems"](https://www.cs.tufts.edu/comp/117/principles). Noah is an [extremely well-credentialed contributor](https://engineering.tufts.edu/cs/people/faculty/noah-mendelsohn) to the World Wide Web. )

### 1. Be built for *everyone*.

Unlike MLB's "World Series", the World Wide Web is true to its name. Tim Berners-Lee recognized that the value of a network grows rapidly [2] as the number of users increases. With that in mind, the Web (and its content) is often engineered to be useful for the maximum number of people.

### 2. Be scalable.

Scalability is a system's ability to increase the number of user's (or operations) it supports without an unacceptable drop off in functionality. There are > 5 billion users of the World Wide Web. In no other software domain is there opportunity to achieve such a large scale. Web- and Internet-focused companies (e.g. Google, AWS) are masters of system scaling.

### 3. Be simple.

A simple system is easier to adopt than a complex one. Simple systems are easier to maintain and diagnose when things break. Simple systems are easier to understand, adapt, and extend.
```
Everything should be as simple as it can be, but not simpler
```
-- [Einstein, maybe](https://quoteinvestigator.com/2011/05/13/einstein-simple/#more-2363).

## Web Architecture
The Web is built on the interactions of two types of players:
- Servers
- Clients

### Servers & URLs
A [server](https://en.wikipedia.org/wiki/Web_server) is, simply put, a computer responsible for *serving* Web content. In reality, the precise definition is more complex, but for the purposes of basic tehcnical discussion, this one is suffciient. Web servers send and receive data over HTTP(S).

The resources a server serves are identified by [uniform resource locators](https://en.wikipedia.org/wiki/URL) (i.e. URLs). A URL's *basic* structure will look familiar:
```
<scheme>://<authority><path>

e.g. 

<scheme> -> https
<authority> -> www.google.com
<path> -> /maps

https://www.google.com/maps
```
In this example, the `scheme` specifies the resource's source and _usually_ (but not always) specifies a protocol over which the resource should be retrieved. For example, `http` and `https` are very common schemes which indicate that the resource is to be retrieved via the [Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/HTTP) (HTTP, or HTTPS when the "secure" variant is used).

The `authority` specifies the _name_ or _location_ of the host computer which can serve the resource. In other words, the `authority` identifies the resource _server_. [3]

Finally, the `path` specifies the exact resource being requested from the server. For example:
```
https://mail.google.com/mail/u/0/#inbox/FMfcgzQXJGmpWBGGLlCsHgmwvScfSgCS
```
links to an email in my inbox identifed by `FMfcgzQXJGmpWBGGLlCsHgmwvScfSgCS`. If, however, I'd like to adjust my Gmail settings, the resource I request looks different:
```
https://mail.google.com/mail/u/1/#settings/general
```
The Web is called a "web" because these URLs acts as "links" in a _web_ of resources. Each resources points to even more resources.

Software the traverses thise web of resources by following links is called a ["web crawler"](https://en.wikipedia.org/wiki/Web_crawler) and are used by, among other things, search engines to "index" resources on the web. The search engine is then responsible for organizing all of these indexed pages based on their apparent relevance to a user's query.

As you might imagine, there are websites which are entirely disconnected from the rest of the "web" (in that nothing links to them) and are unable to be indexed by search engines (how could their web crawlers crawl to these sites?). These components of the Web are referred to as the [deep web](https://en.wikipedia.org/wiki/Deep_web). (The [dark web](https://en.wikipedia.org/wiki/Dark_web) is a _subset_ of the deep web which is _deliberately_ hidden from search engines rather.)

### Clients

A web server's [client](https://en.wikipedia.org/wiki/Client_(computing)) is the computer which is requesting a resource from the server. Clients are _often_, although not always, a personal computer like a laptop or phone. These types of clients are generally running a [web browser](https://en.wikipedia.org/wiki/Web_browser) to request web resources from servers and [render](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work) (i.e. display) the resource to the end user (i.e. a person).

### HTTP(S)

[HTTP](https://en.wikipedia.org/wiki/HTTP) is the communication protocol used by web servers and clients to speak to each other.

TODO(jsnl): Requests + response.

## Footnotes
[1] This is scratching the surface of an _incredibly_ interesting field of mathematics called [information theory](https://en.wikipedia.org/wiki/Information_theory). I did an internship working on data compression algorithms after my sophomore year and had the opportunity to learn a little bit about information theory. One of my biggest regrets from college is that I was never able to take an information theory course. Working in data compression (or some other information-theory-adjacent domain) is a career goal of mine.

The critical concept in information theory (IT, for now) is [entropy](https://en.wikipedia.org/wiki/Entropy_(information_theory)). Entropy represents the _profound_ mathematical reality that information can be _quantified_. If I were to ask you, "how much information is in this guide?", you're likely inclined to respond with something like "a lot", "a good amount", "a little bit", "none at all", etc. (These are all qualitative answers, not quantitative.) I doubt you'd respond "2948374 units of information".

IT is the branch of mathematics that focuses on answering that question _quantitatively_. (Spoiler: to my knowledge, that was a trick question and there is no _single_ correct quantitative answer.). The "unit" of information is measured in bits, a `1` or `0` and, in other words, the answer to a "yes" or "no" question.

Entropy is a reasonably simple, but still too complex concept to cover in a footnote (that is already likely to be too long). But, the general idea that predictable data inherently contains less information that unpredictable data. Reduction to absurdity makes this idea feel a little more understandable.

Suppose you're lost in a new city (without a phone, I guess). There are two strangers that you can ask for directions (i.e. ask for information). You're told that one of the strangers, named Bill, has an odd trait in that he responds to _everything_ simply with "Yes!". He makes no perceivable physical gestures. No blinking. No eye movements. Nothing, but "Yes!". The other stranger, Tom, has a similar condition as Bill, except Tom can honestly respond with "Yes!" _or_ "No!". Which stranger will be able to share more information with you _in as single response_?

Probably Tom because at least Tom's responses are _somewhat_ unpredictable. Granted, Tom won't be sharing information as quickly as a more typical person whose response is _even more_ unpredictable. But regardless, Tom is fundamentally usesful because each response is unpredictable. Tom's responses have more entropy than Bill's.

And importantly, you'll note that in order for this contrived scenario to make sense, I had to deliberately constrain the _other ways_ in which Bill might have been able to behave unpredictably, thus increasing the entropy of his responses, and thus the potential to share more information in each response. If Bill could only say "Yes!", but he could point, blink, shrug, make facial expressions of confusion or understanding, show thumbs up or down, and so on, he'd almost certainly be more useful than Tom.

Developing a basic intuition for entropy and other basic concepts from information theory has been valuable in my career so far even though I don't work _directly_ in that domain. For example, we recently had a machine learning model that exhibited an odd behavior. The model, `M`, accepted 4 types of input data `A`, `B`, `C`, and `D` to produce an output result `Y`.
```
M(A, B, C, D) = Y
```
When the model was fed data of types `A`, `B`, and `C`, it _performed identically_ as when it was run on all 4 input types. Data of type `D` had absolutely no impact on the model's outputs. What does this tell us?

Well, it concretely means that the model "learned" to not weigh `D` data. Theoretically, it suggests that the model learned that `D` data provides **no relevant information** for solving the problem it was tasked to solve. 

It's a difficult decision to say whether we should believe the model. On one hand, the evidence available to us clearly suggests that `D` is void of relevant information. On the other hand, perhaps the model itself wasn't _large_ enough to capture subtle traits in the `D` data that are in fact useful for solving the problem at hand (in other words, the model may not have enough **precision**) or it was trained in an inappropriate way.

In either case, the answer is rooted in information theory. Recognizing that a signal can simply be entirely void of relevant information is reasonably abstract. For a concrete example, the stars and their positions in the sky is a sizeable chunk of data, but not many people would seriously argue that this data contains information relevant to the future performance of the stock market ([astrologists](https://en.wikipedia.org/wiki/Astrology) beg to differ). In theory, it could hold a _tiny_ amount predictive power. For example, maybe a handful of traders are ever-so-slightly inspired by the Orion constellation when its visible in their region and tend to buy more during those periods than others. But I doubt that's significant. 

Similarly, recognizing that while it is _feasible_ for a machine learning model to learn how to predict future performance of the stock market based on economonic signals, trades, geopolitics, climate change, and so on, it may be _infeasible_ for us to train a model large enough to _represent_ all of the mind-bogglingly complex relationships between these types of data.

[2] It's posited that it grows quadratically, not just "rapidly". See [Metcalfe's Law](https://en.wikipedia.org/wiki/Metcalfe's_law).

[3] This is an oversimplification. For example, www.amazon.com doesn't map to a single web server. See [load balancing](https://en.wikipedia.org/wiki/Load_balancing_(computing)).