---
layout: post
title: "Ruby's double bangs !!"
date: 2012-06-06 20:58
comments: true
categories: [Ruby]
sharing: true
---

Ever seen the use of the bang operator ! like this?

```
def signed_in?
  !!current_user
end
```

and wondered why? After all it looks like it's simply negating the original value and then reversing it again to bring it back to its orignal true false value. So why bother? Why not just write 

```
def signed_in?
  current_user
end
```

The problem with the last snippet is that it doesnt return a true or false value. It returns a User object. And further down the line there may be code that expects only a boolean value of true false.

e.g.

`logged_in = signed_in? #logged_in isnt true or false, its a User object`

whilst Ruby happily converts objects to their boolean value in conditional statments 

`if signed_in?`

You may have written some code that doesn't and assumes it's always dealing strictly with boolean values. False assumptions like that can cause bugs or worse **BOOM!**.

So the best way to prevent this is to ensure methods like the above only ever return true or false - and nothing else. 

So how does !! acomplish that. 

Lets take a look at a string. In ruby a string with a value is considered to have a boolean value of true.

str = "Hello"  ==>  **true**

If we use !str, ruby converts the obj into a boolean value true and **then** negates it to return **false** 

If we use another bang and negate one more time, the boolean value will be negated again and the boolean value **true** will be returned.

So by using two !! bangs we **ensure** we get an object's **boolean value**. 






