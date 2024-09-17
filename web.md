```
The World Wide Web (WWW or simply the Web) is an information system that enables content sharing over the Internet through user-friendly ways meant to appeal to users beyond IT specialists and hobbyists.
```
via [Wikipedia: World Wide Web](https://en.wikipedia.org/wiki/World_Wide_Web)

## Introduction
The Web was invented by English computer scientist Tim Berners-Lee in the late 1980s. It was a *significant* innovation in the state-of-the-art and heavily contributed to the wide-spread propagation of computer use in the late 20th century and early 21st century

The primary advantage that the Web offered over the Internet was its **ease of adoption** and **accessibility**. In fact, during its development (which continues today), these properties have consistently been prioritized over others (e.g. network performance). The principles underpinning the original design of the Web also underpin the development of software it serves.

This chapter explores some of the key design decisions that define the Web, explains its basic architecture, and introduces rudamentary concepts of modern Web development (i.e. any software development that involves serving content over the Web).

## Principles of the Web
(Disclaimer: This section is heavily inspired by course content from Noah Mendelsohn's ["Internet-scale Distributed Systems"](https://www.cs.tufts.edu/comp/117/principles). Noah is an [extremely well-credentialed contributor](https://engineering.tufts.edu/cs/people/faculty/noah-mendelsohn) to the World Wide Web. )

### 1. Be built for *everyone*.

Unlike MLB's "World Series", the World Wide Web is true to its name. Tim Berners-Lee recognized that the value of a network grows rapidly [1] as the number of users increases. With that in mind, the Web (and its content) is often engineered to be useful for the maximum number of people.

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

The `authority` specifies the _name_ or _location_ of the host computer which can serve the resource. In other words, the `authority` identifies the resource _server_. [2]

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
[1] It's posited that it grows quadratically, not just "rapidly". See [Metcalfe's Law](https://en.wikipedia.org/wiki/Metcalfe's_law).

[2] This is an oversimplification. For example, www.amazon.com doesn't map to a single web server. See [load balancing](https://en.wikipedia.org/wiki/Load_balancing_(computing)).