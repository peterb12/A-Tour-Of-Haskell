# Week 5 - Higher Order Functions and Our Own Data Types

Note: There were a few  errors in last week's examples! If you think you've encountered an error in the GitHub document, please reach out on Google Classroom.

I think we lost a few of you last week, so I want to take a week to go over some conceptual stuff.  This week I'm giving you _optional_ homeworks, which are somewhat hard, and a basic homework, which is somewhat easy.

The [class program for this week is here](https://repl.it/@peterb/Week-5-Higher-Order-Functions), please fork your own copy.

## Dora, Say "Map"

Last week you wrote a function `myMap` which takes a function from `a -> b` and applies it to `[a]` (a list of type `a`) and returns a list of type `b`.  This is what we call a _higher order function_, and it's the answer to the question "Are you saying we do all loops in Haskell by recursion?"  We do, but we usually do them by using higher order functions.

Think about what we use loops for:

* Doing something to every item in a collection of items
* Looking at every item in a collection and reducing them to one answer.
* Taking a collection of items and making it smaller.

In fact, `map` is a standard Haskell library function that does the first task, and we didn't have to write it ourselves, but writing it yourself showed you how it works under the hood.

Using `map` we can easily transform entire lists of data:

```
  map (++ " is cool") ["Arnav", "Taylor", "Hannah", "Rex"]
=> ["Arnav is cool","Taylor is cool","Hanna is cool","Rex is cool"]
```

Want to take a list of numbers and get their squares? Map makes it easy. (`^` is an operator that says "for `a ^ b`, raise a to exponent b)

```
   map (^2) [1,2,3,4,5,6,7]
=> [1,4,9,16,25,36,49]
```

If you were doing this in Python, you'd probably write something like this:

```
newList = []
for item in [1,2,3,4,5,6,7]:
  newList.append(item ** 2)
```

Using `map` lets you think about this operation in a much simpler way! In Haskell, we said **what we want**, and in Python, we said **how to get what we want**. Often, saying how to get what we want is more complicated than just saying what we want. (Note: Python has its own version of `map`, but many people don't know about it...)

OK, so `map` will let us transform each element of a list. What other higher order functions are there?

## Filter

Remember last week when we wrote a function `avengersEndgameMovieGoers` that did this:

```
> avengersEndgameMoviegoers [5, 3, 20, 63, 13, 14]
=> [False, False, True, True, False, True]
```

That's an example of a map: we mapped from an integer (the age of the moviegoer) to a Boolean (whether they were older than 13.)

There's another Haskell function, `filter`, which will take a function that takes an item and returns `True` or `False` (called a "predicate") and then either _include_ or _exclude_ each item as a member of a new list, depending on whether the predicate is `True` or `False`.

```
> filter (>13) [5, 3, 20, 63, 13, 14]
=> [20,63,14]
>  filter odd [5, 3, 20, 63, 13, 14]
=> [5,3,63,13]
>  filter even [5, 3, 20, 63, 13, 14]
=> [20,14]
```

### OPTIONAL Homework 1: Write Your Own Filter

You knew it was coming:  Write a function `myFilter`.  Since lots of people had trouble with the type signatures last week, this week we are providing them for you.

Inputs: 
* a predicate function that goes from `(a -> Bool)` ("Given this a, is it true or false?"
* A list of type [a]

Output:
* A list of type [a], where `(f a)` for each item in the list returned `True`

HINT: You should write this as a recursive function (in fact, we gave you a head start and provided the base case.) Your job is to replace the word `undefined` with an actual function.  Don't use `filter` in your implementation, the point here is to write it yourself.

## List Origami

There's one more major category of higher-order function you should known about: _reduction_.

You've already written functions that reduce things!  Remember in Week 3, you wrote `myProduct`, which takes a list like `[1, 2, 3]` and determined the product, `6` (in other words, `1 * 2 * 3`.)

How important are `map` and `reduce`?  Here's a hint: the algorithm that allowed Google to index the entire internet, that their entire business is based upon, is called _MapReduce_.  They're not literally the same functions we are talking about here, but they are closely related.

In Haskell, instead of using the term _reduce_ they call it a _fold_, but it's the same thing.  Specifically, it's `foldr` with the "r" meaning "right" (as opposed to left).  `foldr` has a pretty complicated type signature, and we're going to try to not use it for this class, so consider this optional.

```
foldr :: (a -> b -> b) -> b -> [a] -> b
```

Phew, that's a lot!  But let me break it down for you.  `foldr` takes three arguments:

* A **function** that takes two arguments and returns a third.  This sounds complicated but really just about any arithmetic operator, like `+` or `*`, would qualify.
* An **initial value** that will be used for the first thing folded.
* A **list** to be folded.  (You can fold things besides lists, but let's keep it simple).

Foldr returns one value.  Note that _unlike map_, foldr isn't necessarily returning a list, but a value of whatever type the function returns.

So to give you two examples, here is how you could implement `product` and `sum` using only `foldr`:

```
product someList = foldr (*) 1 someList

sum someList = foldr (+) 0 someList
```

Hopefully this example helps explain why the "initial value" argument is necessary - reduction needs a value called an "accumulator" where, effectively, intermediate values are stored. If we tried to use `0` with our multiplication example, then our answer would always be `0`.  Likewise if we tried to use `1` as the initial value for `sum`, our answer would always be off by one.

### OPTIONAL: HOMEWORK 2 (advanced)

**You should probably skip this assignment and come back to it when you feel ready for a challenge.**

Write `myFoldr`. It should behave exactly the same as `foldr`.

This means it takes the same arguments as `foldr` (a function that takes two arguments and returns one, an initial value, and a list) and returns a value of the same type as is in the list.

This is tough.  Consider doing the rest of this lesson first and then saving this for last. If you can do this, take a victory lap on Google Classroom and show everyone your implementation. 

As before, the solution should be recursive, but since there are multiple arguments, it's pretty easy to get lost.  I gave you the base case for free; replace the `undefined` clause with your recursive case.

To test your `myFoldr`, try these:

```
> foldr (*) 1 [2, 3, 4, 5]
=> 120

> foldr (++) [] ["Super", "cali", "fragi", "listic", "expi", "ali", "docious"]
=> "Supercalifragilisticexpialidocious"
```

### HOMEWORK 3: Numbers Only, Please

Dr. DeMore has asked you to write a program to let her computer dial her phone for her.  Sadly, her phone system doesn't know how to handle special characters, only numbers, so a number like "(724) 555-1212" confuses it.  Write a function "phoneNumberSimple" which will take a number with punctuation like that and convert it to a number-only string such as "7245551212".

HINT: the Haskell library `Data.Char`, which is already imported and ready for use in our class program, has a useful predicate [isDigit](http://zvon.org/other/haskell/Outputchar/isDigit_f.html).  I've linked to the documntation for it - you don't have to do anything difficult here, you can just use `isDigit` as if it's a function you wrote.  After clicking Run, you can test it in the repl:

```
> isDigit 'a'
=> False
> isDigit '9'
=> True
```
You may use this predicate if you want, or write your own.

Don't write this as a recursive function!  Use a higher-order function to do the heavy lifting for you.  The best solution will be just one line.

### HOMEWORK 4: Any and All

Write a function `myAny` which has the following type signature:

```
myAny :: (a -> Bool) -> [a] -> Bool
```

In other words, it takes a function that returns `True` or `False` for a given `a`, and then will return True if the list `[a]` has any members for which that value is true.

```
> myAny odd [4, 6, 2, 7, 3, 17]
=> True
> myAny odd [4, 6, 2]
=> False
```
Next, write:

```
myAll :: (a -> Bool) -> [a] -> Bool
```

This is similar to `any`, but instead will _only_ return `True` if _every member of the list_ passes the predicate.

```
> myAll even [4, 6, 2, 7, 3, 17]
=> False
> myAll even [4, 6, 2]
=> True
```



## Data types: Sum Types

Up until now, we've been using Haskell's built in data types, like Strings.  Strings can be a pain to work with, however, because they can have all sorts of data in them, like the parentheses in our phone numbers in homework 3, or the "garbage" nucleotides in our DNA example in week 2. Haskell lets us easily create our own custom datatypes which **only** support exactly the values we want. This is very powerful way to let us write simpler code - typically, you'll have a "skin" on your program that converts from Strings to some internal data type, and then all of your internal code can be _much_ simpler because it won't have to worry about bad input!

### WORKED EXAMPLE: Better Nucleotides

In Week 2, you probably had a `nucleotidePattern` function to determine the complement of a piece of RNA that looked something like this:

```
nucleotidePattern :: Char -> Char
nucleotidePattern 'A' = 'T'
nucleotidePattern 'T' = 'A'
nucleotidePattern 'C' = 'G'
nucleotidePattern 'G' = 'C'
nucleotidePattern  _  = 'X'
```

But that last wildcard pattern is sort of a problem - there is no "X" nucleotide, and if your DNA has that nucleotide in it you might be a space alien.  So we'd rather that not be representable at all!

Let's define a nucleotide type:

```
data Nucleotide = Adenine | Guanine | Cytosine | Thymine deriving (Show, Ord, Eq)
```

The `|` character in that declaration is read as "or".  This says that our data type `Nucleotide` can only be one of those four words, _and nothing else_.  This is called a _sum type_ or sometimes a _tagged union_; I'll call them sum types.  A sum type represents an **exclusive choice** from a set of values.  So in our current example, if I say that the variable `rna` is of the type `Nucleotide` I am making you an _ironclad guarantee_ that it is one of an `Adenine`, a `Guanine`, a `Cytosine`, or a `Thymine`, and that it can not be any other possible thing in the universe.

Those words are now special. They're not strings, they're now actually _values_.  In the example that follows, note that we are **not putting those words in double-quotes**.  Effectively, we have turned them into language keywords in our program - they are _values_, like the integer 3.  The fancy term for this type of value is **data constructor** (remember that term, because it's going to appear again in homework 5.)

The `deriving (Show, Ord, Eq)` is a little bit of magic that will make this work better in our REPL: the `Show` means that Haskell will know to print it out using its name, and the `Ord` means it will consider them to have an ordering based on how we typed them. For example, if you were creating a type for the alphabet, you might type the letters in in alphabetical order. The `Eq` means that Haskell will allow you to compare them with the = sign.  For right now, if you define a data type, just go ahead and throw `deriving (Show, Ord, Eq)` on the end and it will almost certainly be what you want. 

This lets us define a new function in terms of that data type:

```
betterComplement :: Nucleotide -> Nucleotide
betterComplement Adenine = Thymine
betterComplement Thymine = Adenine
betterComplement Cytosine = Guanine
betterComplement Guanine = Cytosine
```

Go ahead and replace the betterComplement function in the class REPL with that.

We don't even need a wildcard case here because it's **literally impossible** for us to compile code that feeds in a bad value to this function.  (Our "skin" code - which is not here, because we didn't write it - that converts from things the user types _into_ this data type will still need that wildcard case, and next week we'll introduce the idea of `Maybe` which is how we will handle it).

After clicking "Run" again, typing `betterComplement Cytosine` into the REPL to see what happens.  You should get

```
>  betterComplement Cytosine
=> Guanine
```

### Homework 5: Playing Cards

A deck of playing cards is composed of 52 playing cards, not counting jokers.

Each card consists of a rank, which can range from Ace, the numbers Two through Ten, or Jack, Queen, or King.

Each card _also_ consists of a suit, which can be Hearts, Spades, Clubs, or Diamonds.

So to represent a card, we need both a rank **and** a suit, and I haven't shown you how to do that yet.  But we **have** talked about how to represent "or" values, like our nucleotides, with Sum types.

Using a sum type (a type that uses `|` to define alternative values), define two data types:

* A `Suit` data type that represents all possible suits.
* A `Rank` data type that represents all possible ranks.

If this sounds complicated, you're overthinking it.  Just use simple names for the data constructors.  Both type names and data constructors **must** start with a capital letter, and I suggest you don't use funny symbols or numbers.

### Homework 6: Post on Google Classroom.

First, and most importantly, I want you to post on the classroom telling the class the most awesome thing you did this week.  It doesn't need to have anything to do with this class, just tell us something you did that was fun.

Second, although we haven't talked about how to do "and" types, tell the class how you think, given a rank and a suit, we might represent a single playing card in a reasonable programming language.  If you have used another programming language where you think you know how to represent it, feel free to give that as an example, or just describe it in words.
