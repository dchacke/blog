---
layout: post
title: "Update on the Discussion Site"
date: 2019-12-13
tags:
 - coding
 - philosophy
---

First, I needed new pages. One to post something new:

![Image for post](/img/1_sAlETxp4NdlwgBZqPupmCg.gif)

And one to see all the posts:

![Image for post](/img/1_wZdNPPKTIXvt-yCwRS-FJw.png)

Pretty standard stuff. But notably, comments can now be made on comments, which then appear as deeply nested threads, each highlighting the passage that has been commented on:

![Image for post](/img/1_aWeFk3hDb6VuYLRkF49wng.png)

So what you're looking at here is the post with the large font in the middle. It is itself a comment on the word "little" in the post above it, highlighted in gray. Highlighted in green are the passages that people have commented on underneath. In this case, someone commented on the phrase "Maybe go with "small" instead?", which turned into a thread with another guy thanking him. The thread is indicated by the gray bar on the left hand side. Additionally, a couple of people made separate comments on the word "cutesy". Those comments are not in a thread because they are not connected by that gray bar.

You can try out that very page here: <https://web.archive.org/web/20191214002835/https://diskussion.herokuapp.com/#/posts/d3c2e998-6e24-45fc-95ea-e3c73fbdfdf0>

Next up, I'll need to implement some navigation, as there is currently no easy way to get back to the home page. And then, the big one: actually persist these posts on a server.
