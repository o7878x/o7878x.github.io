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
```
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
```
$ python test.py
My Super Class
This is my awesome class
```

Everything started with a post by Samuele Pedroni to the Python development malling list. In hist post, Samuele showed that the Python 2.2 method resolution order is not monotonic and he proposed to replace it with the C3 method resolution order. Guido agreed with hist his arguments and therefore now Python 2.3 uses C3.

# C3 Linearization Algorithm
Consider a class C in a multiple inheritance hierarchy, with C inheriting from the base classes B1, B2, ..., BN. We want to compute the linerization L[C] of the class C. The rule is the following:

> The linerization of C is the sum of C plus the merge of the linerizations of the parents and the list of the parents.

In symbolic notation:
> L[C(B1...BN)] = C + merge(L[B1]...L[BN], B1...BN)
