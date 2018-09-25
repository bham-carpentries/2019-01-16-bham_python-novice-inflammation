---
title: Filtering Data
teaching: 5
exercises: 15
questions:
- "How can I filter out bad data?"
objectives:
- "Using conditionals, protect your analysis code from bad data"
keypoints:
- "If you can identify attributes of bad data in your dataset, you can get your program to filter them out"
---

In our last lesson, we discovered something suspicious was going on
in our inflammation data by drawing some plots. Using our new-found knowledge of conditionals,
we can get Python to automatically recognize the different features we saw,
and take a different action for each

> ## Checking the Maxima
>
> In the first couple of plots, the maximum inflammation per day
> seemed to rise like a straight line, one unit per day.
> By editing the code from the previous lesson, add a check in the `for` loop for this effect,
> e.g. that the maximum for the first day is zero and the max for 21st day is 20.
> Print out a message if a problem is found
> 
> > ## Solution
> > ~~~
> > if numpy.max(data, axis=0)[0] == 0 and numpy.max(data, axis=0)[20] == 20:
> >     print('Suspicious looking maxima!')
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

> ## Checking the Minima
>
> We also saw a different problem in the third dataset;
> the minima per day were all zero (looks like a healthy person snuck into our study).
> Add to your code with an `elif` condition to check if all the minima in a dataset add
> up to zero. Hint: `numpy` has a `sum` function!
>
> > ## Solution
> > ~~~
> > elif numpy.sum(numpy.min(data, axis=0)) == 0:
> >     print('Minima add up to zero!')
> > ~~~
> > {: .language-python}
> {: .solution}
{: .challenge}

Finally, if neither of these conditions are true, we can use `else` to give the all-clear:

~~~
else:
    print('Seems OK!')
~~~
{: .language-python}

Run your code and you should hopefully now see messages printed identifying the different
features in the plots --- the first two with suspicious maxima and the third with suspicious
minima.

{% include links.md %}
