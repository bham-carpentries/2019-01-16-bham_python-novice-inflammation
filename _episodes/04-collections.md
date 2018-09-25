---
title: Storing Multiple Values in Collections
teaching: 20
exercises: 20
questions:
- "How can I store many values together?"
objectives:
- "Explain what a list and a dictionary is."
- "Create and index lists of simple values."
- "Change the values of individual elements"
- "Append values to an existing list"
- "Reorder and slice list elements"
- "Create and manipulate nested lists"
- "Create and manipulate dictionaries"
- "Explain what key:pair mapping is"
keypoints:
- "`[value1, value2, value3, ...]` creates a list."
- "Lists can contain any Python object, including lists (i.e., list of lists)."
- "Lists are indexed and sliced with square brackets (e.g., list[0] and
list[2:9]), in the same way as strings and arrays."
- "Lists are mutable (i.e., their values can be changed in place)."
- "Strings are immutable (i.e., the characters in them cannot be changed)."
- "`{ key1:value1, key2:value2, ...}` creates a dictionary"
- "The keys are used to reference and retrieve the values"
- "As with lists, they are mutable - their values can be changed in place"
---

We have learnt how to store single bits of data in variables but what happens when we have several
bits of data that are associated with each other and need to be stored together? For example, 
a vector, array or list of names? For this we can use the built-in collection types of `list`
and `dict` (short for dictionary).

## Storing Multiple Values in a List

We create a list by putting values inside square brackets and separating the values with commas:

~~~
odds = [1, 3, 5, 7]
print('odds are:', odds)
~~~
{: .language-python}

~~~
odds are: [1, 3, 5, 7]
~~~
{: .output}

We select individual elements from lists by indexing them just as we did for strings:

~~~
print('first and third:', odds[0], odds[2])
~~~
{: .language-python}

~~~
first and third: 1 5
~~~
{: .output}

> ## Starting From Zero
>
> It's very important to remember that Python (like many other languages) indexes it's collections
> from zero rather than one. In other words, the first element of list is given by index `0`, the
> second by index `1`, etc. Therefore the last element is given by the number of elements in the
> list minus one, e.g. for the example above, the last element is `odds[3]`.
> 
> Programming languages like Fortran, MATLAB and R start counting at 1
> because that's what human beings have done for thousands of years.
> Languages in the C family (including C++, Java, Perl, and Python) count from 0
> because it represents an offset from the first value in the array (the second
> value is offset by one index from the first value). This is closer to the way
> that computers represent arrays (if you are interested in the historical
> reasons behind counting indices from zero, you can read
> [Mike Hoye's blog post](http://exple.tive.org/blarg/2013/10/22/citation-needed/)).
{: .callout}

You can use negative indices to access elements from the end of the list as well, so the last
element would be `-1`, the penultimate `-2`, etc.:

~~~
print('first and last:', odds[0], odds[-1])
~~~
{: .language-python}

~~~
first and last: 1 7
~~~
{: .output}

You may have noticed there is a significant similarity between lists and strings and
in fact a lot of the things you can do with strings you can also do with lists. However, 
there is one important difference between the two: we can change the values in a list,
but we cannot change individual characters in a string.
For example:

~~~
names = ['Curie', 'Darwing', 'Turing']  # typo in Darwin's name
print('names is originally:', names)
names[1] = 'Darwin'  # correct the name
print('final value of names:', names)
~~~
{: .language-python}

~~~
names is originally: ['Curie', 'Darwing', 'Turing']
final value of names: ['Curie', 'Darwin', 'Turing']
~~~
{: .output}

works, but:

~~~
name = 'Darwin'
name[0] = 'd'
~~~
{: .language-python}

~~~
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-8-220df48aeb2e> in <module>()
      1 name = 'Darwin'
----> 2 name[0] = 'd'

TypeError: 'str' object does not support item assignment
~~~
{: .error}

does not.

> ## Ch-Ch-Ch-Ch-Changes
>
> Data which can be modified in place is called [mutable]({{ page.root }}/reference/#mutable),
> while data which cannot be modified is called [immutable]({{ page.root }}/reference/#immutable).
> Strings and numbers are immutable. This does not mean that variables with string or number values
> are constants, but when we want to change the value of a string or number variable, we can only
> replace the old value with a completely new value.
>
> Lists and arrays, on the other hand, are mutable: we can modify them after they have been
> created. We can change individual elements, append new elements, or reorder the whole list. For
> some operations, like sorting, we can choose whether to use a function that modifies the data
> in-place or a function that returns a modified copy and leaves the original unchanged.
>
{: .callout}

> ## Nested Lists
> Since lists can contain any Python variable, it can even contain other lists.
>
> For example, we could represent the products in the shelves of a small grocery shop:
>
> ~~~
> x = [['pepper', 'zucchini', 'onion'],
>      ['cabbage', 'lettuce', 'garlic'],
>      ['apple', 'pear', 'banana']]
> ~~~
> {: .language-python}
>
> Here is a visual example of how indexing a list of lists `x` works:
>
> [![The first element of a list.
> Adapted from @hadleywickham.](../fig/indexing_lists_python.png)][hadleywickham-tweet]
>
> Using the previously declared list `x`, these would be the results of the
> index operations shown in the image:
>
> ~~~
> print([x[0]])
> ~~~
> {: .language-python}
>
> ~~~
> [['pepper', 'zucchini', 'onion']]
> ~~~
> {: .output}
>
> ~~~
> print(x[0])
> ~~~
> {: .language-python}
>
> ~~~
> ['pepper', 'zucchini', 'onion']
> ~~~
> {: .output}
>
> ~~~
> print(x[0][0])
> ~~~
> {: .language-python}
>
> ~~~
> 'pepper'
> ~~~
> {: .output}
>
> Thanks to [Hadley Wickham][hadleywickham-tweet]
> for the image above.
{: .callout}

> ## Heterogeneous Lists
> Lists in Python can contain elements of different types. Example:
> ~~~
> sample_ages = [10, 12.5, 'Unknown']
> ~~~
{: .callout}

> ## Calling Functions on Objects
> 
> The `list`, `dict` and `string` types are actually more complicated objects than basic numbers
> and therefore have certain built-in bits of code that you can run on them. This is done through
> a [function call]({{ page.root }}/reference/#function-call). For example:
> 
> ~~~
> my_str.find("a")
> ~~~
> {: .language-python}
>
> This code asks Python to run the [function]({{ page.root }}/reference/#function) `find` **on**
> the object pointed at by the variable `my_str`. This [dotted notation]({{ page.root }}/reference/#dotted-notation)
> is used everywhere in Python: the thing that appears before the dot contains the thing that
> appears after.
> `find` has one [parameter]({{ page.root }}/reference/#parameter): the sub-string to look 
> for in the string
> This is sent to the code referened by the `find` name (the **function**) and after this code
> is run, it return the index of the sub-string (if found) and then continues. You can also have
> functions that don't need any input, for example `my_str.split()`.
{: .callout}

There are many ways to change the contents of lists besides assigning new values to individual elements:

~~~
odds.append(11)
print('odds after adding a value:', odds)
~~~
{: .language-python}

~~~
odds after adding a value: [1, 3, 5, 7, 11]
~~~
{: .output}

~~~
del odds[0]
print('odds after removing the first element:', odds)
~~~
{: .language-python}

~~~
odds after removing the first element: [3, 5, 7, 11]
~~~
{: .output}

~~~
odds.reverse()
print('odds after reversing:', odds)
~~~
{: .language-python}

~~~
odds after reversing: [11, 7, 5, 3]
~~~
{: .output}

While modifying in place, it is useful to remember that Python treats lists in a slightly
counter-intuitive way.

If we make a list and (attempt to) copy it then modify in place, we can cause all sorts of trouble:

~~~
odds = [1, 3, 5, 7]
primes = odds
primes.append(2)
print('primes:', primes)
print('odds:', odds)
~~~
{: .language-python}

~~~
primes: [1, 3, 5, 7, 2]
odds: [1, 3, 5, 7, 2]
~~~
{: .output}

This is because Python stores a list in memory, and then can use multiple variables names
(or 'labels') to refer to the
same list. If all we want to do is copy a (simple) list, we can use the `list` function, so we do
not modify a list we did not mean to:

~~~
odds = [1, 3, 5, 7]
primes = list(odds)
primes.append(2)
print('primes:', primes)
print('odds:', odds)
~~~
{: .language-python}

~~~
primes: [1, 3, 5, 7, 2]
odds: [1, 3, 5, 7]
~~~
{: .output}

This is different from how variables worked in lesson 2 when you were storing (immutable)
numbers and strings. By default, Python will apply another variable name to the same object
rather than copying it if it's not one of the basic immutable types.

### Slicing Lists

Subsets of lists and strings can be accessed by specifying ranges of values in the square
brackets using a colon to separate the first and last+1 index required.
This is commonly referred to as "slicing" the list/string.

~~~
binomial_name = "Drosophila melanogaster"
group = binomial_name[0:10]
print("group:", group)

species = binomial_name[11:24]
print("species:", species)

chromosomes = ["X", "Y", "2", "3", "4"]
autosomes = chromosomes[2:5]
print("autosomes:", autosomes)

last = chromosomes[-1]
print("last:", last)
~~~
{: .language-python}

~~~
group: Drosophila
species: melanogaster
autosomes: ["2", "3", "4"]
last: 4
~~~
{: .output}

If you want to take a slice from the beginning of a sequence, you can omit the first index in the
range:

~~~
date = "Monday 4 January 2016"
day = date[0:6]
print("Using 0 to begin range:", day)
day = date[:6]
print("Omitting beginning index:", day)
~~~
{: .language-python}

~~~
Using 0 to begin range: Monday
Omitting beginning index: Monday
~~~
{: .output}

And similarly, you can omit the ending index in the range to take a slice to the very end of the
sequence:

~~~
months = ["jan", "feb", "mar", "apr", "may", "jun", "jul", "aug", "sep", "oct", "nov", "dec"]
sond = months[8:12]
print("With known last position:", sond)
sond = months[8:len(months)]
print("Using len() to get last entry:", sond)
sond = months[8:]
print("Omitting ending index:", sond)
~~~
{: .language-python}

~~~
With known last position: ["sep", "oct", "nov", "dec"]
Using len() to get last entry: ["sep", "oct", "nov", "dec"]
Omitting ending index: ["sep", "oct", "nov", "dec"]
~~~
{: .output}

## Using Dictionaries to Store Associative Data

Lists are used to store ordered collections of objects that you need to access with a simple
index value. However, not all data is like this. For example, how would you store data from an
address book where you have 'fields' that have values associated with them? In Python, you can
use a type of collection called a Dictionary. Values stored in a dictionary are associated with a
**key** that you can then use to retrieve the value instead of using an index:

~~~
info_dict = { "First Name" : "Fred", "Surname": "Peterson", "Age": 25 }
print( info_dict["Surname"] )
print( info_dict["Age"] )
~~~
{: .language-python}

You can use any immutable object as a key (in practise this is generally numbers or strings!) and
store any object as the value including `list`s or other `dict`s. As with lists, there are 
several ways to add entries to a dictionary. The easiest of these is to
simply reference a new key and assign it a value:

~~~
info_dict["Country"] = "UK"
print(info_dict)
~~~
{: .language-python}
~~~
{'First Name': 'Fred', 'Surname': 'Peterson', 'Age': 25, 'Country': 'UK'}
~~~
{: .output}


> ## Slicing From the End
>
> Use slicing to access only the last four characters of a string or entries of a list.
>
> ~~~
> string_for_slicing = "Observation date: 02-Feb-2013"
> list_for_slicing = [["fluorine", "F"], ["chlorine", "Cl"], ["bromine", "Br"], ["iodine", "I"], ["astatine", "At"]]
> ~~~
> {: .language-python}
>
> ~~~
> "2013"
> [["chlorine", "Cl"], ["bromine", "Br"], ["iodine", "I"], ["astatine", "At"]]
> ~~~
> {: .output}
>
> Would your solution work regardless of whether you knew beforehand
> the length of the string or list
> (e.g. if you wanted to apply the solution to a set of lists of different lengths)?
> If not, try to change your approach to make it more robust.
>
> > ## Solution
> > Use negative indices to count elements from the end of a container (such as list or string):
> >
> > ~~~
> > string_for_slicing[-4:]
> > list_for_slicing[-4:]
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Non-Continuous Slices
>
> So far we've seen how to use slicing to take single blocks
> of successive entries from a sequence.
> But what if we want to take a subset of entries
> that aren't next to each other in the sequence?
>
> You can achieve this by providing a third argument
> to the range within the brackets, called the _step size_.
> The example below shows how you can take every third entry in a list:
>
> ~~~
> primes = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37]
> subset = primes[0:12:3]
> print("subset", subset)
> ~~~
> {: .language-python}
>
> ~~~
> subset [2, 7, 17, 29]
> ~~~
> {: .output}
>
> Notice that the slice taken begins with the first entry in the range,
> followed by entries taken at equally-spaced intervals (the steps) thereafter.
> If you wanted to begin the subset with the third entry,
> you would need to specify that as the starting point of the sliced range:
>
> ~~~
> primes = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37]
> subset = primes[2:12:3]
> print("subset", subset)
> ~~~
> {: .language-python}
>
> ~~~
> subset [5, 13, 23, 37]
> ~~~
> {: .output}
>
> Use the step size argument to create a new string
> that contains only every other character in the string
> "In an octopus's garden in the shade"
>
> ~~~
> beatles = "In an octopus's garden in the shade"
> ~~~
> {: .language-python}
>
> ~~~
> I notpssgre ntesae
> ~~~
> {: .output}
>
> > ## Solution
> > To obtain every other character you need to provide a slice with the step
> > size of 2:
> >
> > ~~~
> > beatles[0:35:2]
> > ~~~
> > {: .language-python}
> >
> > You can also leave out the beginning and end of the slice to take the whole string
> > and provide only the step argument to go every second
> > element:
> >
> > ~~~
> > beatles[::2]
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Overloading
>
> `+` usually means addition, but when used on strings or lists, it means "concatenate".
> Given that, what do you think the multiplication operator `*` does on lists?
> In particular, what will be the output of the following code?
>
> ~~~
> counts = [2, 4, 6, 8, 10]
> repeats = counts * 2
> print(repeats)
> ~~~
> {: .language-python}
>
> 1.  `[2, 4, 6, 8, 10, 2, 4, 6, 8, 10]`
> 2.  `[4, 8, 12, 16, 20]`
> 3.  `[[2, 4, 6, 8, 10],[2, 4, 6, 8, 10]]`
> 4.  `[2, 4, 6, 8, 10, 4, 8, 12, 16, 20]`
>
> The technical term for this is *operator overloading*:
> a single operator, like `+` or `*`,
> can do different things depending on what it's applied to.
>
> > ## Solution
> >
> > The multiplication operator `*` used on a list replicates elements of the list and concatenates
> > them together:
> >
> > ~~~
> > [2, 4, 6, 8, 10, 2, 4, 6, 8, 10]
> > ~~~
> > {: .output}
> >
> > It's equivalent to:
> >
> > ~~~
> > counts + counts
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}
[hadleywickham-tweet]: https://twitter.com/hadleywickham/status/643381054758363136

{% include links.md %}
