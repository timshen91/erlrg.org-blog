---
layout: post
title: "As a FP Beginner (0)"
date: 2013-02-01 02:14
comments: true
author: Tim Shen
categories: tim Functional
---

FP stands for *Functional Programming*. Recently I've been following the [online course](https://www.coursera.org/course/proglang) Programming Languages by Professor Dan Grossman. This course introduces programming concepts through introducing and analyzing three languages : Standard ML, Racket and Ruby. Most of the features are from functional programming languages, and later we will find how interesting they are.

A month ago I'm still a total "imperative language" guy, being used to C/C++. After learning something of functional programming, however, my first suggestion is "keep extreme humble and forget everything we've learned from C/C++". "Dear child, stop working, go play. Forget every rule".

Now let's talk about Math. There's an interesting "root of computer"(forget Turing Machine!) called [Lambda Calculus](http://en.wikipedia.org/wiki/Lambda\_calculus). That is :  
- *Every object is a function.*  
- *A function takes exact one function as argument, and return one function as return value.*  
- *We can define a function, or apply one function on another.*

To define a function, use `λx.{return value}`. `λ` means that we want define a function. `x` is the name of the argument, so that we can refer to it in the body. The `{return value}` is either an application or another definition, or the argument itself. Someone may say, what if I want to define a function that receives multiple arguments? The answer is obvious: if we want a function eating the argument `a` and `b`, we define a function eating `a`, returning a function that eating `b`, returning the body we want. This is called [currying](http://en.wikipedia.org/wiki/Currying). So this must be a valid function: `λf.λx.f x`. Notice that `f x` means applying `f` on `x`. It's left-associative, so `f a b` means `(f a) b`, rather than `f (a b)`.

The question is, where're numbers? Wait, what is number, say natural number? You might say "Obviously, 0, 1, 2, 3, 4 ...", but that's wired ------ that the definition of the decimal representation of numbers, isn't elegant: why we need ten characters? OK, with binary representation, so need two characters? But why it's exponential, since `(1001)_2 = 1*2^0 + 0*2^1 + 0*2^2 + 1*2^3`? How many rules there are!

In fact, only two rules are needed:  
- *`0` is a natural number.*  
- *Every natural number has exact one successor, say `succ(n)` is the successor of number n, that is also a natural number.*

Be careful, *every object is a function*, so numbers are also functions. So the definition will be:  
- *`0` is an alias, or name,  of some function.*  
- *The next number of `n` is `succ(n)`, or the result of applying `succ` on `n`.*

The thing is, how to choose the functions `0` and `succ`. [Some one](http://en.wikipedia.org/wiki/Alonzo\_Church) says:  
- *Let `λf.λx.x` be `0`*  
- *Let `λn.λf.λx.n f (f x)` be `succ`*  
So:  
- `0 := λf.λx.x`  
- `1 := λf.λx.f x`  
- `2 := λf.λx.f (f x)`  
- ...  
Looks good, because it seems that every number is different. The explanation of this *encoding* is that, "`n` is a function that takes `f` and `x`, then return the result of applying `f` on `x` `n` times".

Now...Where's `+` operator? So `+` is a function that takes two numbers `a` and `b`, returning sum of them. The sum must be a number, so what we return actually is "a function that takes `f` and `x` and apply `f` on `x` `a + b` times". How to do that? Aha, we can first apply `f` on `x` `b` times, then treat the result as a new `x` ------ `x'`, then give it to `a`: `λa.λb.λf.λx.a f (b f x)`.

Now, multiplication? Stop Reading! Take 2 minutes and think about it.
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
Got it? It's easy : "It's a function that takes `a` and `b`, returning a function that takes `f` and `x`. Apply `b` on `f` first, so we get a function that 'apply `f` on something `b` times', then ... what? Yes, apply `a` on it. Now we get a function apply 'apply `f` on something `b` times' a times. That's exact `a * b` times": `λa.λb.λf.λx.a (b f) x`, or `λa.λb.λf.a (b f)`(please tell yourself why they are equivalent).

Notice that, we can construct a number using `* 2` now. The time complexity is O(lgn), which is equivalent to the exponential way.

OK, think about the operator `^`, as in `2 ^ 3 = 8`.

Good night.
