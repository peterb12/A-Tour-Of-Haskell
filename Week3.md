# Week 3 

OK, team, we've gone easy on you so far, but this week we're going to challenge you.  Up until now, all the code you've written has been more or less a single expression.  Sometimes, as in the case of your nucleotide program if, that expression might have been complicated, but it was always just in and out.  This week, we're going to talk about how to do things multiple times. In most programming languages, you do this by _iteration_. In Haskell, and in most functional languages, you'll do this by _recursion_.

## A Short History of Iteration

In the beginning, a computer was a person (often, in the 20th century up until sometime after World War II, a woman) who did math for engineers, with pencil and paper.  When you wanted the computer to do some calculation a number of times, you'd tell her what you wanted in words - "Do step B 7 times, add up the results, and then go on to step C."

Human computers at NASA, 1955: ![Human computers at NASA](https://www.history.com/.image/c_limit%2Ccs_srgb%2Cfl_progressive%2Cq_auto:good%2Cw_686/MTU3ODc4NjA0MDUwMDgxNTAz/image-placeholder-title.jpg)

### Go to this address in memory

Early computers were often programmed in very low-level instructions called machine language, with "assembly language" being a slightly-more human readable version of ths.  Normally the computer would execute one instruction, then go to the memory location 1 position higher and execute the next instruction.  If you wanted to iterate some task, what you'd do is issue a conditional branch or jump instruction whose target was some other memory location.

Here's a very simple example with a made-up assembly language where each instruction takes up 4 bytes (don't type this into your REPL - it won't work!)

```
; Let's print the numbers from 0 through 9 
0000 MOVE 10 Y       ; Put 10 in the Y register
0000 MOVE 0 A        ; Put 0 in the A register
0004 CALL $FDDB      ; Print
0008 INC A           ; Increment (add 1 to) the value in A
0012 SUB Y A X       ; Subtract A from Y, put the result in X
0016 BRZ X 0024      ; If X is 0, jump to memory location 24
0020 JMP 0004        ; If not, jump back to memory location 4
0024 HALT
```

This type of iteration is very prone to mistakes and it's hard to read, as you can see.

### Iteration with statements - "Loops"

As higher-level and better languages were developed, and they usually included special syntax to make iteration easier. For example, here's the same program, written in C. (Again, don't try this in your REPL.)

```
void count_up_to_ten()

for (int x = 0; x < 10; x++) {
    printf("%d", x);
}
```

Or in Python:

```
def count_up_to_ten():
  for x in range(0,10):
    print(x)
```

### But loops have baggage

There's a joke among programmers that goes like this:

> The **two** hardest problems in Computer Science are:
> -Cache invalidation
> -Naming things
> -Off-by-one errors.

And in fact, when I wrote those programs up above, my original plan was to count from 1 to 10!  But I had an off-by-one error, and so I changed the rules of the game to count from 0 to 9, instead. So we have a live example of how iteration "by hand", even with a statement to help us, is hard to do.

Another error that often happens when iterating is if we _change the thing we're iterating on_.  Think about this (admittedly silly) Python example:

```
x = 1000
myList = [1, 2, 3, 4, 5]
for item in myList:
  print(item)
  x = x + 1
  myList.append(x)

```

If you run that code in a Python REPL, what you'll see is that it will run forever.  In this case, we did that on purpose, but it's very easy to make a mistake inside a loop that causes it to run forever.

We call what we did inside that loop, where we added new values to `myList` while we were iterating on it `mutation`.  "Mutate" in computer science just means "change", and to change things isn't necessarily bad - usually it's very useful! - but it can be a source of errors.

Here's something about Haskell that's interesting: Within the space of a given function, _you can never mutate a variable_.  If in a certain part of a Haskell program, I say `x = 123`, then I cannot later say `x = x + 1`.  `x`, in that part of the program, will _always_  be 123.  (There are ways to reuse the same name in different contexts, which we will see today, but this idea of _immutability_ is one that will take some getting used to.)  This fact that variables in Haskell don't vary, is why I prefer to call them "names" or "bindings".

### Recursion

So ideally we would find some way to run "the same" code over and over again, as in our loops, but ideally in a way that is not subject to off-by-one errors, and which doesn't require us to mutate any variables.  The most common way of doing this in functional languages like Haskell is called _recursion_.

Recursion is the process of a function calling itself to solve a similar version of the problem.

I want to start by doing recursion the _wrong_ way.  Just like in the loop case, you _can_ write a function that calls itself in a way that won't help you.  In your repl.it document, you should see this function:

```
infiniteMonkeys = ["monkeys"] ++  infiniteMonkeys
```

This function puts the word "monkeys" in a list, and then adds it to whatever the function `infiniteMonkeys` does. Which is the same thing.

One of the coolest things about Haskell is that it actually allows us to deal with infinite data in a very clever way: if we say "Just give me the first 10 items", it will only calculate the first 10 items on the infinite list.   Therefore, in the REPL we can type:

```
  take 10 infiniteMonkeys
=> ["monkeys","monkeys","monkeys","monkeys","monkeys","monkeys","monkeys","monkeys","monkeys","monkeys"]
```

and it works just fine.  However, if we just type `infiniteMonkeys` in the REPL...well, go ahead and try it.  You'll probably have to reload the page to get it unlocked though.

What we see here is that `infiniteMonkeys` is recursive (because it calls itself), it's not really _usefully_ recursive (because it might never stop running).  Useful recursive functions do their work and eventually finish that work.

Let's write a function that will terminate. I'm going to use a conditional to do this to make clear what's happening, but after that we will use pattern matching for almost all of our recursive functions.

```
someMonkeys :: Int -> [String]

someMonkeys amount = if amount == 0 
                     then [] 
                     else "monkey" : someMonkeys (amount - 1)
```

So, if "amount" is 0, then we just return the empty list - we do NOT keep recursing.  This is called the "base case", and all well-written recursive code has a base case.  Because comparing things to 0 is so easy to remember, it's a very common pattern for recursive code to count _down_ from the number the user gave, rather than up to the number the user gave.

Let's rewrite `someMonkeys` in pattern-matching form.

```
someMonkeysPM :: Int -> [String]

someMonkeysPM 0      = []
someMonkeysPM amount = "monkey" : someMonkeys (amount - 1)
```

(See how much easier that is to read?)

Now we can have as many monkeys as we want.  That's a lot of monkeys.  
![That's a lot of monkeys!](resources/monkeys.png)

#### Worked Example: Factorial

### Recursion and Lists

#### Worked Example: Length of a List

#### Homework 2: Sum a list of integers

#### Homework 3: Product of a list of integers

#### Homework 4: Convert a string of nucleotides

### Higher-order functions

#### Map

#### Filter

#### A mention of "reduce" / foldr.




