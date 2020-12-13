---
layout: post
title: "Reduce Need Not Be Hard"
date: 2020-12-13 13:50:10 -0800
tags:
 - programming
---

People sometimes struggle with the `reduce` function. Perhaps one reason is that it's incredibly powerful and versatile and so it isn't always clear why or when one would use it.

What may surprise you is that you already have inexplicit knowledge (cf. David Deutsch's *The Beginning of Infinity* ch. 14) of how to use `reduce`—because you use it all the time, in your head.

Imagine you are hungry but don't know what to eat. You open your pantry and scan various items. You see:

- Rolls
- Noodles
- Chili

What is it, exactly, that happens in your mind as your eyes scan your pantry for something you feel like eating? You start with a preference of "unknown." Then you see rolls and ask yourself: "Do I feel like eating rolls?" Let's say the answer is "no," so you don't update your preference. It's still "unknown." Then you see noodles and think to yourself, "that's the best option I've seen so far!" So you update your preference to "noodles." Lastly, you see "chili" and ask yourself: "Am I more in the mood for chili than noodles?" If the answer is "yes," you update your preference to "chili." If it's "no," you leave your preference as is.

That's all `reduce` does. You have some initial value—in this case, your preference—that's "unknown." Then you start iterating over some options and update the initial value based on some criterion. You do this at every step, comparing each option with the previous value, and what you're left with at the end is the "reduced" value.

Many programming languages have a `reduce` function. In Clojure, the process looks like this:

```clojure
(reduce
  (fn [acc curr]
    (if (do-i-feel-like-eating? curr)
      curr
      acc))
  nil
  ["rolls", "noodles", "chili"])
```

`reduce` iterates over the last argument (the vector of different foods), takes an initial value of `nil` (representing the initially "unknown" preference) and then runs the `do-i-feel-like-eating?` function for each item. Whenever that function returns true, that current item (`curr`) is set as the preference. Whenever it returns true, the previously set preference (`acc`) remains the same. (The details of the `do-i-feel-like-eating?` function need to concern us here, and in reality, it may take both `curr` and `acc` to compare them, but doesn't matter all that much. We're often unclear about why we feel like eating one thing and not another.)

You do this every time you decide what to eat from a given set of foods, or what movies to watch from a given set of movies, etc.

That does *not* mean that human decision making can be reduced (no pun intended) to the simple algorithm above, because humans do much more: they create the `do-i-feel-like-eating?` criterion and the options in the first place, they can interrupt the above algorithm and change the options by removing some or adding new ones and then run the algorithm again—especially if they find that the algorithm returns `nil`, meaning they haven't found anything they like yet—they can decide to focus on another problem altogether, and so on. But once they have (tentatively) settled on a set of options and a criterion, they typically use something like the above algorithm to make a decision.

You knew how `reduce` worked all along. Much of programming is about making what you already know explicit.
