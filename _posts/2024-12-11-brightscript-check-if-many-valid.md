---
title: Check if many things are valid in BrightScript 
date: 2024-12-11 20:00:00 -0500
categories: [programming]
tags: [roku, brightscript, code]     # TAG names should always be lowercase
# image:
#   src: /assets/img/posts/2024/code.jpg
#   width: 1000   # in pixels
#   height: 400   # in pixels
#   alt: JavaScript Code
---

When programming BrightScript, there will certainly come a time when you will need to check if multiple variables
are valid; or if you're not using my [isValid() helper function](https://1hitsong.github.io/posts/brightscript-check-if-valid/), if multiple variables are not `invalid`.

In Roku's documentation and sample code you may see this check written as:

```brightscript
if variable1 <> invalid and variable2 <> invalid and variable3 <> invalid
    doSomething()
end if
```

This works, but we can do better.

What if we use the `isValid()` function?

```brightscript
if isValid(variable1) and isValid(variable2) and isValid(variable3)
    doSomething()
end if
```

That's an improvement, but it's still very verbose. That's why I wrote a helper function to check multiple variables at once.

Simply pass it an array of items, and it will return a bool value indicating whether or not all the variables are valid.

```brightscript
function isAllValid(input as object) as boolean
    for each item in input
        if not isValid(item) then return false
    end for
    return true
end function
```

You'll notice the function returns as early as possible to save any unnecessary  iterations.

This helper method keeps the code short, concise, and clean.

```brightscript
if isAllValid([variable1, variable2, variable3])
    doSomething()
end if
```
