---
title: Check if a nested chain of objects is valid
date: 2024-12-12 17:00:00 -0500
categories: [programming]
tags: [roku, brightscript, code]     # TAG names should always be lowercase
# image:
#   src: /assets/img/posts/2024/code.jpg
#   width: 1000   # in pixels
#   height: 400   # in pixels
#   alt: JavaScript Code
---

A core variable type in BrightScript is the associative array. These arrays allow objects to be accessed using
keys. The access methods I've seen used most often are dots or brackets.

Here's an example using dots to access a deeply nested associative array.

```brightscript
movie = { 
    data: {
        overview: {
            slug: "Just When You Thought It Was Safe To Go Back In The Water"
        }
    }
}

print movie.data.overview.slug
```

And here's an example using brackets.

```brightscript
movie = { 
    data: {
        overview: {
            slug: "Just When You Thought It Was Safe To Go Back In The Water"
        }
    }
}

print movie.data.overview["slug"]
```

Often times you'll see the bracket method used when the key's value comes from a variable.

```brightscript
movie = { 
    data: {
        overview: {
            slug: "Just When You Thought It Was Safe To Go Back In The Water"
        }
    }
}

keyToLookup = "slug"
print movie.data.overview[keyToLookup]
```

These methods will work as long as your data is 100% as expected and offers no surprises.

Which we programmers know is how data always is...

😂😆🤣 Just kidding, data is always a mess and should **never** be trusted!

Let's look back at our dot example above.

What happens if our data doesn't have an overview object?

![Exception has occurred. Dot Operator attempted with invalid BrightScript Component or interface reference.](/assets/img/posts/2024/dotException.png)

Yikes! The last thing we want is our channel to crash because our data is in an unexpected format.

That means we should check every key in the object chain - all the way down to the data we need.

One way to do this is nested if statements.

```brightscript
movie = { 
    data: {
        overview: {
            slug: "Just When You Thought It Was Safe To Go Back In The Water"
        }
    }
}

if isValid(movie)
    if isValid(movie.data)
        if isValid(movie.data.overview)
            if isValid(movie.data.overview.slug)
                print movie.data.overview.slug
            end if
        end if
    end if
end if
```

Isn't that so pretty that you want it all over your code! 🤢

Now, you may be asking "Why not simply use BrightScript's built in [optional chaining](https://developer.roku.com/en-gb/docs/references/brightscript/language/expressions-variables-types.md#optional-chaining-operators) support?"

Again, in a perfect world where we can trust the data, that would work, but we don't want to use it because optional chaining only
checks if the item in the chain is valid, it does not also check if the item is an associative array. This can lead to exceptions being throw.

In the example above, what if in the returned data overview was a string? It could lead to several types of errors depending on your code.

Technically the overview object _is_ valid, but it's not an associative array, it's a string. So the client throws a syntax error because we're
attempting to access a property value as if it were.

![Exception has occurred. Syntax Error.](/assets/img/posts/2024/syntaxError.png)

That's why I created a helper function that will step through the object chain checking if each key
is valid and will return false as soon as it hits an `invalid` item.

Note: This function uses the [isValid() helper function](https://1hitsong.github.io/posts/brightscript-check-if-valid/)

```brightscript
function isChainValid(root as dynamic, propertyPath as string) as boolean
    rootPath = root
    properties = propertyPath.Split(".")

    if not isValid(rootPath) then return false

    ' Root path is valid, and no properties were passed. Return state of root
    if properties.count() = 0 then return true
    if properties[0] = "" then return true

    rootPath = rootPath.LookupCI(properties[0])

    if not isValid(rootPath) then return false

    properties.shift()

    if properties.count() <> 0
        nextPath = properties.join(".")
        return isChainValid(rootPath, nextPath)
    end if

    return true
end function
```

Using the `isChainValid` function, we can condense the entire object chain validation check into
a single if statement. Simply pass in a root object and a string of keys separated by periods and
`isChainValid` will safely check if each key is valid before checking the next one in the chain.

```brightscript
movie = { 
    data: {
        overview: {
            slug: "Just When You Thought It Was Safe To Go Back In The Water"
        }
    }
}

if isChainValid(movie, "data.overview.slug")
    print movie.data.overview.slug
end if
```
