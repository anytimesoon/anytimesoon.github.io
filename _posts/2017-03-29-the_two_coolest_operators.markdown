---
layout: post
title:  "The two coolest operators"
date:   2017-03-29 14:58:23 +0000
---


The other day, I had the geekiest thought I've ever had. I have favourite operators in Ruby. Two operators that are so concise and elegant, that it makes me happy to find an opportunity to write it. I'm talking about `!!` and `||=`.

# Let's start with `!!`#

Every object in Ruby has a truthy or falsy value. In fact, the only two values that are falsy `false` itself and `nil`. Everthing else in Ruby is truthy. So how do we get them to return these values? Take the following values:

```
1                 #=> 1
"Hello World"     #=> "Hello World"
true              #=> true
false             #=> false
nil               #=> nil
```

As you can see, only `true` and `false` return truthy or falsy values. This is where the double bang comes in. A single bang would return the following:

```
!1                 #=> false
!"Hello World"     #=> false
!true              #=> false
!false             #=> true
!nil               #=> true
```

So we have transformed the return value from what it would normally be into a boolean. The only problem is that it is the opposite of what it should be. This issue is resolved by putting a second bang in front. The wrong return value is then corrected to become what it should be:

```
!!1                 #=> true
!!"Hello World"     #=> true
!!true              #=> true
!!false             #=> false
!!nil               #=> false
```

# Moving on to `||=` #
This one is slightly more complex, which makes it just that bit more elegant. We don't always know when a method in our program might get called. We don't know if a variable will already have been set, and this is when `||=` has its moment in the sun. If ever there is a possibility that a variable could be `nil` before we try to call methods on it, we need to make sure it has a value, but if it already has a value, we don't want to change it. We could do something like this:

```
x = "hello world"

if x == nil
  x = "hello world"
end
```

There is nothing wrong with the above code, but there is a way of achieving the same thing in a single line.

`x ||= "hello world"`

This says that if `x == nil` then set its value to "hello world", otherise leave it be.
