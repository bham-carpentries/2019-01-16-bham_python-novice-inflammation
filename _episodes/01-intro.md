---
title: Introduction to Python
teaching: 10
exercises: 5
questions:
- "What is Python?"
- "How do I get it to do things?"
objectives:
- "Start up the IPython interpreter"
- "Write your first code"
keypoints:
- "Python is a general purpose programming language that allows you to get a computer to do almost anything"
- "Generally, Python implementations are **interpreted** rather than **compiled**"
- "It is particularly useful at analysing data"
- "The ipython interpreter can use tab completion and keeps a history of the commands you run"
- "Use `Ctrl-D` to exist an IPython session"
- "Python code is case sensitive"
---

## What is Python?
Python is a general purpose programming language which means that it wasn't designed
to solve a particular problem or group of problems (like R or Matlab) but **any** problem you 
can think of to solve on a computer. Consequently, you can use Python to do almost anything from 
analyze data to running computer systems to creating games.

Though comprised of fairly basic syntax (i.e. the grammer of the commands you give it) it is incredibly
powerful. It is relatively easy to pick up as well and thanks to a very large and growing
set of external modules (or blocks of code) written by other programmers, you can do complicated things
quickly and easily.

One of the reasons for this power is that it is (to a certain degree) an **interpreted** language. This means that the code
you type gets translated into instructions the computer can understand as Python reads it. There is not a
separate optimisation or 'compilation' step to create your executable/binary before you can run your code like there is with some other languages like C++. This
allows the language to be very dynamic but does have the drawback of being slower than others.
However, there are many ways Python has of overcoming these drawbacks and you will almost certainly
never notice a problem!

## Getting Started

Before we can get to grips with analysing our arthritis dataset, we must first find out how to run
Python itself. For the time being, we will use the IPython interpreter that acts like the Shell but
for Python commands. In other words, when you type your instructions at the prompt and press
enter, it will be run straight away.

Python is run just like any other program from a shell prompt - by typing it's name.
If you haven't already, you can start up the intrepreter by typing the following:
~~~
$ ipython
~~~
{: .language-shell}
~~~
Python 3.6.5 |Anaconda, Inc.| (default, Apr 26 2018, 08:42:37) 
Type 'copyright', 'credits' or 'license' for more information
IPython 6.4.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: 
~~~
{: .output}

Note that the output will vary depending on your computer and how you've got Python installed.

> ## Python vs. IPython
>
> You may be wondering why you type `ipython` to run the Python interpreter rather than just
> `python`. This does also work but this is a much more basic interpreter than IPython that
> doesn't have tab completion, syntax highlighting, etc. If you ever need an interactive
> Python prompt, IPython is the best option!
{: .callout}

To quit out, you can do one of the following:

* Use `Ctrl-D` - it will ask for confirmation if you want to quit
* type the command `exit`
* type the command `quit`

This will then drop you back to the shell prompt you were at before.

## Getting Python to do something

Now we can start and (possibly more importantly!) exit Python, we can try to get it do something
by giving it a command. The interactive intepreter (i.e. the `In [x]:` prompt) works in
a very similar way to the shell except that here you will be typing python code directly instead
of running programs. We shall start by getting Python to print something. This is very basic but
will be invaluable going forward:

~~~
print("Hello World")
~~~
{: .language-python}

If all is well, you should see:

~~~
Hello World
~~~
{: .output}

So what did we just do? We typed in a python statement that was interpreted by Python and acted
on when we pressed enter. It interpreted this as 'call the function `print` with the argument
`"Hello World"`. It went away, ran the appropriate code and returned.

But what does the `print` function do? In this case, it's fairly self-expanatory but if you wanted
to know more you can use the `help` function:

~~~
help(print)
~~~
{: .language-python}
~~~
Help on built-in function print in module builtins:

print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.
~~~
{: .output}

You can press `q` to quit out of the editor this opened in (`less` if you're interested!).

IPython also has shell-like behaviour in that you can use the up arrow to go to previous commands 
and `Tab` to auto-complete a function or variable name:

~~~
pri [Tab]
~~~
{: .language-python}

~~~
print
~~~
{: .language-python}

> ## Exploring Tab Completion
>
> On up-to-date versions of IPython, the Tab completion functionality will also suggest the commands
> you mean if several match and also show the arguments a function might take.
>
> Give this a try by doing:
>
> ~~~
> pr [Tab]
> print( [Tab]
> ~~~
> {: .language-python}
>
> What happens if you press `Tab` multiple times?
{: .challenge}

An important thing to remember whenever programming in Python though is that the code is 
**case sensitive**. This means that `print` is completely different and unrelated to `Print`.
To show this, type the following:

~~~
Print("Hello World")
~~~
{: .language-python}

~~~
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-82ee0b7fee85> in <module>()
----> 1 Print("Hello World")

NameError: name 'Print' is not defined
~~~
{: .error}

As you can see, Python didn't know what `Print` was so showed an error (a `NameError` in this case).
