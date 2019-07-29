---
layout: post
title: "Python Method Resolution Order Algorithm"
date: 2019-07-29
excerpt: "To show up the Python MRO algorithm."
comments: true
---

# Algorithm Background
Imagine you were implementing a programming language that featured inheritance. When you first approach this topic you decide: a child class will have all of the functions and attributes that it's parent classes should have!

Now this may work for the vast majority of scenarios but what would happen if two parent classes both implemented the same function or attribute?How do you decide what function or attribute takes precedence?

> This is known as the diamond problem. Some languages such as Scala, use an algorithm called **right-first depth-first search** to solve this. Python 3 uses the C3 lineration algorithm.

Example:
```python
#coding: utf-8
#saved as test.py

class awesome_class(object):
    def __init__(self):
        print("My Awesome Class")

    def test_func(self):
        print("This is my awesome class")

class not_so_awesome_class(object):
    def __init__(self):
        print("My Not So Awesome Class")

    def test_func(self):
        print("This is my not so awesome class")

class my_super_class(awesome_class, not_so_awesome_class):
    def __init__(self):
        print("My Super Class")

if __name__ == "__main__":
    my_class = my_super_class()
    my_class.test_func()
```

Output:
```bash
$ python test.py
My Super Class
This is my awesome class
```

Everything started with a post by Samuele Pedroni to the Python development malling list. In hist post, Samuele showed that the Python 2.2 method resolution order is not monotonic and he proposed to replace it with the C3 method resolution order. Guido agreed with hist his arguments and therefore now Python 2.3 uses C3.

# Predefined Symbols
Let me introduce a few simple notations which will be useful for the following discussion. I will use the shortcut notation
> C1 C2 ... CN
to indicate the list of classes [C1, C2, ... CN].

The **head** of the list is its first element:
> head = C1

whereas the **tail** is the rest of the list:
> tail = C2 ... CN

I shall also use the notation
> C + (C1 C2 ... CN) = C C1 C2 ... CN

to denote the sum of the lists [C] + [C1, C2, ... CN].

# C3 Linearization Algorithm
Consider a class C in a multiple inheritance hierarchy, with C inheriting from the base classes B1, B2, ..., BN. We want to compute the linerization L[C] of the class C. The rule is the following:

> The linerization of C is the sum of C plus the merge of the linerizations of the parents and the list of the parents.

In symbolic notation:
> L[C(B1...BN)] = C + merge(L[B1]...L[BN], B1...BN)

In particular, if C is the **object** class, which has no parents, the linearazation is trivial:
> L[object] = object

In general one has to compute the merge according to the following prescription:
> Take the head of the first list; if this head is not in the tail of any of the other lists, then add it to the linearization of C and remove it from ths lists in the merge, otherwise look at the head of the next list and take it, if it is a good head. Then repeat the operation until all the class are removed or it is impossible to find good heads. In this case, it is impossible to construct the merge, Python 2.3 will refuse to creat the class C and will raise an exception.

This prescription ensures that the merge opeation *preserves* the ordering, if the ordering can be preserved. On the order hand, if the order cannot be preserved, the merge cannot be computed.

The **C3** algorithm does the followin:
- It guarantees that base class declaration is preserved
- It guarantees that subclasses appear before base classes
- It guarantees that for every class in a graph of all inherited classes, they adhere to the previous two points

# References
1. [Official Python C3 Algorithm](https://www.python.org/download/releases/2.3/mro/)
2. [Python Method Resolution Order Tutorial](https://tutorialedge.net/python/python-method-resolution-order-tutorial/)
