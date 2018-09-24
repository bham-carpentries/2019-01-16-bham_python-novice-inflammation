---
title: "Operators"
teaching: 10
exercises: 10
questions:
- "How do I manipulate objects and data in Python?"
objectives:
- "Show how to perform operations on python objects"
- "Introduce the basic operators"
keypoints:
- "Operators are used to perform actions on objects"
- "They have different behaviour depending on the objects that are being acted on"
- "There is nothing special about operators - they are just shorthand for running other bits of code"
---

We now know how to create variables to store our data but we don't know how to manipulate them
at the moment. This is done using 'Operators'.

## Basic Operators

Operators are symbols that perform specific operations on one or more objects. A subset of these
are the arithmetic operators you're already familiar with:

* Multiplication: `a * b`
* Addition: `a + b`
* Subtraction: `a - b` 
* Division: `a / b`

For example, `a+b` is the addition operator being applied to the objects pointed at by the variables
`a` and `b`.
What operators you can use depends on what the objects you're applying them to are so some
things won't work - you can't divide two strings or add a string and a number for example.

> ## Under the Hood
>
> It's worth noting that operators in Python are nothing 'special' - they can be thought of
> as basically shorthand for other bits of code. These can range from simple things like
> numerical addition/subtraction/etc. to concatenation (combining) of two strings or performing
> the scalar product on matrices. 
{: .callout}

## Going further

As well as these basic operators, there are also more language specific ones:

* Assignment: `a = b`
* Addition/Subtraction and assignment: `a += b`, `a -= b`
* Exponent: `a ** b` ( e.g. `10**3 = 1000` )
* Modulus: `%` (e.g. `9 % 4 = 1`)
* Floor Division: `a // b` (e.g. `9 // 4 = 2`) 
* Subscript/Array: `[]`

You can see that assignment (`=`) which you've already met is just another
operator - it will attempt to assign the object or value on the right to the variable on the left.
Another of these you will use a lot is the Subscript/Array operator (`[]`). This is generally used to access elements of
collections like getting a single character from a string, e.g.

~~~
my_str = "TESTING"
first = my_str[0]
third = my_str[2]
~~~
{: .language-python}

> ## Check Your Understanding
>
> What values do the variables `mass` and `age` have after each statement in the following program?
> Test your answers by executing the commands.
>
> ~~~
> mass = 47.5
> age = 122
> mass = mass * 2.0
> age = age - 20
> ~~~
> {: .language-python}
{: .challenge}

> ## Challenge
>
> If you assign `a = 123`,
> what happens if you try to get the second digit of `a` via `a[1]`?
>
> > ## Solution
> > Numbers are not stored in the written representation,
> > so they can't be treated like strings.
> >
> > ~~~
> > a = 123
> > print(a[1])
> > ~~~
> > {: .python}
> > ~~~
> > TypeError: 'int' object is not subscriptable
> > ~~~
> > {: .error}
> > 
> > If you had a string then this would have worked as expected:
> > ~~~
> > a = "123"
> > print(a[1])
> > ~~~
> > {: .python}
> > ~~~
> > 2
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}


> ## Using operators in Python
> 
> Now you know how operators work, try to do the following:
> 1. Create two variables, one a float and the other an integer
> 2. Print the product of these
> 3. What happens when you divide a float and an int?
> 4. What happens when you divide two ints?
> 5. Create a string variable and output various letters from it
{: .challenge}


> ## In-place Operators
> 
> What is the value of `a` and `b` after the following code is executed? Try it by running this code yourself
> ~~~
> a = 10
> b = 20
> b += a
> print(a, b)
> ~~~
> {: .language-python}
> > ## Solution
> > ~~~
> > 10 30
> > ~~~
> > {: .output}
> > The addition and assignment operator (`b += a`) is shorthand for `b = b + a` so in this case, the
> > value of `a` is added to `b` but `a` is left unchanged.
> {: .solution}
{: .challenge}