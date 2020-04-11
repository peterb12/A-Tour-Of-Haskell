# Welcome to Haskell!
## Why Haskell?
Haskell is a computer programming language that is probably unlike any you've used before. Haskell is what we call a _functional_ programming language which means that rather than focusing on executing statements sequentially - although it _can_ do that - the language encourages you to break down problems into what we call _pure functions_ that, given the same arguments, will _always_ give the same answer. This is limiting in some ways, but can make it easier to break down large problems into very small parts that are very easy to put together. Haskell has a reputation as a hard language to learn and master, but once we get some practice with it we'll be able to use it to understand some very fundamental concepts in computer science. Knowing these fundamentals will give you an advantage in every other programming class you take, no matter what language it uses.
## Getting Started
In this lesson we're going to be using the `repl.it` environment to do some Haskell programming,  To get started, go to the website `http://repl.it` and create an account. Once you've done that, please visit the **week 1 class program** `https://repl.it/@peterb/Expressions-and-Functions` and choose `Fork` from the top of the screen to create your own copy.
In particular, you should see a big black window to the right of this text.  This is called the REPL. That stands for _Read-Eval-Print Loop_.  Unlike in  `Code.World`, you can type in things in the REPL, and Haskell will evaluate them immediately.
## How to Take This Class
Have this document open in one browser window, and have another browser window open to the repl.it link open to your copy of the **week 1 class program**, mentioned above.  Whenever this lesson talks about something you can try on repl.it, _stop what you are doing and actually try it_.  At the end of this lesson, you'll have two homework assignments to do. You're on your own for these, but you can ask questions on Google Classroom and we will answer them.
A note on typography: when you see numbers or words that look `like this`, that usually means it is something we either are typing into the REPL, or something the REPL is printing back to us.
One last note: the goal of this class is to teach you about basic computer science patterns, in the context of a weird programming language. When you're done with this class, you will be able to impress people at parties with your amazing knowledge of obscure computer programming languages. There are no grades, and the only reason to do this is that you want to.  In the course of the class, you may find yourself getting stuck on some of the homework assignments. You can get yourself unstuck _any way you want_: ask your teachers, talk to your friends who are taking the class, read a Haskell book. Most of the homework assignments here are very well-known problems. You can undoubtedly do Google searches to find answers to them, and nobody is going to bust you for it. The only thing I suggest is that if you do that, _take your time and try to understand the answer that you're finding_. If you google for the answers in the early weeks without understanding them, you'll be completely lost in the following weeks.
## Expressions
Before anything else, make sure you **go to the class program window and click the "Run" button**.  The examples in this document **will not work if you don't do that.**
Most of the things we type are called _expressions_. An expression is any combination of symbols that can be simplified to a _value_. You can think of a value as any expression that is in its simplest form.
For example, go there now and type `123` and hit enter.  Haskell should reply with
`=> 123`
Which is it's way of saying "the number 123 is the same as the number 123". This may not seem very useful, but it means that if we want to evaluate an expression, we can try it out in the repl.  So if we type `123 + 456`, for example, the REPL will reply
`=> 579`
Which is the value that the expression we typed in simplifies to.
In this lesson, we're going to learn about some of the values and expressions we can use in Haskell, focusing on numbers.  We'll also learn how to tie a name to an expression.  Haskell does a lot more than just math, but we're going to start here to keep it simple. 
## Simple values
We're going to be looking at three of the simplest kinds of values Haskell knows about: Ints, Doubles, and Booleans
An Int is a counting number: `0`, `7`, `781958`, and `(-66)` are all Ints. A Double is a floating point number: `1.5`, `3.33333`, and `7.2` are all Doubles. Unlike the numbers you use in math, Ints and Doubles actually have some limitations, but they won't be relevant for this first lesson. Booleans are the simplest type: `True` and `False` are the onlyboolean values.
In our lesson today we're going to need some simple math to help us, so I'm going to introduce you to some math functions (we'll explain a little more about functions later on.)
The basic functions you'll need for this module are:
`+`: add two numbers. Try typing `66 + 44` in the REPL
`-`: subtract two numbers. `66 - 44`
`*`: multiply two numbers `66 * 44`
`/`: divide two floating point numbers `66 / 44`
`==`: evaluates to `True` if two things are equal, `False` if they are not.
`/=`: evaluates to `True` if two things are not equal, `False` if they are equal.
`rem`: The integer remainder from division.  Type typing `rem 19 5` in the REPL - you should get back `4`: 5 goes into 19 only 3 times (making 15) and 19 - 15 = 4.
You might notice that unlike `+` or `-`, `rem` came _before_ the numbers it was applied to, not in between. You'll see more of this later.
## Naming Expressions
So we see that in Haskell (and in many programming languages), an expression is something that evaluates to a value. This should be familiar to you from your math class. For example, the expression `1 + 5 + 8` evaluates to the value `14`
We can name expressions. Most of the programming you do in Haskell is going to involve naming expressions and combining smaller expressions into larger ones.
On **line 6** of the class program, you should see a line that looks like this:
```fourteen = 14```
Go ahead and type `fourteen` in the REPL, and Haskell should reply with `14`. 
On **line 7** of the class program, you should see:
```complicatedFourteen = 1 + 5 + 8```
and if you type `complicatedFourteen` in the REPL, it will also reply with `14`. So we gave the name `complicatedFourteen` to the expression `1 + 5 + 8`, and Haskell will remember that.  What we name expressions is entirely our choice (although 
they have to start with a lower-case letter.)
As far as Haskell is concerned, all expressions are reduced before they are evaluated. So to Haskell, `fourteen`, `complicatedFourteen`,`14` and `1 + 5 + 8` are all the exact same thing.  If you would like to test this for yourself, go to the REPL and type `fourteen == complicatedFourteen`.  It will reply with `True`.
## Functions
We can also make named expressions that take a single 'argument', and build an expression from that argument. When the function is evaluated the value of the argument is substituted into the main expression and that whole thing is evaluated to get the final value.  We call these things "functions". On **line 8* of the REPL simple function that takes one input.
```plusOne x = x + 1```
If you type `plusOne 5` into the REPL (the capitalization matters!) what you get back is `6`.
Notice the `x` to the left of the `=` sign in the definition of `plusOne`.  We say that when we called `plusOne 5`, x is _bound_ to the argument 5.  So on the right side of the = sign, the expression  becomes "5 + 1", which reduces to 6. This is a little different than the sort of naming we do when writing our expressions and functions, because `plusOne` can be used with all sorts of arguments. If we call `plusOne 10` then x will be bound to 10 for the duraton of that call.  If we call `plusOne 5 + 100 + 200`, then x will be bound to the value `306`.
In most programming languages, we would say that the "5" is an input to the function `plusOne`. We might call it a _parameter_ or an _argument_ to the function. If you've programmed in Python, you're probably used to function arguments beingfed in to a function by being in parentheses, like this:
`plusOne(5)`
In Haskell, all you need to do is put the arguments after the function name:
`plusOne 5`
Another way to phrase this, that you'll see used in a lot of Haskell books, is to say that we are applying the function "plusOne" to the value 5. This is one of the things people find confusing about Haskell at first, but you will get used to it after a while.

We named our argument to the plusOne function "x", but thereis nothing special about that name. We can pick whatever name we want. For example, on **line 9** of the REPL, we have
```sillyPlusOne clownCar = clownCar + 1```
This function is effectively the same as the original plusOne. We just used different names. Haskell mostly doesn't care what names we choose.
## Worked Example: Is It an Odd Number?
Let's say we want a function to determine if a number is an odd number.  This function will take one input (a number) and it will return a boolean - if the function returns `True`, it means the number is odd, and if it returns `False`, it means the number is even.
Let's call our function `isOddNumber`.  On **line 11** of the repl, we have started by
writing it "wrong" so that it says that every number is odd.
```isOddNumber num = True```
If you go to the REPL and type `isOddNumber 2`, it will tell you `True`, or in other words that 2 is odd.  This is obviously wrong!
So we need to replace `True` in our function above with something that actually tells us if a number is odd.  How do we know whether a number is odd or even?  Looking it up, the definition of an odd number is _"Any integer (not a fraction) that cannot be divided exactly by 2"_
When you divide a number evenly, it has no remainder. There's a Haskell function that will tell you if an integer division has a remainder, `rem`.  So if the remainder of a number divided by 2 is anything other than 0, it's odd.
Change the function definition on **line 11** to:
```isOddNumber num = rem num 2```
And then **click run**, and in the REPL try a few tests, such as `isOddNumber 7` and `isOddNumber 100`.  Do you get `True` or `False`?
No!  We're not done yet.  What we get back is the remainder, which in this case is always 0 or 1 - and this isn't what we wanted.  To convert this to a boolean, we need to compare it. There are lots of comparisons in Haskell, but the two we care about right now are:
`==`: are two things equal to each other
`/=`: are tow things not equal to each other.
Let's change **line 11** again. This time, make it say:
```isOddNumber num = rem num 2 /= 0```
run the program and test in the REPL again, as before. We did it!
## Homework 1: Fahrenheit to Celsius 
The function called `ftoc` on **line 13** is wrong! You need to change it by writing an expression that takes a temperature in Fahrenheit, and converts it to Celsius. The formula to convert fahrenheit to celsius is: _The temperature in degrees Fahrenheit minus 32, times 5/9_
For example: 32 degrees fahrenheit minus 32 is 0. 0 times 5/9 is 0. 0 celsius is the answer.
Your task: replace "0.0" in the function definition below, on the right side of the = sign, with an expression that does this conversion. You may need to use some parentheses to make sure the operations are evaluated in the proper order, just like in your math class.
If you've done this correctly, all three of the temperature tests should pass when you click "run".  If you encounter an error, try reading it and understanding it. If you still have trouble, bring it up on Google Classroom and we'll work through it with you.
## Homework 2: Is it a Leap Year?
The function called `isLeapYear` on **line 15** (it may have moved lower depending on how long your ftoc function was) is wrong! You need to replace `True` with a function that takes a year and returns True or False depending on whether the passed in year (named `yr`) is a leap year.
Calculating leap years is surprisingly tricky! Most of think it's just "any year that's divided by 4 is a leap year, but there's more to it than that.  The actual definition is:
A year is a leap year if it is evenly divisible by 4, EXCEPT that years evenly divisible by 100 are not leap years, UNLESS those divisible-by-100 leap years are ALSO evenly divisible by 400.
There are a lot of ways to write this function, but many of them use syntax that you haven't been introduced to yet.  I'm going to introduce two more operators that you will probably need to use to write this:
`&&`: pronounced "and", this returns `True` if both arguments are `True` and `False` otherwise.  So for example, `1 < 5 && 2 < 5` is `True` but `1 < 5 && 100 < 5` is `False`
`||`: pronounced "or", this returns `True` if ANY of its arguments are `True`, and `False` only if both are false.  So `1 < 5 || 100 < 5` is `True` but `100 < 5 || 200 < 5` is `False`
When you're done, this expression is going to look pretty complicated, but if you take it a step at a time, you should be fine. Remember to use parentheses where appropriate to keep the order of operations straight in your head, just like you do in math class.
**Good luck!**