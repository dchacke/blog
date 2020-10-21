---
layout: post
title: "Neat Clojure Function"
date: 2019-12-08
tags:
 - coding
---

Yesterday, I learned about the Clojure core function [`merge-with`](https://clojuredocs.org/clojure.core/merge-with). Imagine you keep an inventory of two stores:

```clojure
(def inventory-1 {:cornflakes 3 :chunky-soup 2 :nutella 2})
(def inventory-2 {:cornflakes 1 :chunky-soup 4 :milk 2})
```

Say you want to find out the total number of each item. In this case, a map saying that you have 4 boxes of cornflakes left, 6 chunky soups, 2 jars of Nutella, and 2 cartons of milk. How could you go about this? You can't just merge them or the second map's items will just override those it shares with the first one's:

```clojure
(merge inventory-1 inventory-2)
> {:cornflakes 1 :chunky-soup 4 :nutella 2 :milk 2}
```

This says you have, say, only 4 chunky soups total, when in reality you have 6.

Try `merge-with` instead:

```clojure
(merge-with + inventory-1 inventory-2)
> {:cornflakes 4 :chunky-soup 6 :nutella 2 :milk 2}
```

What's going on here? It basically iterates over the tuples in each map and constructs a new map that will have both maps' keys. Whenever the given maps share a key, it passes both corresponding values to the given function (in this case `+`); otherwise, it just adds the remaining key and value to the result without invoking the given function.

In this particular case, it sees that `:cornflakes` occurs in both maps, once with value `3`, and once with value `1`, so the result will have an entry of `:cornflakes (+ 3 1)` . It also sees that `:nutella` only occurs in the first map, so an entry of `:nutella 2` is added to the result. And so on.

This works for any number of maps:

```clojure
(merge-with + {:a 1} {:a 2} {:b 1})
> {:a 3 :b 1}
```

Of course, it works for any function, not just `+`. What function you pass it is up to you. You may get creative; say you have a bunch of vectors of numbers in each key, and you want to `concat` them:

```clojure
(merge-with concat {:a [1 2 3]} {:a [4]} {:b [1 5]})
> {:a (1 2 3 4) :b [1 5]}
```

(Note that while the value of `:a` value turned into a list (the result of `concat`, `:b`'s stayed a vector because concat was not invoked with it since no other map had `:b` for a key.)

Or perhaps you can add a bunch of integers up that are hidden within vectors behind keys? You sure can:

```clojure
(merge-with (comp #(apply + %) concat)
  {:a [4 2 1]} {:a [7] :b [3]} {:b [3 2]})
> {:a 14 :b 8}
```

As you can see, `merge-with` is powerful. Neato, huh fellas?

PS: Guess how often I miss OOP when writing Clojure.

*If you enjoyed this article, *[*follow me on Twitter*](https://twitter.com/dchackethal)* for more content like it.*
