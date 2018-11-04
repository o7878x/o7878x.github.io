---
layout: post
title: "Lua Coroutine Basic"
date: 2018-11-04
excerpt: "To show up the basic Lua coroutine language."
tags: [Lua, coroutine]
comments: true
---

# Coroutine Basics
Lua offers all ites coroutine functions packed in the *coroutine* table. The **create** function creates new coroutines. It has a single statement, a function with the code that the coroutine will run. It returns a vlue of type **thread** , which reprepsents the new coroutine.Quite often, the argument to **create** is anonymous function, like here:

```
co = coroutine.create(function()
print("hi")
end)

print(co) --> thread: 0x8071d98
```

The function *coroutine.resume(re)** stats the execution of a coroutine, changing its state from suspended to running:
```
coroutine.resume(co) --> hi 
```
Until now, coroutines look like nothing more than a complicated way to call functions. The real power of coroutines stems from the **yield** fuynction, whcih allows a runing coroutine to suspend its excetion so that it can be reummsed later. Let us see a simple example:


For those that already know someyhing about coroutines, it is important to clarify some concepts before we go. Lua offers what I call *asynmmetric
 coroutines*. That means that it has a function to suspend the exceution of a coroutine and a different function to resume a suspeded coroutine. Some other language offer *symmetric coroutines*, where there is only one function to ransfer control from any coroutines to another.
 
Some people call asymeytric courtine *semi-coroutines*(because they are not symmetrical*, they are not really co). However, other people use the sam term *semi-coroutine` to denote a restricted implementation of coroutines, where a coroutine can only suspend its exceution when it is not inside any auxiliary function, that is, when it has noe pending calls in its control satakc. In other words, only the main boy o such smie-coroutines can yield. A generator in Python is an example of this meaining of semi-coroutines.

Unlike the difference between symmetric and asymmetic coroutens, the differene between coroutines and generators ( as presented in Python) is a deep one; generators are simply not powerful enough to implememnt several intereseting constructions that we can write with true coroutines. Lua offers true, asymmetric coroutines.  Thos that prefer symmteci corouties can implement them on top of the asymmetci facilitiyes of Lua. It is an easy taks. (Basically, each transfter does a yield followed by a resume.)
