---
layout: post
title: "Lua Function Basics"
date: 2018-11-12
excerpt: "To show up the basic Lua function syntax"
tags: [Lua, function]
comments: true
---

## Defining Functions
Functions can be defined in the "ordinary" way, and we can call them.
```Lua
function double(x) return x*2 end
return double(1)
```

We can access the function object created simply by using its name without any parentheses. Thus we can pass the function as an argument, store it in a data structure, etc.
```Lua
return double
a = {double}
return double == a[1]
```

so-called lambda expressions or anonymous inline functions can also be created in Lua. They are similar to the "ordinary" functions described above in almost every way.
```Lua
return function(x) return x*2 end
return (function(x) return x*2 end)(1)
```

Note that functions and other variables share the namespace in Lua (and in most other languages), unlike Lisp. In fact, in Lua, a function is just another kind of data you can store in a variable.

## Function Arguments
Function objects can be passed to other functions as arguments. To invoke an argument as a function, just append the parenthesised list that you want to invoke it with. Using the *double* function defined earlier, we can do thins like:
```Lua
function dofunction(f) return f(21) end
return dofunction(double)
```

The  "canonical" example of a function that takes another function as a parameter is *map*. Unfortunately *map* does not come with Lua, so we'll have to code it ourselves.
```Lua
function map(func, array)
local new_array = {}
for i, v in ipairs(array) do
new_array[i] = func(v)
end
return new_array
end

This is a simple `map` implementation that only works with one array. But it workds well:
 
 ```Lua
return table.concat(map(double, {1, 2, 3}), ",")
```

A more complex `map` implementation that works with more than one array is possible:
```Lua
functon mapn(func, ...)
    local new_array = {}
    local i = 1
    local arg_length = table.getn(arg)
    while true do
        local arg_list = map(function(arr) return arr[i] end, arg)
        if table.getn(arg_list) < arg_length then return new_array end
        new_array[i] = func(unpack(arg_list))
        i = i + 1
    end
end
```
