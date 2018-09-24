---
title: "Types, Objects, Values and Variables"
teaching: 20
exercises: 5
questions:
- "How can I store and access basic information in Python?"
objectives:
- "Explain what Types, Objects, Values and Variables are with respect to Python"
- "Introduce the basic variable types"
- "Show how to initialise, access and change variables"
keypoints:
- "Types are how python should interpret data in a memory location ('object') and what operations can be performed by it"
- "Objects are defined areas of memory that holds data ('Values') associated with a Type"
- "Values are the actual data/bits in memory interpreted by the 'Type'"
- "Variables are a flag or name for a particular area of memory ('Object')"
- "Variable names must only contain letters, numbers and underscores. They are case-sensitive."
- "You can assign values to a variable using the `=` operator"
- "The basic (non collection) data types are: integers, floating point numbers, strings and booleans."
---

Now we have learnt the technical aspects of using the Python interpreter, we can
move on to the basics of programming using it. The first thing we'll learn about is
how Python stores and interprets information.

## Types, Objects, Values and Variables

Any Python interpreter can be used as a calculator:
~~~
3 + 5 * 4
~~~
{: .language-python}
~~~
23
~~~
{: .output}

This is great but not very interesting.
To do anything useful with data, we need to assign its value to a _variable_ otherwise
we'd have to write the whole analysis as one long calculation.

But what is a variable? And what is it's relation to how Python organises the information you
give it? This is all covered by four terms:

* Types – How to interpret data in a memory location ('object') and what operations can be performed by it
* Object – Defined area of memory that holds the data ('values') associated with a type
* Value – Actual data/bits in memory interpreted by the 'type' 
* Variable – A flag or name of an area of memory ('object')

This probably seems quite abstract but it can be very useful to know the difference
as we progress!

Another way of looking at this is in terms of a physical object like a laptop:

![A Generic laptop](../fig/laptop.jpg)

In this case, the **Object** is the physical laptop sitting on the desk, 
the **Type** of the object is 'Laptop', the **Value** is the bits and pieces that actually make
up the laptop (forming a MacBook in this case) and finally the **Variable** would be who's laptop 
it was, e.g. Fred's laptop.

## Assigning Variables

In Python, we can [assign]({{ page.root }}/reference/#assign) an object or value to a
[variable]({{ page.root }}/reference/#variable), using the equals sign `=`.
For example, to assign value `60` to a variable `weight_kg`, we would execute:

~~~
weight_kg = 60
~~~
{: .language-python}

From now on, whenever we use `weight_kg`, Python will refer back to the **Object** it points to
(in this case an integer with value '60') and effectively substitute it's value where the variable is. 

> ## What's in a name?
>
> In Python, variable names:
>
> - can include letters, digits, and underscores
> - cannot start with a digit
> - are [case sensitive]({{ page.root }}/reference/#case-sensitive).
>
>This means that, for example:
> - `weight0` is a valid variable name, whereas `0weight` is not
> - `weight` and `Weight` are different variables
{: .callout}

When you run this code to create a variable, Python performs the following actions:
* create space for the integer object in the computer's memory
* mark it as being of type 'Integer'
* assign the value '60' to it
* label it with 'weight_kg'.

This all happens each time you create a new variable, so if you ran the following code:

~~~
a = 43
b = 76.2
c = "Hello"
~~~
{: .language-python}

What happens in the computer's memory can be shown like this:

![Schematic computer memory](../fig/memory-schematic.png)

where the dark grey boxes are elements of the computer's memory, the light grey boxes 
assigned memory with
the values inside, the coloured outline is the type and the flags indicate where each variable points to.

## Types of data
Python knows various types of data. The four basic ones (not including the collection types) are:

* integer numbers - whole numbers
* floating point numbers - decimal numbers
* strings - collections of letters
* booleans - a binary type that can only have the values `True` and `False`

In the example above, variable `weight_kg` has an integer value of `60`.
To create a variable with a floating point value, we can execute:

~~~
weight_kg = 60.0
~~~
{: .language-python}

And to create a string (as for `c` above) we simply have to add single or double quotes around some text, for example:

~~~
weight_kg_text = "weight in kilograms:"
~~~
{: .language-python}

> ## Single or Double quotes
>
> To indicate a string, you need to enclose it in matching single or double quotes. Python will accept both
> but it's generally a good idea to use double quotes as if you tried to assign a string with an apostrope
> in it using single quotes, you will get an error. Give this a try:
>
> ~~~
> msg = 'All's well'
> ~~~
> {: .language-python}
>
> As you are much more likely to have apostrope's in a string than double quotes, it's best to stick with
> double quotes for strings.
{: .callout}

## Using Variables in Python

To display the value of a variable to the screen in Python, we can use the `print` function as we did before:

~~~
print(weight_kg)
~~~
{: .language-python}

~~~
60
~~~
{: .output}

Not that we can display multiple things at once using only one `print` command:

~~~
print(weight_kg_text, weight_kg)
~~~
{: .language-python}
~~~
weight in kilograms: 60
~~~
{: .output}

To change the value of the `weight_kg` variable, we have to
**assign** `weight_kg` a new value using the equals `=` sign:

~~~
weight_kg = 65.0
print('weight in kilograms is now:', weight_kg)
~~~
{: .language-python}

~~~
weight in kilograms is now: 65.0
~~~
{: .output}

> ## The Difference between Strings and Variables
>
> Which of the following would you use to assign the value of the `test1` variable to the `test2` variable? 
> Note the difference between a string (indicated
> by quotes) and a variable name (without quotes).
>
> 1. `test2 = "test1"`
> 2. `test2 = test1`
> 3. `"test2" = test1`
> 3. `"test2" = "test1"`
>
> > ## Solution
> > 1. No. This will assign the value `"test1"` to the `test2` variable, **not** the value of the `test1` variable
> > 2. Yes
> > 3. No. This will raise an error as it is trying to change the value of a constant string (`"test2"`)
> > 4. No. Same as for 3
> {: .solution}
{: .challenge}

> ## Choosing a Name
>
> Which is a better variable name, `m`, `min`, or `minutes`?
> Why?
> Hint: think about which code you would rather inherit
> from someone who is leaving the lab:
>
> 1. `ts = m * 60 + s`
> 2. `tot_sec = min * 60 + sec`
> 3. `total_seconds = minutes * 60 + seconds`
>
> > ## Solution
> >
> > `minutes` is better because `min` might mean something like "minimum"
> > (and actually does in Python, but we haven't seen that yet).
> {: .solution}
{: .challenge}

> ## Give it a try
> 
> Have a go at creating some variables of the three basic types we've been looking at: Integer, Floating Point, Boolean and String.
> Print each out using the `print` function.
{: .challenge}