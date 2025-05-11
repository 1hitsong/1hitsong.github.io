---
title: Case insensitive string comparison in BrightScript
date: 2025-05-11 12:05:00 -0500
categories: [programming]
tags: [roku, brightscript, code]     # TAG names should always be lowercase
---

String comparisons in BrightScript are case sensitive. Since we programmers know you should never trust data is in the expected format, we need a simple method to compare two strings for equality.

That's why I created this helper function to compare two strings. The function checks to ensure the passed values are in an expected format then compares them using a forced case.

First we use the `isAllValid()` helper function to ensure both passed values are valid. If even 1 is invalid, we exit early by returning false.

We then check the type of both passed values. This function is only for strings, so if a passed value is any other type, we again exit early by returning false. This also prevents a possible exception when we call `LCase()` on the values. Calling `LCase()` on anything other than a string will result in an exception being thrown.

And finally we compare the two passed values while forcing them both to be lower case.

```brightscript
function isStringEqual(input1, input2) as boolean
    if not isAllValid([input1, input2]) then return false
    if LCase(type(input1)) <> "rostring" and LCase(type(input1)) <> "string" then return false
    if LCase(type(input2)) <> "rostring" and LCase(type(input2)) <> "string" then return false

    return LCase(input1) = LCase(input2)
end function
```

And there ya' have it. A simple case insensitive function to test if two strings are equal in BrightScript.
