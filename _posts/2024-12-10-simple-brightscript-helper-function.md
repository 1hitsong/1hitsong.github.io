---
title: A simple BrightScript helper function
date: 2024-12-10 20:00:00 -0500
categories: [programming]
tags: [roku, brightscript, code]     # TAG names should always be lowercase
# image:
#   src: /assets/img/posts/2024/code.jpg
#   width: 1000   # in pixels
#   height: 400   # in pixels
#   alt: JavaScript Code
---

If there is one thing I've learned from working in code for so long it's that negative conditions in if statements
can easily trip people up. That's why when possible, I try to use positive conditions instead of negative conditions.

Obviously, this doesn't always make sense, but in BrightScript, there is one fundamental condition we can apply
this code style to and it greatly improves code readability.

In BrightScript, you will need to frequently check if a variable is not `invalid`. In most of Roku's documentation
and sample code you'll see this check written as:

```brightscript
if variable <> invalid
    doSomething()
end if
```

This works just fine; however, place several of these checks in a chain or in a function and it can get messy quick!

Here's a simple helper method I made to save a few characters and make the code a little easier to read at a
glimpse.

```brightscript
function isValid(input as dynamic) as boolean
    return input <> invalid
end function
```

It doesn't get much simpler than that. Now instead of using the negative condition to check if something is not
invalid, we can use a positive condition to check if something is valid.

```brightscript
if isValid(variable)
    doSomething()
end if
```
