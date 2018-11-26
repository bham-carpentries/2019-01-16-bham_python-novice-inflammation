---
title: Using External Modules
teaching: 15
exercises: 5
questions:
- "How can I extend Python's functionality?"
- "How can I use code other people have written?"
objectives:
- "Import modules into your python code"
- "Call the functions provided by these modules just like other code"
keypoints:
- "To import a module, simply call `import <module>`"
- "You can import particular elements of a module using `from <module> import <func>`"
- "Rename a module in your code using `import <module> as <myname>`"
---

We've now covered a lot of the basic syntax and commands in Python. However, you may be
wondering how you do anything useful with this without creating lots of code for all sorts
of mundane jobs such as reading in data, performing statistical analyses or producing plots.
Luckily, Python has **many** external bits of code (called 'modules') that you can easily
use within your own code.

## Importing an External Module

Importing a module is like getting a piece of lab equipment out of a storage locker and setting it
up on the bench. Moduels provide additional functionality to the basic Python package, much like
a new piece of equipment adds functionality to a lab space. Just like in the lab, importing too
many libraries can sometimes complicate and slow down your programs - so we only import what we
need for each program.

If you want access to an external module in you code, all you have to do is:
~~~
import math
~~~
{: .language-python}

From this point on in your code, you can use the `math` name to access this module. For
example, to add up all the numbers in a list you can do:

~~~
import math
nums = [1., 6., 9.23]
total = math.fsum(nums)
print(total)
~~~
{: .language-python}

This code asks Python to run the function `fsum` which
belongs to the `math` module in a similar way to how the `append` function belonged to the
`list` object. 

As an example, John Smith is the John that belongs to the Smith family,
We could use the dot notation to write his name `smith.john`,
just as `fsum` is a function that belongs to the `math` module.

It's not just functions that a module can provide - there can also be variables as well:
~~~
import math
print(math.pi)
~~~
{: .language-python}

If you just want to import a specific function rather than a whole module, you can say this
when importing. You then only need to call the function name without the module name as well:
~~~
from math import fsum
nums = [1., 6., 9.23]
total = fsum(nums)
print(total)
~~~
{: .language-python}

Finally, you can also rename what something is imported as if it conflicts with another 
name you are using or you just want to make it clearer:

~~~
import math as sys_math
nums = [1., 6., 9.23]
total = sys_math.fsum(nums)
print(total)
~~~
{: .language-python}

> ## Using the `sys` module
>
> Another module we will be using in the future is the `sys` module which contains functions
> and variables that are associated with Python system that you are running in. One variable
> in particular which we will use later is a list of all the command line arguments passed to 
> Python.
>
> Either using the built in help system or Google, find the variable in the `sys` module that
> corresponds to the search path that python uses to find modules and write a loop to print out each one.
> 
> > ## Solution
> > ~~~
> > import sys
> > for p in sys.path:
> >    print(p)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}
