# Welcome to Haskell!
## Why Haskell?
Haskell is a computer programming language that is probably unlike any you've used before. Haskell is what we call a _functional_ programming language which means that rather than focusing on executing statements sequentially, the language encourages you to break down problems into _expressions_ and _functions_.  Functions are just a fancy kind of expression that can take one or more arguments and use them to compute an answer. This is limiting in some ways, but can make it easier to break down large problems into very small parts that are very easy to put together. Haskell has a reputation as a hard language to learn and master. but once we get some practice with it we'll be able to use it to understand some very fundamental concepts in computer science. Knowing these fundamentals will give you an advantage in every other programming class you take, no matter what language it uses.
## Getting Started
In this lesson, we're going to be using the `repl.it` environment to do some Haskell programming. To get started, go to the website [`https://repl.it`](https://repl.it) and create an account. Once you've done that, please visit the **week 1 class program** [`https://repl.it/@peterb/Expressions-and-Functions`](https://repl.it/@peterb/Expressions-and-Functions) and choose `Fork` from the top of the screen to create your own copy.  From now on, I will sometimes call your copy of the repl.it coursework the "class program window"

In particular, you should see a big black window to the right of this text.  This is called the REPL. That stands for _Read-Eval-Print Loop_.  Unlike in  `Code.World`, you can type in things in the REPL, and Haskell will evaluate them immediately.

**Any time you make a change in the repl.it editor, you MUST click "run" before testing your code in the REPL.**

## How to Take This Class
Have this document open in one browser window, and have another browser window open to the repl.it link open to your copy of the **week 1 class program**, mentioned above.  Whenever this lesson talks about something you can try on repl.it, _stop what you are doing and actually try it_.  At the end of this lesson, you'll have two homework assignments to do. You're on your own for these, but you can ask questions on Google Classroom and we will answer them.

A note on typography: when you see numbers or words that look `like this`, that usually means it is something we either are typing into the REPL, or something the REPL is printing back to us.

This class is going to start very slowly, because Haskell is so different to other programing languages you've used. If you're experienced, you may feel insulted by how little material we cover this week. But I want to make sure everyone is able to use the tools we're providing, and I want to make sure we get the fundamentals of writing expressions and functions down cold. Future weeks will be more challenging, I promise.

One last note: the goal of this class is to teach you about basic computer science patterns, in the context of a weird programming language. When you're done with this class, you will be able to impress people at parties with your amazing knowledge of obscure computer programming languages. There are no grades, and the only reason to do this is because you want to.  In the course of the class, you may find yourself getting stuck on some of the homework assignments. You can get yourself unstuck _any way you want_: ask your teachers, talk to your friends who are taking the class, read a Haskell book. Most of the homework assignments here are very well-known problems. You can undoubtedly do Google searches to find answers to them, and nobody is going to bust you for it. The only thing I suggest is that if you do that, _take your time and try to understand the answer that you're finding_. If you google for the answers in the early weeks without understanding them, you'll be completely lost in the following weeks.
## Expressions
Before anything else, make sure you **go to the class program window  and click (or tap) the "Run" button**.  The examples in this document **will not work if you don't do that.**  There will be some messages in your REPL window (the big black area on the right) about tests passing and failing. This is normal. Then, below that, will be a > prompt. That's where you are going to type.

Most of the things we type are called _expressions_. An expression is any combination of symbols that can be simplified to a _value_. You can think of a value as any expression that is in its simplest form.

For example, go there now and type `123` and hit enter.  Haskell should reply with

`=> 123`

Which is its way of saying "the number 123 is the same as the number 123" -- in other words, 123 == 123. This may not seem very useful, but it means that if we want to evaluate an expression, we can try it out in the repl.  So if we type `123 + 456`, for example, the REPL will reply...

`=> 579`

...which is the value that the expression we typed in adds up to.

In this lesson, we're going to learn about some of the values and expressions we can use in Haskell, focusing on numbers.  We'll also learn how to name expressions (sometimes called "binding a name").  Haskell does a lot more than just math, but we're going to start here to keep it simple. 
## Simple values
We're going to be looking at three of the simplest kinds of values Haskell knows about: Ints, Doubles, and Booleans.

An Int is a whole number: `0`, `7`, `781958`, and `(-66)` are all Ints. A Double is a floating point number, which is like a decimal: `1.5`, `3.33333`, and `7.2` are all Doubles. Unlike the numbers you use in math, Ints and Doubles actually have some technical limitations - they're not quite the infinite numbers you're used to from math class - but they won't be relevant for this first lesson. Booleans are the simplest type: `True` and `False` are the only boolean values.

In our lesson today we're going to need some simple math to help us, so I'm going to introduce you to some math functions (we'll explain a little more about functions later on).

The basic functions you'll need for this module are:

`+`: add two numbers. Try typing `66 + 44` in the REPL

`-`: subtract two numbers. `66 - 44`

`*`: multiply two numbers. `66 * 44`

`/`: divide two Doubles. `66.0 / 44.0`

`==`: Equal to. Evaluates to `True` if two things are equal, `False` if they are not.  Try `66 == 44` in the REPL.

`/=`: Not equal to. Evaluates to `True` if two things are not equal, `False` if they are equal. Try `66 /= 44` in the REPL.

`rem`: The Int remainder from division.  Try typing `rem 19 5` in the REPL - you should get back `4`: 5 goes into 19 only 3 times (making 15) and 19 - 15 = 4.

You might notice that unlike `+` or `-`, `rem` came _before_ the numbers it was applied to, not in between. You'll see more of this later.
## Naming Expressions
In Haskell (and in many programming languages), an expression is something that evaluates to a value. This should be familiar to you from your math class. For example, the expression `1 + 5 + 8` evaluates to the value `14`.

We can also _name_ expressions. Most of the programming you do in Haskell is going to involve naming expressions and combining smaller expressions into larger ones.

On **line 6** of the class program, you should see a line that looks like this:

```fourteen = 14```

Go ahead and type `fourteen` in the REPL, and Haskell should reply with `14`. We bound the _name_ "fourteen" to the _value" `14`.  As far as Haskell is concerned, these two things are now almost completely interchangeable.

On **line 7** of the class program, you should see:

```complicatedFourteen = 1 + 5 + 8```

and if you type `complicatedFourteen` in the REPL, it will also reply with `14`. So we gave the name `complicatedFourteen` to the expression `1 + 5 + 8`, and Haskell will remember that.  What we name expressions is entirely our choice (although they have to start with a lower-case letter: we will explain why in week 4).

As far as Haskell is concerned, all expressions are reduced before they are evaluated. So to Haskell, `fourteen`, `complicatedFourteen`, `14` and `1 + 5 + 8` are effectively all the exact same thing.  If you would like to test this for yourself, go to the REPL and type `fourteen == complicatedFourteen`.  It will reply with `True`.

## Functions
If the only thing we could do with names is use them to refer to expressions like `1 + 5 + 8`, they'd be pretty boring. Fortunately, they do more than that.

There's a special type of name called a _function_ that allows the us to _substitute our own values_ into an expression that is written in a certain way at the time it is used. We call these values that will be substitued _arguments_ or _parameters_. (Technically , the _parameter_ is the name you give to the thing passed into the function, and the _argument_ is the actual value the parameter represents. In practice, the two terms are used interchangeably and if you use either one, everyone will know what you mean.)

We can think of a function as being like a box: it's going to take one (or more) arguments in one side of the box, and then will spit the answer out the other side.  We say that the argument to a function is its _input_ and the value it spits out the other side is its _output_.

We can also make named expressions that take a single 'argument' as input, and build an expression from that argument. When the function is evaluated, the value of the argument is substituted into the main expression and that whole thing is evaluated to get the final value.  We call these things "functions". 

On **line 8* of the REPL, you will see a simple function that takes one input:

```plusOne x = x + 1```

If you type `plusOne 5` into the REPL (the capitalization matters!) what you get back is `6`.

Notice the `x` to the left of the `=` sign in the definition of `plusOne`.  We say that when we called `plusOne 5`, x is _bound_ to the argument 5.  So on the right side of the = sign, the expression  becomes "5 + 1", which reduces to 6. This is a little different than the sort of naming we do when writing our expressions and functions, because `plusOne` can be used with all sorts of arguments. If we call `plusOne 10` then x will be bound to the argument 10 for the duration of that call.  If we call `plusOne 5 + 100 + 200`, then x will be bound to the value `305`.

In most programming languages, we would say that the "5" is an input to the function `plusOne`. We might call it a _parameter_ or an _argument_ to the function. If you've programmed in Python, you're probably used to function arguments being fed in to a function by appearing in parentheses, like this:

`plusOne(5)`

In Haskell, all you need to do is put the argument (or arguments) after the function name:

`plusOne 5`

Haskell books like to describe this as, "We are applying the function 'plusOne' to the value 5". This no-parentheses syntax is one of the things people find confusing about Haskell at first, but you will get used to it after a while.

We named our argument to the plusOne function "x", but there is nothing special about that name. We can pick whatever name we want. For example, on **line 9** of the REPL, we have

```sillyPlusOne clownCar = clownCar + 1```

This function is effectively the same as the original plusOne. We just used different names. Haskell typically doesn't care what names we choose, as long as it begins with a lower case letter.

## Worked Example: Is It an Odd Number?
Let's say we want a function to determine if a number is an odd number.  This function will take one input (a number) and it will return a boolean.  If the function returns `True`, it means the number is odd, and if it returns `False`, it means the number is even.

Let's call our function `isOddNumber`.  On **line 11** of the REPL, we have started by
writing it "wrong" so that it says that every number is odd.

```isOddNumber num = True```

If you go to the REPL and type `isOddNumber 2`, it will tell you `True`, or in other words that 2 is odd.  This is obviously wrong! 

`True` in that example is just a placeholder I put there for your convenience. So we need to replace `True` in our function above with something that actually tells us if a number is odd.  How do we know whether a number is odd or even?  Looking it up, the definition of an odd number is _"Any integer (not a fraction) that cannot be divided exactly by 2"_.

When you divide a number evenly, it has no remainder. There's a Haskell function that will tell you if an integer division has a remainder, `rem`.  So if the remainder of a number divided by 2 is anything other than 0, it's odd. 

Reminder for this example: **remember to click or tap run** after every change you make to the REPL; if you don't do this, the computer won't know to use your new version.

1. Change the function definition on **line 11** (in the editor window on the left, not in the REPL) to:

```isOddNumber num = rem num 2```

What this expression is saying in English is "`isOddNumber num` means 'the remainder of some number divided by 2'".

2. Now **click or tap run**, and then in the REPL try a few tests, such as `isOddNumber 7` and `isOddNumber 100`.  Do you get `True` or `False`?

No, you don't!  You probably got a number.  This means we're not done yet.  What we get back is the remainder, which in this case is always 0 or 1, and this isn't what we wanted.  To convert this to a boolean, we need to compare it. There are lots of comparisons in Haskell, but the two we care about right now are:

`==`: are two things equal to each other

`/=`: are two things not equal to each other

3. Let's change **line 11** again. This time, make it say:

```isOddNumber num = rem num 2 /= 0```

(Remember to click Run again!) 

To read that above function in English: "The remainder of the number divided by 2 is not zero."  What would happen if we called `isOddNumber 6`?

We know that 6 is an _even_ number, so we want `isOddNumber 6` to return `False`, right? Let's see what happens if we substitute `6` for `num` above.  That would be `rem 6 2 /= 0`.  `rem 6 2` is going to evaluate to `0` (because **6 divided by 2 equals 3, remainder 0**), which would leave us with `0 /= 0`, or in English "0 is not equal to 0".  This is false, and the computer knows it just like we do, and indeed this function will return `False`, which is exactly what we wanted.

If on the other hand we called `isOddNumber 7`, then we'd subtitute `7` for `num`, giving `rem 7 2 /= 0`.  `rem 7 2` is going to evaluate to `1` (because **7 divided by 2 equals 3, remainder 1**), which leaves us with `1 /= 0`, or in English, "1 is not equal to 0". This is true, so `isOddNumber 7` returns `True`, which is again what we expected.

One question you might have: how does Haskell know to evaluate the `rem` before the `/=`? There is an order of operations, as in math, but it's pretty easy to get it wrong! So if we wanted to be extra-safe, we could use parentheses to make _extra-sure_ that the expression is evaluated the way we want it to. Like so:

```isOddNumber num = (rem num 2) /= 0```

When in doubt, add parentheses!

4. Run the program and test in the REPL to check for yourself. We did it!

## Homework 1: Fahrenheit to Celsius 
Write a function to convert a temperature in Fahrenheit to Celsius.

In the **class program** the function called `ftoc` on **line 13** is wrong! You need to change it by writing an expression that takes a temperature in Fahrenheit, and converts it to Celsius. The mathematical formula to convert Fahrenheit to Celsius is: _The temperature in degrees Fahrenheit minus 32, times 5/9_

For example, if you were doing this on paper: 52 degrees fahrenheit minus 32 is 20. 20 times 5/9 is 11.11. 11.11 Celsius is the answer.  Let me rephase that in more mathy terms:  

```(52°F - 32 == 20). 
20 * (5/9) == 11.11.
11.11°C```

Your task: replace `0.0` on **line 13 of the class program**, on the right side of the = sign, with an expression that does this conversion. You may need to use some parentheses to make sure the operations are evaluated in the proper order, just like in your math class.

If you've done this correctly, all three of the temperature tests should pass when you click or tap "run".  If you encounter an error, try reading it and understanding it. If you still have trouble, bring it up on Google Classroom and we'll work through it with you.

## Homework 2: Is it a Leap Year?
Write an expression to determine if a given year is a leap year.

TThe function called `isLeapYear` on **line 15** (it may have moved lower depending on how long your ftoc function was) takes a year as input (called `yr`), and returns `True` or `False` as output - once again, the function that's there is just a placeholder. You need to replace the placeholder expression (`True`) with an expression that takes the input year and returns `True` or `False` depending on whether `yr` is a leap year.

Calculating leap years is surprisingly tricky! Most people think that "any year that's divided by 4 is a leap year," but there's more to it than that.  The actual definition is:

A year is a leap year if it is evenly divisible by 4, EXCEPT that years evenly divisible by 100 are not leap years, UNLESS those divisible-by-100 leap years are ALSO evenly divisible by 400.

There are a lot of ways to write this function, but many of them use syntax that you haven't been introduced to yet.  I'm going to introduce two more operators that you will probably need to use to write this:

`&&`: pronounced "and", will return `True` if both arguments are `True` but `False` otherwise.  So for example, `(1 == 1) && (2 == 2)` is `True` but `(1 == 1) && (2 == 3)` is `False`

`||`: pronounced "or", will return `True` if ANY of its arguments are `True` but `False` only if both are false.  So `(1 == 5) || (100 == 100)` is `True` but `(1 == 5) || (2 == 5)` is `False`

When you're done, this expression is going to look pretty complicated, but if you take it a step at a time, you should be fine. Remember to use parentheses where appropriate to keep the order of operations straight in your head, just like you do in math class.

If you've done this correctly, all four of the leap year tests should pass when you click or tap "run". If you encounter an error, try reading it and understanding it. If you still have trouble, bring it up on Google Classroom and we'll work through it with you.

**Good luck!**