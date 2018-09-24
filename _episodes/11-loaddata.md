---
title: Reading in Tabular Data
teaching: 60
exercises: 30
questions:
- "How can I load tabular data files in Python?"
objectives:
- "Read tabular data from a file into a program."
- "Select individual values and subsections from data."
- "Perform operations on arrays of data."
keypoints:
- "Use the `numpy` library to work with arrays in Python."
- "The expression `array.shape` gives the shape of an array."
- "Use `array[x, y]` to select a single element from a 2D array."
- "All the indexing and slicing that works on strings and lists also works on arrays."
- "Use `numpy.mean(array)`, `numpy.max(array)`, and `numpy.min(array)` to calculate simple statistics."
- "Use `numpy.mean(array, axis=0)` or `numpy.mean(array, axis=1)` to calculate statistics across the specified axis."
---

In this lesson we will take what we've learnt about Python and start applying it to our arthritis
inflammation data by loading some data in and performing the first bits of analysis.

For this part, we would recommend switching back to IPython while you're still exploring
the datasets as it will print out the **large** tables of data in a sensible way!

## Loading data into Python

In order to load our inflammation data, we are going to use a library called
[NumPy](http://docs.scipy.org/doc/numpy/ "NumPy Documentation"). This module contains many
numerical routines for data analysis and we will only be scratching the surface of what it can do
in this course --- it is well worth having a look to see what else is there!

> ## Load in the data
>
> The arthritis data is recorded in comma-separated list files 
> To load this, use the function `loadtxt` provided by `numpy` using the `fname`
> argument for the filename `inflammation-01.csv` and `delimiter` argument set as `,`. 
> Assign this to a variable and the `print` the variable to see what has been loaded.
> 
> > ## Solution
> > ~~~
> > import numpy
> > data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
> > print(data)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

You should hopefully have found the output looking like this:

~~~
array([[ 0.,  0.,  1., ...,  3.,  0.,  0.],
       [ 0.,  1.,  2., ...,  1.,  0.,  1.],
       [ 0.,  1.,  1., ...,  2.,  1.,  1.],
       ...,
       [ 0.,  1.,  1., ...,  1.,  1.,  1.],
       [ 0.,  0.,  0., ...,  0.,  2.,  0.],
       [ 0.,  0.,  1., ...,  1.,  1.,  0.]])
~~~
{: .output}

The `loadtxt` function has loaded all the data from the `inflammation-01.csv` file and stored it
in an object. By default,
only a few rows and columns are shown
(with `...` to omit elements when displaying big arrays).
To save space,
Python displays numbers as `1.` instead of `1.0`
when there's nothing interesting after the decimal point.

This object looks a bit like a list of lists (note the square brackets!) but let's check 
exactly what it is by using the `type` function:

~~~
print(type(data))
~~~
{: .language-python}

~~~
<class 'numpy.ndarray'>
~~~
{: .output}

The output tells us that `data` currently refers to
an N-dimensional array, the functionality for which is provided by the NumPy library.
These arrays are similar to lists but you can do a lot more with them and they are
used throughout the numpy library.
These data correspond to arthritis patients' inflammation.
The rows are the individual patients, and the columns
are their daily inflammation measurements.

> ## Data Type and Shape
> 
> When we created the variable `data` to store our arthritis data, we didn't just create the 
> array; we also created information about the array, called 
> [members]({{ page.root }}/reference/#member) or attributes. These members are accessed just
> like functions on an object or from a module using the `.` operator.
>
> Use the `dtype` and `shape` members of your `data` variable to find out what the array contains
> and how many rows and columns it has.
> > ## Solution
> > ~~~
> > print(data.dtype)
> > print(data.shape)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

This should have told you that the array contains `float64` or floating point numbers and
has 60 rows and 40 columns. 

If we want to get a single number from the array, we must provide an
[index]({{ page.root }}/reference/#index) in square brackets after the variable name, just as we
do in math when referring to an element of a matrix and how we accessed elements in strings and
lists. However, our inflammation data has two dimensions, so
we will need to use two indices to refer to one specific value. Here is where NumPy arrays differ
significantly from normal lists in that you can give both indices in the square brackets:

~~~
print('first value in data:', data[0, 0])
~~~
{: .language-python}

~~~
first value in data: 0.0
~~~
{: .output}

~~~
print('middle value in data:', data[30, 20])
~~~
{: .language-python}

~~~
middle value in data: 13.0
~~~
{: .output}

The expression `data[30, 20]` accesses the element at row 30, column 20. As with lists, NumPy arrays
are zero-indexed and so start from (0,0).

> ## In the Corner
>
> What may also surprise you is that when Python displays an array,
> it shows the element with index `[0, 0]` in the upper left corner
> rather than the lower left.
> This is consistent with the way mathematicians draw matrices
> but different from the Cartesian coordinates.
> The indices are (row, column) instead of (column, row) for the same reason,
> which can be confusing when plotting data.
> ![Zero Index](../fig/python-zero-index.png)
{: .callout}

Arrays also know how to perform common mathematical operations on their values.  The simplest
operations with data are arithmetic: addition, subtraction, multiplication, and division.  When you
do such operations on arrays, the operation is done element-by-element.  Thus:

~~~
doubledata = data * 2.0
~~~
{: .language-python}

will create a new array `doubledata`
each elements of which is twice the value of the corresponding element in `data`:

~~~
print('original:')
print(data[:3, 36:])
print('doubledata:')
print(doubledata[:3, 36:])
~~~
{: .language-python}

~~~
original:
[[ 2.  3.  0.  0.]
 [ 1.  1.  0.  1.]
 [ 2.  2.  1.  1.]]
doubledata:
[[ 4.  6.  0.  0.]
 [ 2.  2.  0.  2.]
 [ 4.  4.  2.  2.]]
~~~
{: .output}

If, instead of taking an array and doing arithmetic with a single value (as above), you did the
arithmetic operation with another array of the same shape, the operation will be done on
corresponding elements of the two arrays.  Thus:

~~~
tripledata = doubledata + data
~~~
{: .language-python}

will give you an array where `tripledata[0,0]` will equal `doubledata[0,0]` plus `data[0,0]`,
and so on for all other elements of the arrays.

~~~
print('tripledata:')
print(tripledata[:3, 36:])
~~~
{: .language-python}

~~~
tripledata:
[[ 6.  9.  0.  0.]
 [ 3.  3.  0.  3.]
 [ 6.  6.  3.  3.]]
~~~
{: .output}





Often, we want to do more than add, subtract, multiply, and divide array elements.  NumPy knows how
to do more complex operations, too.  If we want to find the average inflammation for all patients on
all days, for example, we can ask NumPy to compute `data`'s mean value:

~~~
print(numpy.mean(data))
~~~
{: .language-python}

~~~
6.14875
~~~
{: .output}

`mean` is a [function]({{ page.root }}/reference/#function) that takes
an array as an [argument]({{ page.root }}/reference/#argument).

> ## Not All Functions Have Input
>
> Generally, a function uses inputs to produce outputs.
> However, some functions produce outputs without
> needing any input. For example, checking the current time
> doesn't require any input.
>
> ~~~
> import time
> print(time.ctime())
> ~~~
> {: .language-python}
>
> ~~~
> 'Sat Mar 26 13:07:33 2016'
> ~~~
> {: .output}
>
> For functions that don't take in any arguments,
> we still need parentheses (`()`)
> to tell Python to go and do something for us.
{: .callout}

NumPy has lots of useful functions that take an array as input.
Let's use three of those functions to get some descriptive values about the dataset.
We'll also use multiple assignment,
a convenient Python feature that will enable us to do this all in one line.

~~~
maxval, minval, stdval = numpy.max(data), numpy.min(data), numpy.std(data)

print('maximum inflammation:', maxval)
print('minimum inflammation:', minval)
print('standard deviation:', stdval)
~~~
{: .language-python}

Here we've assigned the return value from `numpy.max(data)` to the variable `maxval`, the value
from `numpy.min(data)` to `minval`, and so on.

~~~
maximum inflammation: 20.0
minimum inflammation: 0.0
standard deviation: 4.61383319712
~~~
{: .output}

> ## Mystery Functions in IPython
>
> How did we know what functions NumPy has and how to use them?
> If you are working in the IPython/Jupyter Notebook, there is an easy way to find out.
> If you type the name of something followed by a dot, then you can use tab completion
> (e.g. type `numpy.` and then press tab)
> to see a list of all functions and attributes that you can use. After selecting one, you
> can also add a question mark (e.g. `numpy.cumprod?`), and IPython will return an
> explanation of the method! This is the same as doing `help(numpy.cumprod)`.
{: .callout}

When analyzing data, though,
we often want to look at variations in statistical values,
such as the maximum inflammation per patient
or the average inflammation per day.
One way to do this is to create a new temporary array of the data we want,
then ask it to do the calculation:

~~~
patient_0 = data[0, :] # 0 on the first axis (rows), everything on the second (columns)
print('maximum inflammation for patient 0:', patient_0.max())
~~~
{: .language-python}

~~~
maximum inflammation for patient 0: 18.0
~~~
{: .output}

Everything in a line of code following the '#' symbol is a
[comment]({{ page.root }}/reference/#comment) that is ignored by Python.
Comments allow programmers to leave explanatory notes for other
programmers or their future selves.

We don't actually need to store the row in a variable of its own.
Instead, we can combine the selection and the function call:

~~~
print('maximum inflammation for patient 2:', numpy.max(data[2, :]))
~~~
{: .language-python}

~~~
maximum inflammation for patient 2: 19.0
~~~
{: .output}

What if we need the maximum inflammation for each patient over all days (as in the
next diagram on the left) or the average for each day (as in the
diagram on the right)? As the diagram below shows, we want to perform the
operation across an axis:

![Operations Across Axes](../fig/python-operations-across-axes.png)

To support this functionality,
most array functions allow us to specify the axis we want to work on.
If we ask for the average across axis 0 (rows in our 2D example),
we get:

~~~
print(numpy.mean(data, axis=0))
~~~
{: .language-python}

~~~
[  0.           0.45         1.11666667   1.75         2.43333333   3.15
   3.8          3.88333333   5.23333333   5.51666667   5.95         5.9
   8.35         7.73333333   8.36666667   9.5          9.58333333
  10.63333333  11.56666667  12.35        13.25        11.96666667
  11.03333333  10.16666667  10.           8.66666667   9.15         7.25
   7.33333333   6.58333333   6.06666667   5.95         5.11666667   3.6
   3.3          3.56666667   2.48333333   1.5          1.13333333
   0.56666667]
~~~
{: .output}

As a quick check,
we can ask this array what its shape is:

~~~
print(numpy.mean(data, axis=0).shape)
~~~
{: .language-python}

~~~
(40,)
~~~
{: .output}

The expression `(40,)` tells us we have an N×1 vector,
so this is the average inflammation per day for all patients.
If we average across axis 1 (columns in our 2D example), we get:

~~~
print(numpy.mean(data, axis=1))
~~~
{: .language-python}

~~~
[ 5.45   5.425  6.1    5.9    5.55   6.225  5.975  6.65   6.625  6.525
  6.775  5.8    6.225  5.75   5.225  6.3    6.55   5.7    5.85   6.55
  5.775  5.825  6.175  6.1    5.8    6.425  6.05   6.025  6.175  6.55
  6.175  6.35   6.725  6.125  7.075  5.725  5.925  6.15   6.075  5.75
  5.975  5.725  6.3    5.9    6.75   5.925  7.225  6.15   5.95   6.275  5.7
  6.1    6.825  5.975  6.725  5.7    6.25   6.4    7.05   5.9  ]
~~~
{: .output}

which is the average inflammation per patient across all days.


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

> ## Sorting Out References
>
> What does the following program print out?
>
> ~~~
> first, second = 'Grace', 'Hopper'
> third, fourth = second, first
> print(third, fourth)
> ~~~
> {: .language-python}
>
> > ## Solution
> > ~~~
> > Hopper Grace
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Slicing Strings
>
> A section of an array is called a [slice]({{ page.root }}/reference/#slice).
> We can take slices of character strings as well:
>
> ~~~
> element = 'oxygen'
> print('first three characters:', element[0:3])
> print('last three characters:', element[3:6])
> ~~~
> {: .language-python}
>
> ~~~
> first three characters: oxy
> last three characters: gen
> ~~~
> {: .output}
>
> What is the value of `element[:4]`?
> What about `element[4:]`?
> Or `element[:]`?
>
> > ## Solution
> > ~~~
> > oxyg
> > en
> > oxygen
> > ~~~
> > {: .output}
> {: .solution}
>
> What is `element[-1]`?
> What is `element[-2]`?
>
> > ## Solution
> > ~~~
> > n
> > e
> > ~~~
> > {: .output}
> {: .solution}
>
> Given those answers,
> explain what `element[1:-1]` does.
>
> > ## Solution
> > Creates a substring from index 1 up to (not including) the final index,
> > effectively removing the first and last letters from 'oxygen'
> {: .solution}
{: .challenge}

> ## Thin Slices
>
> The expression `element[3:3]` produces an [empty string]({{ page.root }}/reference/#empty-string),
> i.e., a string that contains no characters.
> If `data` holds our array of patient data,
> what does `data[3:3, 4:4]` produce?
> What about `data[3:3, :]`?
>
> > ## Solution
> > ~~~
> > []
> > []
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Plot Scaling
>
> Why do all of our plots stop just short of the upper end of our graph?
>
> > ## Solution
> > Because matplotlib normally sets x and y axes limits to the min and max of our data
> > (depending on data range)
> {: .solution}
>
> If we want to change this, we can use the `set_ylim(min, max)` method of each 'axes',
> for example:
>
> ~~~
> axes3.set_ylim(0,6)
> ~~~
> {: .language-python}
>
> Update your plotting code to automatically set a more appropriate scale.
> (Hint: you can make use of the `max` and `min` methods to help.)
>
> > ## Solution
> > ~~~
> > # One method
> > axes3.set_ylabel('min')
> > axes3.plot(numpy.min(data, axis=0))
> > axes3.set_ylim(0,6)
> > ~~~
> > {: .language-python}
> {: .solution}
>
> > ## Solution
> > ~~~
> > # A more automated approach
> > min_data = numpy.min(data, axis=0)
> > axes3.set_ylabel('min')
> > axes3.plot(min_data)
> > axes3.set_ylim(numpy.min(min_data), numpy.max(min_data) * 1.1)
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Drawing Straight Lines
>
> In the center and right subplots above, we expect all lines to look like step functions because
> non-integer value are not realistic for the minimum and maximum values. However, you can see
> that the lines are not always vertical or horizontal, and in particular the step function
> in the subplot on the right looks slanted. Why is this?
>
> > ## Solution
> > Because matplotlib interpolates (draws a straight line) between the points.
> > One way to do avoid this is to use the Matplotlib `drawstyle` option:
> >
> > ~~~
> > import numpy
> > import matplotlib.pyplot
> >
> > data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
> >
> > fig = matplotlib.pyplot.figure(figsize=(10.0, 3.0))
> >
> > axes1 = fig.add_subplot(1, 3, 1)
> > axes2 = fig.add_subplot(1, 3, 2)
> > axes3 = fig.add_subplot(1, 3, 3)
> >
> > axes1.set_ylabel('average')
> > axes1.plot(numpy.mean(data, axis=0), drawstyle='steps-mid')
> >
> > axes2.set_ylabel('max')
> > axes2.plot(numpy.max(data, axis=0), drawstyle='steps-mid')
> >
> > axes3.set_ylabel('min')
> > axes3.plot(numpy.min(data, axis=0), drawstyle='steps-mid')
> >
> > fig.tight_layout()
> >
> > matplotlib.pyplot.show()
> > ~~~
> > {: .language-python}
> ![Plot with step lines](../fig/01-numpy_exercise_0.png)
> {: .solution}
{: .challenge}

> ## Make Your Own Plot
>
> Create a plot showing the standard deviation (`numpy.std`)
> of the inflammation data for each day across all patients.
>
> > ## Solution
> > ~~~
> > std_plot = matplotlib.pyplot.plot(numpy.std(data, axis=0))
> > matplotlib.pyplot.show()
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Moving Plots Around
>
> Modify the program to display the three plots on top of one another
> instead of side by side.
>
> > ## Solution
> > ~~~
> > import numpy
> > import matplotlib.pyplot
> >
> > data = numpy.loadtxt(fname='inflammation-01.csv', delimiter=',')
> >
> > # change figsize (swap width and height)
> > fig = matplotlib.pyplot.figure(figsize=(3.0, 10.0))
> >
> > # change add_subplot (swap first two parameters)
> > axes1 = fig.add_subplot(3, 1, 1)
> > axes2 = fig.add_subplot(3, 1, 2)
> > axes3 = fig.add_subplot(3, 1, 3)
> >
> > axes1.set_ylabel('average')
> > axes1.plot(numpy.mean(data, axis=0))
> >
> > axes2.set_ylabel('max')
> > axes2.plot(numpy.max(data, axis=0))
> >
> > axes3.set_ylabel('min')
> > axes3.plot(numpy.min(data, axis=0))
> >
> > fig.tight_layout()
> >
> > matplotlib.pyplot.show()
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Stacking Arrays
>
> Arrays can be concatenated and stacked on top of one another,
> using NumPy's `vstack` and `hstack` functions for vertical and horizontal stacking, respectively.
>
> ~~~
> import numpy
>
> A = numpy.array([[1,2,3], [4,5,6], [7, 8, 9]])
> print('A = ')
> print(A)
>
> B = numpy.hstack([A, A])
> print('B = ')
> print(B)
>
> C = numpy.vstack([A, A])
> print('C = ')
> print(C)
> ~~~
> {: .language-python}
>
> ~~~
> A =
> [[1 2 3]
>  [4 5 6]
>  [7 8 9]]
> B =
> [[1 2 3 1 2 3]
>  [4 5 6 4 5 6]
>  [7 8 9 7 8 9]]
> C =
> [[1 2 3]
>  [4 5 6]
>  [7 8 9]
>  [1 2 3]
>  [4 5 6]
>  [7 8 9]]
> ~~~
> {: .output}
>
> Write some additional code that slices the first and last columns of `A`,
> and stacks them into a 3x2 array.
> Make sure to `print` the results to verify your solution.
>
> > ## Solution
> >
> > A 'gotcha' with array indexing is that singleton dimensions
> > are dropped by default. That means `A[:, 0]` is a one dimensional
> > array, which won't stack as desired. To preserve singleton dimensions,
> > the index itself can be a slice or array. For example, `A[:, :1]` returns
> > a two dimensional array with one singleton dimension (i.e. a column
> > vector).
> >
> > ~~~
> > D = numpy.hstack((A[:, :1], A[:, -1:]))
> > print('D = ')
> > print(D)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > D =
> > [[1 3]
> >  [4 6]
> >  [7 9]]
> > ~~~
> > {: .output}
> {: .solution}
>
> > ## Solution
> >
> > An alternative way to achieve the same result is to use Numpy's
> > delete function to remove the second column of A.
> >
> > ~~~
> > D = numpy.delete(A, 1, 1)
> > print('D = ')
> > print(D)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > D =
> > [[1 3]
> >  [4 6]
> >  [7 9]]
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## Change In Inflammation
>
> This patient data is _longitudinal_ in the sense that each row represents a
> series of observations relating to one individual.  This means that
> the change in inflammation over time is a meaningful concept.
>
> The `numpy.diff()` function takes a NumPy array and returns the
> differences between two successive values along a specified axis.  For
> example, a NumPy array that looks like this:
>
> ~~~
> npdiff = numpy.array([ 0,  2,  5,  9, 14])
> ~~~
> {: .language-python}
>
> Calling `numpy.diff(npdiff)` would do the following calculations and
> put the answers in another array.
>
> ~~~
> [ 2 - 0, 5 - 2, 9 - 5, 14 - 9 ]
> ~~~
> {: .language-python}
>
> ~~~
> numpy.diff(npdiff)
> ~~~
> {: .language-python}
>
> ~~~
> array([2, 3, 4, 5])
> ~~~
> {: .language-python}
>
> Which axis would it make sense to use this function along?
>
> > ## Solution
> > Since the row axis (0) is patients, it does not make sense to get the
> > difference between two arbitrary patients. The column axis (1) is in
> > days, so the difference is the change in inflammation -- a meaningful
> > concept.
> >
> > ~~~
> > numpy.diff(data, axis=1)
> > ~~~
> > {: .language-python}
> {: .solution}
>
> If the shape of an individual data file is `(60, 40)` (60 rows and 40
> columns), what would the shape of the array be after you run the `diff()`
> function and why?
>
> > ## Solution
> > The shape will be `(60, 39)` because there is one fewer difference between
> > columns than there are columns in the data.
> {: .solution}
>
> How would you find the largest change in inflammation for each patient? Does
> it matter if the change in inflammation is an increase or a decrease?
>
> > ## Solution
> > By using the `numpy.max()` function after you apply the `numpy.diff()`
> > function, you will get the largest difference between days.
> >
> > ~~~
> > numpy.max(numpy.diff(data, axis=1), axis=1)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > array([  7.,  12.,  11.,  10.,  11.,  13.,  10.,   8.,  10.,  10.,   7.,
> >          7.,  13.,   7.,  10.,  10.,   8.,  10.,   9.,  10.,  13.,   7.,
> >         12.,   9.,  12.,  11.,  10.,  10.,   7.,  10.,  11.,  10.,   8.,
> >         11.,  12.,  10.,   9.,  10.,  13.,  10.,   7.,   7.,  10.,  13.,
> >         12.,   8.,   8.,  10.,  10.,   9.,   8.,  13.,  10.,   7.,  10.,
> >          8.,  12.,  10.,   7.,  12.])
> > ~~~
> > {: .language-python}
> >
> > If inflammation values *decrease* along an axis, then the difference from
> > one element to the next will be negative. If
> > you are interested in the **magnitude** of the change and not the
> > direction, the `numpy.absolute()` function will provide that.
> >
> > Notice the difference if you get the largest _absolute_ difference
> > between readings.
> >
> > ~~~
> > numpy.max(numpy.absolute(numpy.diff(data, axis=1)), axis=1)
> > ~~~
> > {: .language-python}
> >
> > ~~~
> > array([ 12.,  14.,  11.,  13.,  11.,  13.,  10.,  12.,  10.,  10.,  10.,
> >         12.,  13.,  10.,  11.,  10.,  12.,  13.,   9.,  10.,  13.,   9.,
> >         12.,   9.,  12.,  11.,  10.,  13.,   9.,  13.,  11.,  11.,   8.,
> >         11.,  12.,  13.,   9.,  10.,  13.,  11.,  11.,  13.,  11.,  13.,
> >         13.,  10.,   9.,  10.,  10.,   9.,   9.,  13.,  10.,   9.,  10.,
> >         11.,  13.,  10.,  10.,  12.])
> > ~~~
> > {: .language-python}
> >
> {: .solution}
{: .challenge}

{% include links.md %}
