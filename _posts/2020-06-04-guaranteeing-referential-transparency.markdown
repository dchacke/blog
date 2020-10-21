---
layout: post
title: "Guaranteeing Referential Transparency"
date: 2020-06-04
tags:
 - coding
---

![Glasses](/img/1_2RdfimeWaFU2lsGSgWVViw.jpg)

<p style="text-align: center;">
  <small>Photo by <a href="https://unsplash.com/@budhelisson?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Bud Helisson</a> on <a href="https://unsplash.com/s/photos/transparency?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a></small>
</p>

The other day, I saw a video on [Brian Will’s YouTube channel](https://www.youtube.com/user/briantwill) — I’m afraid I don’t remember which video it was — in which he mentioned how cool it would be if a programming language offered a special kind of function that can only access the parameters it was given and nothing else. The function would then be referentially transparent and, therefore, truly modular: you could cut it out of any arbitrary code and paste it into any arbitrary code and it would still work.

His idea came at a good time. For the past few days, I have been dabbling with creating a new programming language. My main motivation is just to learn how to write a transpiler, but I also want to build a language that makes learning functional concepts easier for JavaScript developers. Ideally, the language’s syntax will look very similar to that of JavaScript while applying functional concepts we know and love from Clojure.

I think Brian’s idea could be implemented relatively easily. The transpiler could check the generated abstract syntax tree for any symbols within the body of a function that are not part of that function’s argument list.

Having such functions seems to me a great step toward guaranteeing referential transparency. Alas, it’s not itself a complete guarantee yet, because you could still pass an impure function *g* that then gets invoked by your newly declared function *f*. If *f*’s return value changes depending on *g*’s return value, *f* is not referentially transparent.

To solve this problem, you may choose to have the transpiler throw an exception whenever a function you declare to be referentially transparent takes referentially intransparent functions as arguments.

EDIT: This feature is now implemented as part of the [Berlin programming language](http://berlinlang.org/).
