---
layout: post
title: "Discussions Revisited"
date: 2019-12-08 20:35:04 -0700
tags:
 - philosophy
 - coding
---

Today's websites "enabling" discussions are mostly awful.

First, conversations are typically modeled as a linear exchange. You say something, I say something. But that's not how real conversations work. Anything we say can be rich in consequences and merits exploring, which may deserve dedicated attention separate from the rest of the thread. Sometimes, we state several ideas at once, and addressing them one by one in a linear fashion is cumbersome, especially when each idea requires further conversation. So in reality, conversations are like trees. There are some platforms like Reddit and Twitter where you can comment on comments, but it isn't always clear which part of a comment you are responding to, unless you take the trouble to manually copy the original text and quote it --- that is, if you know markdown. And Twitter is generally bad for discussions because it enforces a character limit on each tweet, which makes discussing larger ideas cumbersome if not virtually impossible.

Second, current social networks are built around the concept of *approval*. It incentivizes people to make unargued assertions, since those that are going to agree with a statement are going to agree with it without an explanation for why it is true. But to those who do not already agree with the idea, unargued assertions are invitations to disagree. This is why social networks are polarizing: they are not built to learn, but to agree and disagree. We don't learn from either of those. We learn *through constructive criticism*. As the great philosopher Karl Popper said, “I may be wrong and you may be right, and by an effort, we may get nearer to the truth.”

People worry about fake news and the election coverage for fear of voter manipulation, so they remind us to "check our sources". That does not help, because a false idea does not become true when uttered by someone else, and vice versa. An idea is an *impersonal* thing. It is either true or false, and we can only find out which through conjecture and criticism. But since today's platforms do not provide a good experience and discourage real discussions in favor of agreeing or disagreeing with each other, we have no good place to discuss online.

Learning how to discuss is important because it teaches you *how to think*. When you ponder an idea the same thing happens in your mind as when you discuss it with someone else. Many different ideas come up and collide, and you want to get closer to the truth. Whether this is with yourself or someone else does not really matter.

Medium is a refreshing platform because it encourages people to post longer pieces. And its editing tools are better than what else I've seen online. They still are not really conducive to critical discussions, though.

What are we left with? Believe it or not, it's email. It's the only tool we have that really allows you to do what you want to do. You can quote others, comment precisely on the quotes you want inline, and conversations can carry on in long form in a tree shape. Alas, emails are boring, they are visually nude, they do not provide any tools to make discussions easier, and longer email threads are notoriously hard to maintain and reference. This isn't to mention that oddly enough, commenting is usually done *above* a quote, and unless everyone agrees that this should be avoided because it disrupts the order in which you read naturally, there is no way to enforce this standard.

What is needed is nothing less than a new discussion platform; a new approach which gives you long form posts, great commenting and editing tools, tree shaped conversations, and precise quoting. When you write a piece, people should be able to comment inline on the parts that matter, and you should see which comments you have not addressed yet at a glance. This matters because an idea is true if all its known refutations are false. In other words, the whole thing would roughly mirror how critical discussions work in real life. It could be used to evaluate new ideas. Indeed, way down the road, scientists and philosophers --- or anyone with an idea, really --- can post a conjecture and then ask for criticism. If, at any given time, there is at least one outstanding criticism, the idea is considered refuted, or at least its truth value is "unknown", and it can be marked as such. That way, others know what the current status of an idea is. Over time, such a platform could become a (fallible!) "source" of ideas and their truth status.

I figured it might be fun to work on such a platform. The first snapshot is available here: <https://web.archive.org/web/20191208201736/https://diskussion.herokuapp.com/>

I'll keep working on it for as long as it's fun. Who knows where that will take me. So far, the website only displays a static text; it's only a mockup of what an actual implementation might look like:

![Image for post](/img/1_1unl8-tycrFKsVPBR0HjoA.png)

You can comment on a passage by highlighting it:

![Image for post](/img/1_FQdggJ4IjU1glF7z1RBd1w.png)

The button on the left appears, and you can click it to expand a form:

![Image for post](/img/1_gaASQBjMAF-LeP12e3VRKg.png)

After you submit the comment, the corresponding passage stays highlighted:

![Image for post](/img/1_cPwo_VNXCqKS1Lab7-k5gQ.png)

The idea of highlighting text to comment on it is inspired by the Medium website. But on Medium, highlights are rather limited. For example, you cannot highlight passages across paragraphs. But why not? I'm guessing this is because getting the selected from many different HTML elements can be a bit tricky. On my site, you can select across any HTML elements within the post. You can even select text *around* the comment form, assuming you already have it open, to correct your selection. It won't quote anything you typed into the comment form and it will place the comment form correctly.

When a second comment is made, its corresponding passage can overlap with another passage that has been commented on:

![Image for post](/img/1_efjH-BM3FTX269ZagvzuMg.png)

Note how the green is slightly darker in the middle, around the word "button", indicating that this word is perhaps a bit controversial.

The comments below first indicate their *range* --- the index of the first and last letter of the passage relative to the rest of the text. Then the quote is shown, indicated by a blue bar on the left, followed by the comment itself.

Next up, I'd like to make it so that you can link from a passage to its corresponding comments, so you can always quickly see what people are saying about a particular passage, and vice versa, so that if you're scrolling through the comments, you can see what passage they belong to and the quote does not provide enough context.
