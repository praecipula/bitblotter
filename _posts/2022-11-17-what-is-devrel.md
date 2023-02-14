---
layout: post
title: What is Developer Relations
---

It happens more often than not when introducing myself to someone new - that age-old question, "What do you do?"

Generally I respond that I'm a software engineer and see if they continue to be curious. It's a little white lie, I must admit, but close enough to the truth to give people the right idea without charging off quixotically into tales of educating others, liasising across teams, and interfacing with developers across whole industries. I could talk about this for ages of course, just as anyone passionate about their job likes to do, but I'm also keenly aware that most people don't really want to be taken on a theme park ride through the Journey of Relationships that they can't get off, or at least, they don't generally want to when asking such a simple introductory question.

I'm slightly ashamed to admit that I do this because I assume the volume of content I have is much greater in span than the attention of someone I've known for all of 27 seconds. Perhaps more folks would be interested than I assume, but we've all been there when a simple introduction turns into a TED talk.

{% include captioned_image.html
  alt="Fry meme: not sure if boring or I don't care"
  caption="This is how to lose new friends" 
  attribution="quickmeme.com"%}

So. Software Engineer it is. Close enough.

But sometimes just sometimes, people *are* more interested, and we start to get into the details. What do I **really** do? What frameworks does my team use? What team do I work on? What does a typical day look like?

And then what?

Here's what I talk about.

## Hard problems, soft people, software, and hard deadlines.

As the conversation swings between discussion of the merits of React Native, monetization plans for a startup idea, marketing funnels, Javascript polyfills, sales motions, and database indexing strategies, Developer Advocates[^1] can often hang with most of the topics. Does that mean DevRel is engineering? Does that mean they are salespeople? Are they in marketing? Do they build software for our company?

[^1]: What's the difference between Developer Relations and Developer Advocates? Roughly, Developer Relations is the field and Developer Advocates are the practitioners. You might also hear DevRelians, API Evangelists, etc... but they are all roughly different labels for much of the same types of activities.

Yes, no, sorta.

### What is the problem we're trying to solve here?

I think it's easiest to start with a problem. Let's consider a hypothetical case where you have a product for developers to use, let's call it `LoremIpsumBot` (`LIB`), and you want to maximize the impact that `LIB` has on the industry. Let's also say that `LIB` is a web service with an API, you monetize some part of `LIB`, and are, naturally, incentivized to drive revenue as much as possible.

How do you do this?

This will likely be a multidisciplinary adoption effort for your team and for theirs, naturally, but when the rubber meets the road a critical part of the process will involve their developer team integrating `LoremIpsumBot` into their own product. `LIB` can't add value if nobody uses it, and you really want people to use it, and use it a lot.

So your success involves addressing the needs of the developers on their team.

A crucial element to note is that *this is usually outside of the sales and marketing cycles* for `LIB`. It's often said that engineers are hard to sell to and hard to market to. That's correct, because that concept is a targeting error: **you aren't trying to sell to engineers, you're trying to empower them.** Or, to put it another way, we engineers are natural skeptics and are used to making up our own mind; you can point us to where you want us to look, but no matter what we will generally evaluate your product on its own merits. The best way to sell a car to an engineer is not to polish the car, it's to open the hood.

Engineers are there to solve a problem and we are concerned on how well your solution will work for our needs above all other considerations. Our user interaction with your website starts with "Find in page..." We spend all day working in monospace fonts, not fancy graphics. We don't adopt your solution, we clone its repository.

The best way to engage with engineers? Interact with them as engineers, otherwise known as the "it takes one to know one" strategy. This means we're engineers who don't own parts of the code base, per se, we own how other engineers will interact with the code base.

#### Developer Relations owns the engineering interface of your product.

For the purpose of this discussion I'm going to define the the "interface" of a library or API as:

Interface
: The explicit and implicit contract between the implementer of a tool and the consumer of the tool.

In a reductionist way, if you're used to thinking in code you can start by thinking of it as a function signature or API call, but that's only a start.

Let's take, for example, the basic task of reversing a character string using the C standard library call to compare strings. The function signature for this is:

    int strcmp (const char* s1, const char* s2);

So straight away the contract for this call is that it will take two constant character pointers by value, that is, creating new local pointer variables that point to the same character string addresses as the caller, and it will do so without modifying the characters referenced by those pointers. It will return a signed integer. However, there's so much more to the actual interface of this call - what does it do, what does it not do, what can we *expect* it to do.

The interface is further specified, *in the spec* (not in code), that:

> The strcmp function returns an integer greater than, equal to, or less than zero, accordingly as the string pointed to by s1 is greater than, equal to, or less than the string pointed to by s2.

For all intents and purposes "greater than" is considered as being alphabetically "later" or "longer", i.e. it is positive for `strcmp("b", "a")` and for `strcmp("aa", "a")`). This is not specified in this part of the spec but does fall out of how strings are stored and ordered in memory for most practical purposes, e.g. for the ASCII character set later letters are simply arithmetically greater in value than earlier letters. Note that what humans expect for ordering is not explicitly stated in the spec, they just say "greater than" and "less than". For instance, the printable ASCII character `?` (question mark) is greater than the whitespace `^M` (carriage return). What does that mean? The interface neither knows nor cares, and its silence is deafening in its omission of any mention of garbage-in-garbage-out semantic meaning. If you were to define your character set as something like reverse-ASCII (IICSA?), I believe that's technically allowed in C, even though it's a good way to piss off programmers who use your character set. This function can still gladly give you an answer for IICSA that is, to humans, the reverse of alphabetical ordering--the alphabet song would go, 🎵"ZYXWVUT, SRQPONMLK"🎶...

Also probably every computer everywhere that uses your character set will break because some code somewhere implicitly assumed that nobody would be so insane as to build a character set this way. Still, the implementers of `strcmp` can say with justification, "well, we never said it had to make sense..."

Additionally, it is elsewhere defined in the C spec that character strings will be null-terminated (have a byte value of `\0` at the end). Nothing is said here about what happens if the strings are not null terminated. In fact, there's very little this function can do as specified if this case happens; there's no feedback mechanism to tell the caller that they goofed. Nice implementations could possibly decide that you're nuts if your comparing strings greater than a zillion characters... but how many characters would be too many? And how would it tell you if it figured out that you've gone too far, there's no error reporting mechanism here. Operating systems can build in some mechanisms for this, i.e. setting a global error number that sort of technically breaks the interface with its non-side-effect-free code, and the operating system can see that, say, this function is running off to access protected memory (an OS-level concept) and trigger a segfault / crash, but the interface as defined in c is silent in this case. This brings us to our good friend "undefined behavior": it could crash, or not, it could delete your hard drive, or strap your grandparent in a parachute and toss them out of the window of an airplane. Who knows?

Why this is an interesting case to me is that it's

1. A very basic function of a super common programming language - "just alphabetize these strings",
1. Fully codified in a technical spec to an exacting level of detail and to an intentional level of omissions,
1. Has all sorts of valid questions about what it does in practice,
1. Is theoretically capable of defenestrating your ancestors at 35,000 feet.

So managing a software interface can actually be a pretty significant job that often brings up lots of "How do we say this? *Should* we say this?"-type questions

#### Interface design is expectations management

Principle of least surprise

Embracing the undefined

Lies of omission



Other resources:
https://medium.com/google-developers/the-core-competencies-of-developer-relations-f3e1c04c0f5b#:~:text=They%20need%20to%20be%20excellent,inspiring%2C%20interesting%2C%20and%20entertaining.
