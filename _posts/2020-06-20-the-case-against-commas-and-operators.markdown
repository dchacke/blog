---
layout: post
title: "The Case against Commas and Operators"
date: 2020-06-20
tags:
 - coding
---

![Image for post](/img/0_4LFqAYsRKbb9x8qQ.jpg)

<p style="text-align: center;">
  <small>Photo by <a href="https://unsplash.com/@ffstop?utm_source=medium&utm_medium=referral">Fotis Fotopoulos</a> on <a href="https://unsplash.com/?utm_source=medium&utm_medium=referral">Unsplash</a></small>
</p>

Commas are widespread in programming languages. In JavaScript, for example, commas are used to delineate elements of arrays and maps:

```js
[1, 2, 3, 4]
{foo: "bar", bar: "foo"}
```

They are also used in functions' argument lists:

```js
foo(1, 2, 3, 4)
```

Of course, any interpreter or compiler *could* still read the above code samples unambiguously without commas:

```js
[1 2 3 4]
{foo: "bar" bar: "foo"}
foo(1 2 3 4)
```

A comma-less map may initially lead to some confusion for a human reader trained to look for commas to replicate key-value groupings mentally, but that can easily be remedied by adding a line break:

```js
{foo: "bar"
 bar: "foo"}
```

In any case, here I am concerned with the necessity of commas from the compiler's or interpreter's perspective, and in none of the above cases would either one need commas. In arrays and argument lists, every element is a standalone element, and in maps every key-value *pair* is standalone.

So why are commas so ubiquitous in programming? StackOverflow user Carl Norum [points out](https://stackoverflow.com/a/3488237/1371131) that they originated in mathematics, where they have been used "for centuries." He also claims they eliminate ambiguity in cases such as:

```js
foo(1 - 2)
```

Did the programmer mean to call `foo` with `1` and `-2`, or did he mean to call it with the result of `1 --- 2`, i.e., `-1`?

One commenter, a user by the name of sepp2k, [points out](https://stackoverflow.com/questions/3488229/why-do-programming-languages-use-commas-to-separate-function-parameters#comment3642921_3488237) that one can eliminate the ambiguity by introducing groupings with parentheses:

```js
foo(1 (-2))
```

That works, but it could still be simpler. The interpreter/compiler could have the following heuristic: if the `---` operator is separated from the next element by whitespace, it is meant to subtract --- otherwise, it is meant to negate. With that heuristic, you won't need commas or parentheses.

In any case, the underlying problem leading to the ambiguity in the first place is that `---` is an *operator* and not a function. If `---` were a function, it would simply be another parameter, and writing `foo(1 --- 2)` would mean you are passing *three* arguments: the number `1`, the function `---` , and the number `2`. If you wanted to pass the result of the subtraction, you would instead do:

```js
foo(-(1 2))
```

Operators, like commas, are standard math notation, but that's no reason to prefer them. Besides, functions are standard math notation, too. And unlike operators, functions can be passed around, so you get an additional ability for free. That's not to mention that in existing languages, commas could be *optional*. You could use them the few times you need to eliminate ambiguity and omit them in all other cases, and the interpreter/compiler could have a heuristic to deal with ambiguous cases.

Rich Hickey made a smart choice when he decided to treat commas as whitespace in Clojure. (And when he decided to use semicolons as comment indicators!)

One --- perhaps the only --- legitimate use case I see for commas is that of a thousands separator in numbers: 1,200,000 is easier to read than 1200000. Ruby uses underscores for this: 1_200_000. Meh, better than nothing.

Commas and operators detract from programming languages. Use functions instead to eliminate ambiguity, to get rid of countless commas, and to make operators first-class citizens. I must have typed hundreds of thousands of unnecessary commas by now. Once you write in a language that doesn't have them, you won't look back.

*If you enjoyed this article, *[*follow me on Twitter*](https://twitter.com/dchackethal)* for more content like it.*
