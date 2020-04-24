## Week 2

Welcome to week 2!  This week is going to start easy, but will finish up introducing some simple techniques that will help us solve more complicated problems.

This week is probably going to be easier than last week. The reason for this is that I'm introducing three things to you that do essentially the same job.  The differences in syntax between them are in some cases subtle, so pay attention as you write them and see if you can understand when you might use one instead of another.

We're also going to give you a very quick preview of a new data structure: the list.

The REPL for this week's exercise is here: https://repl.it/@peterb/Conditionals

Please Fork your own copy of the REPL and then follow along with this document.

## A Word About Error Messages

Last week some of you encountered what I consider to be the very worst thing about Haskell - its error messages. There's no getting around this - all programmers make mistakes sometimes, and when we do, we're going to get an error message. I want to take some of our time to look at an example of an error message and how to read it.

Haskell's error messages tend to be very, very long and very wordy. There's a technical reason for this, which is that the language tries to protect you from making a certain class of mistake called a type error by requiring all types in your program to match, but it also tries to _guess_ what type you mean where possible. This prevents you (for example) from using a Boolean in a place where an Integer was expected.  Let's take a simple example.

If you remember last week, we had this function, `complicatedFourteen = 1 + 5 + 8`.  What if instead we wrote, `complicatedFourteen = 1 + 5 + True`?

We'd get this error message:

```
main.hs:7:23: error:
    * No instance for (Num Bool) arising from a use of `+'
    * In the expression: 1 + 5 + True
      In an equation for `complicatedFourteen':
          complicatedFourteen = 1 + 5 + True
  |
7 | complicatedFourteen = 1 + 5 + True
  |                       ^^^^^^^^^^^^
<interactive>:3:1: error:
    * Variable not in scope: main
    * Perhaps you meant `min' (imported from Prelude)
```

That's a lot of text for an error that you already understand!  The most important part is probably the very first line, which tells us that the problem began on line 7.  Then `No instance for (Num Bool) arising from a use of "+"` is telling us, awkwardly, that `+` expects a Num (which includes both Ints and Doubles), but instead got a Bool, and there's no Number instance for the type Bool.  The reason the error message is so complicated is that we can make very complicated types, and Haskell will try to infer what we mean as much as possible. This verbose error is more helpful when you're working with more general types, but can be frustrating in the simpler cases. 

the last 3 lines of the error message are effectively meaningless - the earlier error confused the compiler, so it no longer knew what to do with the rest of the program.  

It's generally a good idea to deal with your errors from the top down - fix the first thing you find, then click 'Run' again and go on to the next one.

## Making Decisions

Last week all of the expressions we wrote were very straightforward. Given an input value, the computer could find the answer by just repeatedly simplifying the expression.

But sometimes our expressions need to be more complicated than that. We may want to make different decisions about our answer depending on what in our environment is true.  Today we're going to look at two different ways to make decisions in our program:  Conditionals and Pattern Matching.  (There are actually at least two other techniques that do the same thing as conditionals - _guards_ and _case expressions_, but we're not going to go into them here. Feel free to look them up yourself later if you're interested.)

Both of these techniques will be useful at different times. You can often rewrite code written one way so that it uses the other technique.  Which you use often depends on which is easiest to write, or to read and understand.

More generally, this aspect of Haskell is something that is both good and bad.  The bad thing is that for any task, there's more than one way to do it. The good thing is _also_ that for any task, there's more than one way to do it.

### Our Example: DNA Nucleotides

If you've taken a biology course that talks about DNA, you may know about nucleotides; these are the molecules that make up our genes.  The molecules fit together in a very specific way so that when a DNA (or RNA) molecule is created, it always fits together. We can say that the nucleotide that "plugs into" another nucleotide is its _complement_.

There are four types of Nucleotides: adenine, guanine, thymine, and cystine.  For convenience, let's call these `'A'`, `'G'`, `'T'`, and `'C'`. (There's actually a `'U'` for RNA as well, but let's ignore that one for now).

The rules of complement are as follows:

* The complement of `'A'` is `'T'`.
* The complement of `'T'` is `'A'`.
* The complement of `'C'` is `'G'`.
* The complement of `'G'` is `'C'`.

You may have noticed that we are now using a new datatype: `Char`, which represents a character.  The rules of Char are pretty simple: each Char represents a single letter or number or symbol, and if you want to quote one literally, you enlose it in single quotes, like this:  `'Z'`.  Chars are distinct from numbers even when they look like them:  `5` is a number, but `'5'` is the character 5 - you can't substitute one for the other.  Lastly, a Char is *just one character*.  You can't say `'ABCDE'` and have it still be a Char.  (Those are Strings, which we will get to later, and they would be written `"ABCDE"` - note the double quotes.)

In the following sections, we're going to write a function that takes a single character representing a nucleotide, and returns a single character representing the complement of that nucleotide.  For right now, if we come across a character we don't recognize, we will return `'X'`. (This is actually not a great way to do this - one of the most powerful tools Haskell gives us is the ability to define types in a way that prevents us having to write lots of error-handling code, but we will get to that in a future week).

### Conditionals: if-then-else

Let's start with something you might be familiar with from other programming languages: the idea of `if`.

This _if_ is what we call a _conditional expression_.  The _conditional_ part means that it will evaluate differently depending on some condition.  The _expression_ part means that it _must evaluate to something_.

In Python or other languages you might be used to writing something like this:

```
def checkName = if (myName == "Lydia"):
                  return "Hi, Lydia!"
```

Haskell's syntax is similar, but with a wrinkle: there must _always_ be an `else` part of the expression, because without it the expression would not evaluate to anything.  So we'd have to write the above example like this:

```
checkName myName = if (myName == "Lydia") then "Hi, Lydia!" else "Sorry, I don't talk to strangers."
```

Sometimes it can also be helpful to format your if statements to make them easier to read.  This code is the same as the last example, just written differently:

```
checkName myName = if (myName == "Lydia")
            then "Hi, Lydia!"
            else "Sorry, I don't talk to strangers."
```

(This program is in your REPL; try it out.)

#### Worked Example: The Vowel Game, with `if…then…else`

Let's say we're playing a word game where the goal is to play words with lots of vowels.  In this game, the vowels A, E, I, O, and U are worth 2, 1, 3, 4, and 5 points respectively; all other letters are worth 0.  As part of writing a computer version of this game, we want a function that will tell us the score for a particular letter.

```
letterScoreUsingIf letter = if (letter == 'A') then 2
```

We're not done yet, though - this won't even compile! Remember, the `else` clause is *mandatory*


```
letterScoreUsingIf letter = if (letter == 'A') then 2
                              else 0
```

Of course, the letter might not be an `'A'`, so we have to write _another_ if to handle the next case:

```
letterScoreUsingIf letter = if (letter == 'A') then 2
                              else if (letter == 'E') then 1
                                else 0
```

And we do this several more times:

```
letterScoreUsingIf letter = if (letter == 'A') then 2
                              else if (letter == 'E') then 1
                                else if (letter == 'I') then 3
                                  else if (letter == 'O') then 4
                                    else if (letter == 'U') then 5
                                      else 0
```

Note our final `else` clause, which will handle any letter that isn't a vowel.

Now we can try it in the REPL:

```
letterScoreUsingIf 'O'
=> 4
letterScoreUsingIf 'X'
=> 0
```

So as you can see, if statements are pretty simple, but they have some drawbacks - in particular, if you need to nest several conditions in a row, they can be a bit hard to read.  We'll learn some alternatives to `if` after your first homework.

## Homework 1: Nucleotides, Using If
Write a program which, when given a nucleotide (such as 'A'), returns that nucleotide's complement (such as 'T').  If the letter provided is not a valid nucleotide, return 'X'.

It sounds pretty easy, doesn't it?  The letter score example should give you a pretty good sense of how to proceed.  

Fill in the function `nucleotideIf` in the REPL, replacing the current return value ('Z') with a program that returns the proper value.

One note: since this function is looking at _individual characters_, remember to enclose them in single-quotes, like this: `'A'`, NOT in double-quotes.

### Pattern Matching

So far, every time we've written a function, we've written it one time and never re-used the name.  Furthermore, when defining the parameters to the function, we've just given it a single name (like `letter` in the letter score example) and then adjusted our code inside the function to deal with the fact that the parameter could contain any argument.

Haskell lets us do something really powerful, though: it lets us write functions for _specific_ arguments, by effectively writing the function multiple times - with a different function body for each argument.

#### Worked Example: The Vowel Game, Pattern Matching.

We're going to write our letter score function again, only this time instead of using a deeply-nested `if` statements, we're going to use pattern matching.

In your repl, find the function:

```
letterScorePM _ = 99999
```

That code means "Given ANY input (the `_` means "anything"), return the value 99999.  Obviously that's not good enough for our game; let's fix it.

The first case we need to handle is the vowel `'A'`.  Our rules say that `'A'` is worth 2 points.

```
letterScorePM 'A' = 2
```

That's it!  Note that instead of giving the function parameter a name like item or x or number, we specified a _literal `'A'` character_ as the function parameter.  This means that this function will _only_ run when the argument to it is `'A'`.

Let's write the rest of the functions.  I bet you can see how this will go.

```
letterScorePM 'A' = 2
letterScorePM 'E' = 1
letterScorePM 'I' = 3
letterScorePM 'O' = 4
letterScorePM 'U' = 5
```

That handles all of our vowels.  But we still need to handle the case where the function is called with anything else.  In Haskell, `_` in a function parameter means "I don't care, I'm going to ignore this," so we can use that here to handle all the other cases.


```
letterScorePM 'A' = 2
letterScorePM 'E' = 1
letterScorePM 'I' = 3
letterScorePM 'O' = 4
letterScorePM 'U' = 5
letterScorePM  _  = 0
```

That's it! Try it out in the REPL.

One note: **the order matters**: Haskell will check these cases from top to bottom in the order in which they were declared.  When you're matching on a literal this isn't that important, but if you were to move the `letterScorePM _` line above the `A` case, every letter would be worth 0, which would be wrong.

### Homework 2: Nucleotides, Using Pattern Matching

Please write a new version of the nucleotide function you wrote for Homework 1, using the function named `nucleotidePattern`. This time, don't use if, and instead use pattern matching to accomplish the task.

### Editorial Comment

Pattern matching is probably **the single most important syntax you'll learn in Haskell**.  It actually does more than we are telling you here.  It's not just a fancy conditional, but also is the **primary way** that we break down complex data structures to allow us to write easier functions. Since we don't have any complex data structures yet, you're not seeing this side of it.  But if you remember one thing from this chapter, make it pattern matching.  Pattern matching should always be the first technique you reach for when solving problems in Haskell. It won't always apply, but when it does it will usually be the best way.

## Lists

We've been talking about DNA here, but when we wrote our progams, we've just been manipulating genes a single gene at a time.  But people's DNA is composed of _many_ genes, not just one. How do we represent that in Haskell?

You won't be surprised to hear me say "There's more than one way to do it", but one of the most fundamental data structures in Computer Science, and one that is used a lot when teaching programmers, is the _list_.  Next week we are going to be spending a lot of time with lists. For this week, I wanted to give you just the briefest introduction to them.

A list in casual conversation has a simple definition: a collection of items, in a specific order.  The formal definition is a little more involved, and in English is this:

> A _list of some type t_ is either:  [] ("the empty list") **or** an object of type t put **onto the front of another list** of some type t.

One implication of this definition is that a list can only hold objects of one type.  `[1, 2, 3, 4]` is a list.  `['A', 'B', 'C', 'D']` is a list.  but `[1, 'A', 2, 'B']` is not a list, because it contains multiple types, and can't be built.  (There *are* ways to build lists that contain all of those items, but you can to use another data structure, the tuple, that we haven't introduced yet)

The operator we use to build a list is `:`.  This is pronounced `cons`, which is short for "constructor", for historical reasons.  When the above defintiion says "put onto the front of another list" that means we take the item we want to add to the front of the list, and use `:` to do it.  

Let's say we're working with lists of Ints, and we want to end up with a list of the numbers 1, 2, and 3, in that order.  There are very simple ways to do this, but let's do it the **hard** way first.

The funny thing about the definition above is that it says you can only build a list _if you already have another list_.  The number "3" by itself _isn't a list_.  It's only a list if you attach that number to a list.

Fortunately, there's something that is always a list, that appears in every list: the empty list, or `[]`.  So we can put 3 onto the empty list, like so:

```
3 : []
```

If you type this into the REPL, you'll get back

```
=> [3]
```

And we can extend this logic to all the numbers we want:

```
1 : 2 : 3 : []
=> [1, 2, 3]
```

In fact, we can simply type `[1, 2, 3]` if we want that list, and it will work fine - Haskell knows what we mean.  But _under the hood_, keep in mind that that list represents `1 : 2 : 3 : []`, because next week it's going to be _very important_ that we remember that the empty list is there.

### Homework 3: Writing a List

In your REPL are two names, `myLongDNA` and `myLongComp`, both currently set to the empty list.

In `myLongDNA`, write a list of 6 valid nucleotides - they can be whatever you want, as long as they are one of the four nucleotides `A`, `C`, `T`, and `G`.  Write this list in the `[1, 2, 3]` list syntax we just discussed.

In `myLongComp`, write a list of 6 nucleotides that complement the 6 nucleotides you chose for `myLongDNA`.  Please write this list in the `1 : 2 : 3 : []` format.

Bonus question: Write a one-line function that **proves** that the list `[1, 2, 3]` is the exact same thing as the list `1 : 2 : 3 : []`. Name it whatever you want.

As always, if you have any questions, feel free to post them on Google Classroom!
