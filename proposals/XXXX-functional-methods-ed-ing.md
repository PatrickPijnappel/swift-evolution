# Apply -ed/-ing rule to core functional methods

* Proposal: [SE-NNNN](NNNN-functional-methods-ed-ing.md)
* Author: [Patrick Pijnappel](https://github.com/PatrickPijnappel)
* Status: **Awaiting review**
* Review manager: TBD

## Introduction

The Swift API Guidelines standardizes non-mutating method forms on verbs ending in -ed/-ing (or nouns). However, a few non-mutating forms have been kept as "Terms of Art":
`map`, `flatMap`, `filter`, `reduce`, `dropFirst` and `dropLast`. This proposal proposes to bring these in line with all other non-mutating forms (e.g. `filter => filtered`).

Swift-evolution threads: [Source](http://news.gmane.org/find-root.php?group=gmane.comp.lang.swift.evolution&article=20783), [Draft](http://news.gmane.org/find-root.php?group=gmane.comp.lang.swift.evolution&article=20864)

## Motivation

These method have been kept to preserve the terms of art. Generally, this can have significant benefits:
- Anyone familiar with the term will immediately understand it, and use their assumptions about how it works.
- Users learning the term from Swift can use their knowledge when encountering it elsewhere.
- Experienced users will be able to use the mental pattern matching they've built-up for quickly recognizing common programming patterns.

However, basically all of the benefits of using a term of art still apply to the modified forms:
– For recognition, the modified forms are still very close to the traditional terms of art. So both coming to and from Swift you'll be able to use your knowledge pretty much unaffected.   
- If the user looks for e.g. `filter` they are pretty much guaranteed to quickly find the correct form, be it through code-completion, google or a fix-it.
- There isn't really any violation of assumptions that might cause problems in this case.
- Any mental pattern matching will likely transfer quickly due to the minimal difference.

## Proposed solution

The proposed solution modifies the method verbs to their -ed/-ing forms (preferring the former). 

It removes the last clear exceptions to the -ed/-ing rule from the standard library, which previously
were exactly the opposite of what one would expect based on the API guidelines (and the rest of the language).

It also aids users in learning to pattern match on the -ed/-ing rule and internalizing the API guidelines,
since now all methods are named this way – instead of the most commonly used methods defying the normal pattern.

## Detailed design

The change would rename the following method families:

```
map       => mapped
flatMap   => flatMapped 
filter    => filtered
reduce    => reduced
dropFirst => droppingFirst
dropLast  => droppingLast
```

## Impact on existing code

The Swift migrator and fix-its would be provided for the change. 

## Alternatives considered

- Alternatively -ing suffixes could be used for `map`/`flatMap`/`filter`/`reduce`. However, these are normally reserved for when -ed doesn't really work (e.g. droppedFirst).  
