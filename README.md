# Module 6: Introduction to Functions

In this module, we'll explore how to use **functions** in R to perform advanced capabilities and actually ask questions about data. After considering a function in an abstract sense, we'll look at using built-in R functions, accessing additional functions by loading R packages, and writing our own functions.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

**Contents**

- [Resources](#resources)
- [What are functions?](#what-are-functions)
- [Built-in R Functions](#built-in-r-functions)
- [Loading Functions](#loading-functions)
- [Writing functions](#writing-functions)
- [Conditional Statements](#conditional-statements)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Resources
- [R Function Cheatsheet](https://cran.r-project.org/doc/contrib/Short-refcard.pdf)
- [User Defined R Functions](http://www.statmethods.net/management/userfunctions.html)

## What are functions?
In a broad sense, a **function** is a named sequence of instructions (lines of code) that you may want to perform one or more times throughout a program. They provide a way of _encapsulating_ multiple instructions into a single "unit" that can be used in a variety of different contexts. So rather than needing to repeatedly write down all the individual instructions for "make a sandwich" every time you're hungry, you can define a `MakeSandwich()` function once and then just **call** (execute) that function when you want to perform those steps.

In addition to grouping instructions, functions in programming languages like R also tend to follow the mathematical definition of functions, which is a set of operations (instructions!) that are performed on some **inputs** and lead to some **outputs**. Functions inputs are called **arguments** or **parameters**, and we say that these arguments are **passed** to a function (like a football). We say that a function then **returns** an ouput for us to use.

### R Function Syntax
R functions are referred to by name (technically they are values like any other variable). As in many programming languages, we **call** a function by writing the name of the function followed immediately (no space) by parentheses `()`. Inside the parentheses, we put the **arguments** (inputs) to the function separated by commas. Thus computer functions look just like mathematical functions, but with names longer than `f()`.

```r
# call the print() function, pass it "Hello world" value as an argument
print("Hello world")  # "Hello world"

# call the sqrt() function, passing it 25 as an argument
sqrt(25)  # 5, square root of 25

# call the min() function, pass it 1, 6/8, AND 4/3 as arguments
# this is an example of a function that takes multiple args
min(1, 6/8, 4/3)  # 0.75, (6/8 is the smallest value)
```

  - _Note:_ To keep functions and variables distinct, I try to always include empty parentheses `()` when referring to a function name. This does not mean that the function takes no arguments, it is just a useful shorthand for indicating that something is a function.

If you call any of these functions interactively, R will display the **returned value** (the output) in the console. However, the computer is not able to "read" what is written out in the console&mdash;that's for humans to view! If we want the computer to be able to _use_ a returned value, we will need to give that value a name so that the computer can refer to it. That is, we need to store the returned value in a variable:

```r
# store min value in smallest.number variable
smallest.number <- min(1, 6/8, 4/3)

# we can then use the variable as normal, such as for a comparison
min.is.big <- smallest.number > 1  # FALSE

# we can also use functions directly when storing to variables
phi <- .5 + sqrt(5)/2  # 1.618...

# we can even pass the result of a function as an argument to another!
# watch out for where the parentheses close!
print(min(1.5, sqrt(3)))  # prints 1.5
```

## Built-in R Functions
As you may have noticed, R comes with a large number of functions that are built into the language. In the above example, we used the `print()` function to print a value to the console, the `min()` function to find the smallest number among the arguments, and the `sqrt()` function to take the square root of a number. Here is a _very_ limited list of functions you can experiment with (or see a few more [here](http://www.statmethods.net/management/functions.html)).

| Function Name | Description | Example |
| --- | --- |  --- |
| `sum(a,b,...)`  | Calculates the sum of all input values  | `sum(1, 5)` returns `6`|
| `round(x,digits)` | Rounds the first argument to the given number of digits | `round(3.1415, 3)` returns `3.142` |
| `toupper(str)`  | Returns the characters in uppercase  | `toupper("hi there")` returns `"HI THERE"` |
| `paste(a,b,...)` | _Concatenate_ (combine) characters into one value | `paste("hi", "there")` returns `"hi there"` |
| `nchar(str)` | Counts the number of characters in a string | `nchar("hi there")` returns `8` (space is a character!) |
| `c(a,b,...)` | _Concatenate_ (combine) multiple items into a _vector_ (see [module-7](https://github.com/info201-w17/module7-vectors)) | `c(1, 2)` returns `1, 2` |
| `seq(a,b)`  | Return a sequence of numbers from a to b  | `seq(1, 5)` returns `1, 2, 3, 4, 5` |

To learn more about any individual function, look them up in the R documentation by using running the `?FunctionName` account as described in the last module:

> You can also look up help by using the `help()` function (e.g., `help(print)` will look up information on the `print()` function, just like `?print` does). There is also an `example()` function you can call to see examples of a function in action (e.g., `example(print)`). This will be more important in the next module!

**Important** "Knowing" how to program in a language is to some extent simply "knowing" what provided functions are available in that language. Thus you should look around and become familiar with this functions... but _do not_ feel that you need to memorize them! It's enough to simply be aware "oh yeah, there was a function that sums up numbers", and then be able to look up the name and argument for that function.


## Loading Functions
Although R comes with lots of built-in functions, you can always use more functions. **Packages** are additional sets of R functions that are written and published by the R community. Because many R users encounter the same data management / data analysis challenges, programmers are able to benefit from the work of others (this is the amazing thing about the open-source community&mdash;people solve problems and then make those solutions available to others!) R packages **do not** ship with the R software by default, and need to be downloaded (once) and loaded into your program each time you wish to use them. While this may seem cumbersome, the R software would be huge and slow if you had to install and load _all_ available packages to use it.

Luckily, it is quite simple to install and load R packages from within R! To do so, you'll need to use the _built-in_ R functions `install.packages` and `library`. Here's an example of installing and loading the `stringr` package (which contains more handy functions for working with character strings):

```r
# Install the `stringr` package. Only needs to be done once on your machine
install.packages("stringr")

# Load the package (tell R functions are available for use)
library("stringr") # quotes optional here
```

- Note that when you load a package, you may receive a warning message about the package being built under a previous version of R. In all likelihood this shouldn't cause a problem, but you should pay attention to the details of the messages and keep them in mind (especially if you start getting unexpected errors).

After loading the package with the `library` function, you have access to functions that were written as part of that package (see [the documentation](https://cran.r-project.org/web/packages/stringr/stringr.pdf) for a list of functions included with the `stringr` library).


## Writing functions
Even more exciting than loading other peoples' functions is writing your own. Any time that you have a task that you may repeat throughout a script&mdash;or you simply want to organize your thinking&mdash;it's good practice to write a function to perform that task. This will limit repetition and reduce the likelihood of error... as well as make things easier to read and understand.

Functions are named like any othe variable, so we use the _assignment operator_ (**`<-`**) to store a new `function` in a variable. It's [best practice ](https://google.github.io/styleguide/Rguide.xml#functiondefinition) assign functions names in _CamelCase_ without any periods (`.`) in the name. This helps distinguish functions from other variables.

The best way to understand the syntax for defining a function is to look at an example:

```r
# A function named `MakeFullName` that takes two arguments
# and returns the "full name" made from them
MakeFullName <- function(first.name, last.name) {
  # Function body: perform tasks in here
  full.name <- paste(first.name, last.name)

  # Return: what you want the function to output
  return(full.name)
}

# Call the MakeFullName function with the values "Alice" and "Kim"
my.name <- MakeFullName("Alice","Kim")  # "Alice Kim"
```

Functions have a couple of pieces to them:

- **Arguments**: the data assigned to the function variable uses the syntax `function(...)` to indicate that you're creating a function (as opposed to a number or character string). The values put betweeen the parentheses are variables that _will contain_ the values passed in as **arguments**. For example, when we call `MakeFullName("Alice","Kim")`, the value of the first argument (`"Alice"`) will be assigned to the first variable (`first.name`), and the value of the second argument (`"Kim"`) will be assigned to the second variable (`last.name`).

  Importantly, we could have made the argument names anything we wanted (`name.first`, `given.name`, etc.), just as long as we then use _that variable name_ to refer to the argument while inside the function. Moreover, these argument variable names _only apply_ while inside the function. You can think of them like "nicknames" for the values. The variables `first.name`, `last.name`, and `full.name` only exist within this particular function.

- **Body**: The body of the function is a **block** of code that falls between curly braces **`{}`** (curly braces are called a "block"). Note that cleanest style is to put the opening `{` immediately after the arguments list, and the closing `}` on its own line.

  The function body specifies all the instructions (lines of code) that your function will perform. A function can contain as many lines of code as you want&mdash;you'll usually want more than 1 to make it worth while, but if you have more than 20 you might want to break it up into separate functions. You can use the argument variables in here, create new variables, call other functions... basically any code that you would write outside of a function can be written inside of one as well!

- **Return value**: You can specify what output a function produces by calling the `return()` function and passing that the value that you wish _your function_ to return (output). The `return()` function will execute instructions that end the current function and _return_ the flow of code execution to whereever this function was called from. Note that even though we returned a variable called `full.name`, that variable was _local_ to the function and so doesn't exist outside of it; thus we have to take the returned value and assign it to a new variable (as with `name <- MakeFullName("Alice","Kim")`).

  Because the `return()` call exits the function, it is usually the last line of code in the function.

We can call (execute) a function we defined the same way we called built-in functions. When we do so, R will take the **arguments** we passed in (e.g., `"Alice"` and `"Kim"`) and assign them to the _argument variables_. Then it execute each line of code in the **function body** one at a time. When it gets to the `return()` call, it will end the function and return the given value, which can then be assigned to a different variable.

For practice writing basic functions, see [exercise-1](exercise-1).


## Conditional Statements
Functions are a way to organize and control the flow of execution (e.g., what lines of code get run in what order). In R, as in other languages, we have one other way of controlling program flow, and that is by specifying different instructions that can be run based on a different set of conditions. **Conditional statements** allow us to specify different chunks of code to run when given different contexts, which is often valuable within functions.

In an abstract sense, an conditional statement is saying:

```
IF something is true
  do some lines of code
OTHERWISE
  do some other lines of code
```

In R, we write these conditional statements using the keywords **`if`** and **`else`** and the following syntax:

```r
if(condition){
  # lines of code to run if condition is TRUE
} else {
  # lines of code to run if condition is FALSE
}
```

(Note that the the `else` needs to be on the same line as the closing `}` of the `if` block. It is also possible to omit the `else` and its block).

The `condition` can be any variable or expression that resolves to a logical value (`TRUE` or `FALSE`). Thus both of the below conditional statements are valid:

```r
porridge.temp <- 115  # in degrees F
if(porridge.temp > 120) {
  print("This porridge is too hot!")
}

too.cold <- porridge.temp < 70
if(too.cold) {  # a logical value
  print("This porridge is too cold!")
}
```

For practice writing conditional statements in functions, see [exercise-2](exercise-2).
