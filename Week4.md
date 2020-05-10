# Week 4 - Generalizing Recursion

Let's do some more recursion this week, and take steps towards generalizing 
it.

To mix things up a bit: By now, you should have some idea of how to write functions.  I am providing an almost blank REPL for you this week, [click here](https://repl.it/@peterb/Week-4-Generalizing-Recursion), and not providing any function names or type declarations or writing any tests for you.  Write your functions from scratch, and then prove that your functions work by testing them in the REPL.

No worked example this week - I'm going to give you three super-simple recursive functions to write that shouldn't give you any trouble. Homework 4 is where you think about what you did, and post on the Google Classroom.  Then, in Homework 5, we're going to take everything we know and start putting it together. The real _Dark Souls_ begins in Homework 5.

### A Note on Type Signatures

Up until now, whenever you've seen a type signature, it's always started with an actual, real type - what we call a "concrete" type, like `Int` or `Bool` or `Double`.

However, Haskell also supports something called a -- $10 word incoming -- _polymorphic_ type, which means a type that could be one of any of a number of types.  This is a deep topic, and we're not going to get very far into it, but the upshot of this is that if you see a type that begins with a **lowercase letter** like:

```
listLength :: [a] -> Int
```

What that means is that the lowercase letter can be _of any type_.  In the case of `listLength`, for example, we don't care if it's a list of `Doubles` or `Bools` or `Strings` or anything else - we're just counting the things in it, not doing anything with them. So we just say it's a list of `a`, where `a` can be anything.

You'll need this knowledge for Homework 5.

## Homework 1 - Add 1 to every number

Write a function called `addOne` that takes an Int and returns a number that is one greater.

Then, write a function called `addOnes` that takes a _List_ of `Ints` and returns a list of Int where each number is increased my one.  Your `addOnes` function **must** use your `addOne` function.

Example:
```
addOne [1, 2, 3, 4, 5]
=> [2, 3, 4, 5, 6]
```

If you decide to write a type signature for this function (which might help with homework 4), remember that a List of `Int` has the type signature `[Int]`.

## Homework 2 - Multiply every number by 5.

Write a function called `multFive` that takes an Int and returns a number that is that number multiplied by 5.

Then, write a function called `multFives` that takes a _List_ of `Ints` and returns a list of Int where each number is multiplied by 5.  Your `multFives` function **must** use your `multFives` function.

Example:
```
multByFive [1, 2, 3, 4, 5]
=> [5, 10, 15, 20, 25]
```
## Homework 3 - olderThan13

Write a function `olderThan13` that takes an `Int` (representing the age of a kid) and returns a `Bool`: True if the kid is older than 13, or False otherwise.

Then, write a function `pg13Attendees`, given a list of `Int`s representing the ages of kids you know, returns a _List_ of `Bool`s where each item in the list is `True` if the corresponding input age was greater than 13, or `False` otherwise.  You **must** use your `olderThan13` function when writing this.

```
olderThan13 [5, 3, 20, 63, 13, 14]
=> [False, False, True, True, False, True]
```

## Homework 4 - convertDNA 

Go back and read your `convertDNA` function from last week. Then look at `addOnes` and `multByFives` and your `pg13Attendees` functions.  How are they similar?  How are they different?  If you chose to write type signatures for your functions, what are they?

Please post your answer to these questions on Google Classroom.

## Homework 5 - Abstraction

Now comes the fun part.  I'm going to hurt your brain a little.

Functions in Haskell can be passed around just like values.  What I mean by this is that you can use a function as an argument to another function, or return a function as a result from a function.

Take a look at your `multByFives`, and your `addOnes` functions, and your `convertDNA` functions.  All of these functions take a list with some item type `a` and apply some transformation to each item in the list, using some function `(a -> b)`, to turn the whole list into a list of type `b`.  (It's possible for types `a` and `b` to be the same, but they don't have to be - for `multByFives` and `addOnes`, both `a` and `b` are `Int`s, but for `pg13Attendees`, `a` is an `Int` and `b` is a `Bool`.)

Write a function `myMap` that takes as an argument:
 * A function that goes from `(a -> b)`
 * A list of `a`
and returns
 * A list of `b`

In other words, your myMap should have the type signature:
```
myMap :: (a -> b) -> [a] -> [b]
```

Homework five is done when you can run these examples in the REPL and get the right answer:

```
myMap addOnes [6, 7, 8, 9, 10]
=> [7, 8, 9, 10, 11]

myMap pg13Attendees [5, 3, 20, 63, 13, 14]
=> [False, False, True, True, False, True]

myMap convertDNA ['T', 'T', 'C', 'G', 'A']
=> ['A', 'A', 'G', 'C', 'T']
