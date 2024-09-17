# Learn Programming

```
Computer programming or coding is the composition of sequences of instructions,
called programs, that computers can follow to perform tasks.
```
via [Wikipedia: Computer programming](https://en.wikipedia.org/wiki/Computer_programming)

## Introduction
The financial success of tech companies (and the code monkeys they call "software engineers") has inspired a lot of people to pick up programming either out of curiosity or an interest to break into the industry. Bootcamps and courses, free and paid, as well as community and four-year college degrees all offer paths to build programming skills. Some even choose to forego any structured program and "self-teach" computer science (CS). I want to give a few reality checks on the topic of learning how to program before moving on.

### 1. There is no easy way
Learning to program at _any_ level is just plain hard. People who have programmed for 15 years will have just as much trouble wrestling with new concepts as programmers with 15 minutes of experience. Obviously the older programmer will take on more complex and challenging ideas, but the experience of feeling "too stupid" to understand something is universal across all skill levels.

Successful programmers are A) aware that it will never get easier and B) are patient and kind to themselves as they tackle new concepts. Kind of like training for a race: the running doesn't hurt as you get in better shape; you just do it faster. A programmer's ability to learn harder ideas improves drastically over their career in large part because they develop a stronger tolerance for sitting with the discomfort of not understanding something.

"Being smart" is the asset you'll lean on that affects _what_ your brain is able to reason about and _how quickly_ it can develop the ability to do so. There are very few concepts in the introductory levels of computer science that an adult brain physically _cannot_ reason about. However, there are many concepts in entry-level CS that will take adult brains a long time to understand. The key is to give your brain time to do so.

Good programmers are patient with themselves, aware that developing deep understanding takes time, and are secure in the fact that they'll figure it out _eventually_.

### 2. There is a best way
Contrary to much of the rhetoric on the internet, earning a four-year degree is clearly the most effective and straightforward path to becoming a strong programmer. It's by no means a guaranteed path (I've seen plenty of smart kids drop out of CS programs, but only ever because they gave up). But, it's likely more effective than other routes.

Short of a college degree, surrounding yourself with people who are passionate about programming, excited to help, and learning about it themselves is the best option.

## JavaScript
Let's get started.

JavaScript (JS) is a modern, high-level programming language used extensively on the World Wide Web: ["As of 2023, 98.7% of websites use JavaScript"](https://en.wikipedia.org/wiki/JavaScript). JS uses a [weakly-enforced](https://en.wikipedia.org/wiki/Strong_and_weak_typing), [dynamic](https://en.wikipedia.org/wiki/Type_system#Dynamic_type_checking_and_runtime_type_information) type system. It's a "multi-paradigm" language with support for [event-driven](https://en.wikipedia.org/wiki/Event-driven_programming), [functional](https://en.wikipedia.org/wiki/Functional_programming), and [imperative](https://en.wikipedia.org/wiki/Imperative_programming) programming styles.

In layman's terms, JavaScript is one of the most flexible languages in existence. However, it's not without critics. To quote one of my coworkers when he saw me reading the JavaScript Wikipedia page while writing this:
```
JavaScript: Just say no.
```
Nonetheless, JavaScript is a reasonable place to start learning how to program. (It also happens to be the language our freelance projects use.)

### Running code
As you continue reading, I encourage you to enter any code you see in code snippets into this [online JavaScript compiler](https://www.programiz.com/javascript/online-compiler/). We won't use this compiler for long, but it's a fine place to start.

Modify and run the code to challenge and confirm your assumptions about how the programs work. Experimenting on your own is absolutely critical for learning how to program quickly.

### Comments
"Comments" are a way for programmers to communicate their ideas to other programmers in the code they write without affecting the behavior of the program itself. In JavaScript, comments come in two forms:
```javascript
/* This is a comment which will be ignored by the computer. It has absolutely no
impact on the program's behavior. You'll note that this comment is multiple
lines long. This is called a BLOCK COMMENT. */

// This is also a comment which similarly has no effect on the program's
// behavior. Unlike block comments, every line must start with \\ in order to be
// ignored by the computer. These are called INLINE COMMENTS.
```
I use comments in code snippets to explain what's happening in the program, so pay attention to them. In some comments, you might see something that looks like this:
```javascript
// TODO: <An instruction to do something.>
```
These are called "TODO" comments and, in industry source code, they document something that needs to be changed in the code. In my guides, they represent something I want the reader to do.

Alternatively, you may seem comments that look like this:
```javascript
// TODO(jsnl): <An instruction to do something.>
```
These are reminders to myself to do something (my initials are JSNL). You can ignore these and assume that I forgot to do it or will get around to it later.

As you program, you should develop a habit of leaving reminders for yourself. Being consistent in how you write TODO comments for yourself is extremely important. Consistency means you can search a codebase for all unresolved TODOs assigned to you. For example, at my job, I can find 100% of my TODO comments by searching for "TODO(jsnl)".
```javascript
// TODO(<identifier>):
```
Your `<identifier>` should be unique amongst developers working on your project. It should also be something that others can easily associate with you. `TODO(8x73j4)` is a pretty crummy identifier because its not obviously related to you. Conversely, `TODO(john)` is also bad because there are _a lot_ of people named John. Some identifiers I've seen:
```javascript
jsnl  // Mine.
madrugar  // My brother, Braden's.
jmes  // A friend named James.
```

### Output
A program with no outputs is a useless program. There are many different ways for programs to share their output. Some programs output data across the internet. Some programs output information to your computer screen. Others output signals that control heavy machinery. But all useful programs output _something_.

In JavaScript, the simplest form of program output is printing to the console. Print information to the console is simple. In fact, it's so simple that it's the very first task all programmer's do the first time they begin learning a new language. Here is JavaScript's ["Hello, world" program](https://en.wikipedia.org/wiki/%22Hello,_World!%22_program). ("Hello, world" programs have acquired a legendary status over the past several decades and are culturally significant to programmers.)
```
console.log("Hello, world.");
```
When run, the console shows:
```
Hello, world.
```
### Input
Similar to output, most programs (if not all, but I'm not as confident about this one) are only useful if they can receive input from a user. Again, programs can receive input in a ton of different ways. Keyboards, microphones, the internet, and so on are all examples of input mechanisms. Regardless of how they're received, inputs to the program impact its behavior and the answers the it produces for us.

Collecting input from a user via the command line in JavaScript is also simple:
```javascript
let username = prompt("Username: ");
let password = prompt("Password: ");

console.log("Username is", username, "Password is", password);
```
I _strongly_ encourage you to plug this code into the [online JavaScript compiler](https://www.programiz.com/javascript/online-compiler/). Because this prompts the user for input, you'll have to type your answers into the command line on the right hand side of the page before the program proceeds.

Output:
```
Username: hehe
Password: pass
Username is hehe Password is pass
```

### Variables
Variables are one of the atomic (i.e. smallest) units in practically all programs in all programming languages. A variable is a chunk of the **program**'s **state** (see glossary subsection for **bolded** terms) connected to a name. In other words, variables store data that your program can read and manipulate while it runs.

In JavaScript, you create a variable like so:

```javascript
// Declares a variable called "some_number" with the value 10.
let some_number = 10;
```

The `let` keyword tells the computer that you're declaring a variable. Immediately following the `let` keyword is the variable's name, `some_number`. Finally, you give the variable a value with the `=` operator. `=` is called the "assignment operator" because it _assigns_ a value to a variable. In this case, you've assigned `some_number` the value `10`. It's important to understand that the assignment operator is NOT the same as the "equals sign" in math.

Now we can do interesting things with our variable. (Not _that_ interesting.) Variables, as the name suggests, can _change_.
```javascript
let some_number = 10;

// In plain English, assign the value of `some_number` plus 5 to the variable
// called `some_number`. Not suprisingly, the `+` symbol is called the addition
// operator. It... adds... the values of its two operands (in this case, 
// `some_number` and `5` are its operands).
some_number = some_number + 5;
```
In the code snippet above, I've "incremented" the `some_number` variable by `5`. In theory, `some_number` should contain the value `15`, right? Let's check.
```javascript
console.log(some_number);
```
Output:
```
15
```
Here are some other vaguely interesting things we can do with variables.
```javascript
// Number of days in a calendar year.
let days_in_one_year = 365;

// I'm 23 years old.
let my_age_in_years = 23;

// The backtick `` syntax here lets me inline an expression which can't do with
// the traditional "" string syntax.
// `*` is the multiplication operator. You should be catching the drift by now.
console.log(`I am at least ${days_in_one_year * my_age_in_years} days old.`);

// There are 100 years in 1 century.
let years_per_century = 100;

// `/` is the division operator.
console.log(`I am at least ${my_age_in_years / years_per_century} centuries old.`);
```
Output:
```
I am at least 8395 days old.
I am at least 0.23 centuries old.
```

### Control flow
[Control flow](https://en.wikipedia.org/wiki/Control_flow#:~:text=In%20computer%20science%2C%20control%20flow,from%20a%20declarative%20programming%20language.) is the order in which a program's instructions are executed by the computer. As a programmer, you dictate the program's control flow. There are a few mechanisms available to help you do so.

#### Conditionals
Conditionals are a control flow mechanism that let the programmer outline how the program should behave dependent upon conditions.
```javascript
// TODO: Try running this in the online JS compiler with different values
// for `person_age_in_years` and see what gets printed to console.
let person_age_in_years = 45;

if (person_age_in_years < 16) {
  // If the age is less than 16, this happens.
  console.log("This person can't legally drive.");
} else if (person_age_in_years < 18) {
  // OTHERWISE, if the age is less than 18 (and implicitly >= 16), this happens.
  console.log("This person can drive, but they can't rent a car.");
} else if (person_age_in_years < 25) {
  // OTHERWISE, if the age is less than 25 (and implicitly >= 18), this happens.
  console.log("This person can drive and rent a car, but it costs a lot.");
} else {
  // OTHERWISE, this happens.
  console.log("This person can drive and rent cars for cheap. What a life.");
}
```
Another example if conditional statements uses the `%` operator, called the modulo operator. The modulo operator returns the remainder of dividing its left-hand operand by its right-hand operator.
```javascript
// What does `result` store? What is the remainder of 10 divided by 2?
let result = 10 % 2;

console.log(result);

let other_result = 11 % 2;

console.log(other_result);
```
Output:
```
0
1
```
An interesting property of the modulo operator when its right-hand operator is `2` is that it serves as a way to detect when an integer is even or odd. If the remainder of dividing by `2` is 0, then of course the integer is even. Otherwise, if the remainder is `1`, the integer is odd. (The remainder of a division by `2` can only ever be `1` or `0`. If it were something else, `3` for example, then obviously you've done your division wrong because `2` divides into `3` one more time leaving a remainder of `1`.)

Armed with this knowledge, we can write a program that detects if an integer is even or odd and prints the result to the console.
```javascript
// TODO: Try this with different numbers in the online JS compiler.
let number = 385483;

// In plain English, "if `number` is divisible by 2..."
if (number % 2 == 0) {
  console.log(`${number} is even.`);
} else {  // In plain English, "otherwise..."
  console.log(`${number} is odd.`);
}
```
Output:
```
385483 is odd.
```

#### Loops
Another control flow mechanism is the loop. Loops are used when the program wants to repeat a pattern multiple times. There are two key types of loops in JavaScript: the `for` loop and the `while` loop.

A `for` loop looks like this. (The `++` symbol here is called the "post-fix increment operator" and it's a fancy short hand form of `i = i + 1`. In other words, increment `i` by `1`.)
```javascript
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```
Output:
```
0
1
2
3
4
5
6
7
8
9
```
The structure of a `for` loop is:
```javascript
for (/* initialization */, /* condition */, /* afterthought */) {
  /* action */
}
```
The `initialization` expression is executed exactly one time before the loop begins. Once executed, the `initialization` expression isn't executed again regardless of how many times the loop's `action` takes place (unless the loop is encountered again).

Then, the `condition` expression is evaluated. If the condition expression evalutes to `false`, then the loop terminates. Otherwise, if the `condition` is `true`, the `action` is executed. Finally, the `afterthought` expression is executed. This cycle repeats until the `condition` eventually evaluates to `false`.

An interesting side note is if your `condition` _never_ evaluates to `false`, then your loop will run _forever_. That's almost always not something you want and a _very_ common source of **bugs** for new programmers.

Suppose we'd like to add up the first 1000 natural numbers (natural numbers are defined as all positive integers). In other words, what is `1 + 2 + 3 + 4 + ... + 997 + 998 + 999 + 1000`?
```javascript
// Initialize a variable to hold our sum.
let sum = 0;

// Starting with `i` set to `1`, execute some action until `i` is no longer less
// than or equal to 1000.
for (let i = 1; i <= 1000; i++) {
  sum = sum + i;
}

console.log("The sum of the first 1000 natural numbers is", sum);
```
Output:
```
The sum of the first 1000 natural numbers is 500500
```

The other common type of loop is a `while` loop. The syntax of a `while` loop is much more simple than the `for` loop, but the concept is identical. In fact, anything that can be solved with a `while` loop can also be solved using a `for` loop and vice versa.
```javascript
while (/* condition */) {
  /* action */
}
```

The `while` loops `action` is executed _while_ its `condition` is `true`. If the `condition` is `false`, the loop terminates execution.

Here's a `while` loop that computes the sum of the first 1000 natural numbers just like the `for` loop above.
```javascript
let sum = 0;
let i = 1;

while (i <= 1000) {
  sum = sum + i;
  i++;
}

console.log(sum);
```
Output:
```
500500
```

#### Functions
Finally, arguably the most important of them all, functions are yet another mechanism for structuring control flow of your program. Functions are the key ingredient that lets human programmers ascend from solving goofy little problems like checking if a number is even or odd to achieving truly mind-boggling accomplishments. The value of functions cannot be overstated.

They are the first example in this guide of a concept called [abstraction](https://en.wikipedia.org/wiki/Abstraction_(computer_science)) which has, without _any_ exaggeration, underpinned _every single_ engineering feat for the last several millennia of human history. Pay attention to functions.

A JavaScript function defintion looks like this:
```javascript
function name(/* parameters */) {
  /* body */
}
```

In fact, nearly all modern programming languages define their functions in a manner similar to this.

In C,
```javascript
/* return type */ name(/* parameters */) {
  /* body */
}
```

In Rust,
```rust
fn name(/* params */) -> /* return type */ {
  /* body */
}
```

In Python,
```python
def name("""params"""):
    # body
```

All JS functions (Ok, not _all_, but for the purposes of this guide, assume it is) have a name. Much like how we use human names, programmers use function names to _call_ the function.

Below I define a simple function that prints a message to the console and then call it.
```javascript
function PrintSimpleMessageToConsole() {
  console.log("Hello, this is a simple message for the console.");
}

// Once the function is defined, I can call it!

// This is the syntax for calling my function.
PrintSimpleMessageToConsole();
```
Calling a function tells the computer to execute the function's `body`.

Output:
```
Hello, this is a simple message for the console.
```
Some functions take "parameters". Parameters are inputs that will (presumably) affect the function's behavior or outputs. For example, let's define and call a function that adds three integers together.
```javascript
// Adds the three input parameters together and returns the result.
function AddThreeIntegers(x, y, z) {
  return x + y + z;
}

console.log(AddThreeIntegers(1, 2, 3));
console.log(AddThreeIntegers(483, -3, -89483));
```
Output:
```
6
-89003
```
The `return` keyword tells the computer to _return_ to where the function was called, optionally with a value to replace the function call with. In this case, calls to `AddThreeIntegers` are replaced by whatever the sum of the three integers is.

Functions are so powerful because we can use them to abstract away complicated ideas and implementations. For example, suppose we wanted to count how many of the first 1000 natural numbers are perfect squares (recall that a perfect square is an integer which can be expressed by multiplying another integer by itself. E.g. 2 * 2 = 4, so 4 is a perfect square).

This seems like a pretty challening problem to solve, but if we take a deep breath and break it down into subproblems, it becomes much easier. Presumably, in order to count how many perfect squares are in the first 1000 natural numbers, we'll need a way to check if some number _is_ a perfect square. Let's make that function first.

(As with many programming problems, there are _many_ ways to solve this problem.)

```javascript
function IsPerfectSquare(number) {
  // We need to identify if `number` is a perfect square. Let's just iterate
  // over all natural numbers smaller than `number` and square them to see if we
  // can find the square root of number.

  // First, we have to address what's called an "edge" case. What happens if the
  // `number` is 1?
  if (number == 1) {
    // 1 is a perfect square, of course, so return `true`.
    return true;
  }

  // Now that we've handled the case where `number` == 1, we can safely run this
  // loop. Otherwise, `i` would start as 1 and thus `i < number` would be
  // `false`. The loop would never run and we'd return `false`, lying to the
  // caller of the function by incorrectly claiming that 1 is not a perfect
  // square.
  for (let i = 1; i < number; i++) {
    // Note: the `==` operator is called the equality operator. It serves a very
    // different purpose than the `=` assignment operator. The equality operator
    // returns `true` if its two operands are the same value. Otherwise it
    // returns `false`.
    if (i * i == number) {
      // `i` is the square root of `number`, so `number` is a perfect square!
      return true;
    }
  }

  // We didn't find a square square root between 1 and `number`, so `number`
  // is not a perfect square.
  return false;
}

// Let's test our new function.
console.log(IsPerfectSquare(1));
console.log(IsPerfectSquare(64));
console.log(IsPerfectSquare(295 * 295));
console.log(IsPerfectSquare(47837539));
```
Output:
```
true
true
true
false
```

Perfect! Now that we have this useful `IsPerfectSquare` function, counting how
many perfects square there are seems like a much more simple task.
```javascript
// Counts how many perfect squares are in the first N natural numbers.
function CountPerfectSquaresInTheFirstNNaturalNumbers(n) {
  let count = 0;
  for (let i = 1; i <= n; i++) {
    if (IsPerfectSquare(i)) {
      count++;
    }
  }

  return count;
}

console.log(CountPerfectSquaresInTheFirstNNaturalNumbers(1000));
```
Output:
```
31
```
Apparently there are 31 perfect squares in the range `[1, 1000]`. Who knew? Not me.

Now imagine how complicated the code for our `CountPerfectSquaresInTheFirstNNaturalNumbers` function would have been if we didn't have the `IsPerfectSquare` functon. Probably a lot. By breaking the problem down in smaller, simpler pieces, we were able to come up with a correct solution much more quickly.

Another benefit of functions is that we can _reuse_ them for multiple purposes. What if at some point in the future we want to write a new function that needs to know if a number is a perfect square? Then we can use `IsPerfectSquare` for that too! Similarly, what if we run into a problem that can only be solved by knowing how much perfect squares exist in a range of integers? Well, then we can use our `CountPerfectSquaresInTheFirstNNaturalNumbers` for that too.

Functions support abstraction (hiding away complex implementation details so our brains are free to reason about harder, high-level problems without getting stuck in the weeds) _and_ code reuse (once we've solved the problem once, we never have to solve it again). We can compose functions together to produce more useful functions until, ultimately, one of our funtions is sending a chat message to someone halfway around the world.

### Types
The last concept I want to introduce in this guide is types. "A type system is a logical system comprising a set of rules that assigns a property called a type to ever term." - [Type system Wikipedia](https://en.wikipedia.org/wiki/Type_system)

Every "term" in your programs ("term" is a weird term here, pun intended, so let's just use "variable" instead) will have a type. JavaScript is notorious for its type system because it rarely tells the programmer that they've done something bad. That might seem nice, but just because the compiler doesn't _tell_ you that you've done something wrong doesn't mean you didn't do something wrong!

There are three extremely important types in JavaScript (and several others that we'll get to later). They are:
1. Number
2. String
3. Boolean

In your solutions to the programming challenges and all of the code snippets in this document, every single variable will be assigned one of these types. Here's an example:
```javascript
let a_number = 1234;  // The type of this variable is Number
let a_string = "This is a string!";  // The type of this variable is String
let a_bool = false;  // The type of this variable is Boolean!
```
A Number variable stores, well, a number.

A String variable stores a sequence of 'characters' (i.e. letters and symbols). Strings are used to represent written language in programs as you've seen regularly in this document.

A Boolean variable stores a binary `true` or `false` value.

Each of these types (Number, String, or Boolean) has a set of operations that it supports. Confusingly, some of the operations overlap. For example, you can add two Numbers like this:
```javascript
console.log(4 + 5);
```
Output:
```
9
```
But you can also add two Strings in the same exact way (it's not actually called addition -- it's concatenation):
```javascript
console.log("Hello," + " world!");
```
Output:
```
Hello, world!
```
Surprisingly (to programmers in my field), JavaScript will allow a program like this to run without problems:
```javascript
console.log("Hello, " + 1235);
```
In strongly typed languages, the compiler would reject the program because you're adding a String with a Number which makes no sense. When was the last time you added text to a number? In this regard, JavaScript is weakly typed. It lets you play fast and dirty with the types in your program which can cause subtle and hard-to-find bugs. For example, what do you think will print to console when you run this program?
```javascript
// TODO: Run this program in the online JS compiler.
console.log("100" + 100);
```
In this example, the type mismatch is pretty obvious, but it gets obfuscated when we add variable names, functions, and parameters:
```javascript
// NOTE: This program has a bug! Don't use it for reference if you'd like your code to be correct.
function Add(x, y) {
  return x + y;
}

let bank_account_value = 1205;  // dollars

let new_transaction = prompt("Enter deposit size ($): ");

bank_account_value = Add(bank_account_value, new_transaction);

console.log("New account balance:", bank_account_value);
```
The bug is that we're adding a String and a Number, but the source code doesn't make that immediately clear. On top of that, the JS compiler doesn't _tell_ us that we're doing something wrong. This is the primary drawback of languages like JavaScript. Many other languages are designed, both in syntax and compilation, to make it abundantly clear when the programmer is making a mistake like this.

Type systems are very complex, so the only thing I hope you take way from this section is that as you work on the programming challenges (and any time you're programming), pay close attention to the _types_ of the variables you're using. Remember that every variable must have _some_ type and it _always_ matters if you want your code to be correct. When you write a function, think about what types you're expecting its parameters to have and remember that (or write it down as a comment) when you're using the function in other places.

## Programming challenges
There are two programming challenges associated with the concepts in this document. In each challenge, I outline the possible inputs and what your program should _do_. Other than those two things, the solution is entirely up to you.

Write your solutions in a `.js` file.

### Challenge 1

Prompt the user for an integer via the command line (i.e. use the `prompt` function). Print (to the console) whether the integer has either:

1. One digit.
2. Two digits.
3. Three or more digits.

#### Hints
1. Research the `parseInt` function online.
2. Remember that integers can be positive _and_ negative.

### Challenge 2

Prompt the user for a number of cents (the unit of money). Print how many quarters, dimes, nickels, and pennies are needed for exactly how much the user input using the _least number of coins total_.

#### Examples
```
Input: 25 --> 1 quarter  (e.g. 25 pennies is wrong because it uses more coins.)
Input: 27 --> 1 quarter, 2 pennies
Input: 10 --> 1 dime
```
#### Hints
1. Recall the modulo operator (%).
2. Remember that you can _change_ variables (e.g. perhaps by subtraction).

## Glossary
I use a lot of terms that I don't expect someone who's just starting to program to understand (e.g. weak type system, dynamic, programming "paradigms"). However, there are others that I think are important to learn now which are listed below.

### Program
A series of instructions consumed by a computer to perform a task.

### State
The remembered information in a program typically stored in variables. 

### Bug
A behavior exhibited by a program while running that is incorrect attributed to an implementation error in some part of the software.

### Variable
An entity in a program that has a _name_ and stores a piece of the program's state.

### Function
A bundle of instructions packaged together with a name that can be reused in several places throughout the program.

## People
The "Grass Touchers LLC" Discord server is home to many friendly and talented people that are passionate about programming (or video games).

Here are just a few who are around to talk about programming and excited to answer questions.

### Braden (madrugar)
Braden is my brother and a senior studying Computer Science at the Rochester Institute of Technology. He's interned as a software engineer at Bentley Systems, Datto, and SpaceX.

### James (bridge_)
James and I graduated from the Tufts School of Engineering together where we both studied Computer Science. James just finished his Master's degree in CS at Northwestern University. He interned at Google as a software engineer last summer and at Micron Technologies the summer before.

### Max (mgreenw)
Max is a veteran web developer who also studied CS at Tufts but graduated several years before me (I believe in Dec 2018). He's worked as a software engineer at several companies including recently directing engineering at a small start up. Certainly our resident JavaScript expert.
