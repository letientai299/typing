Tip 22: Repeat Line-Wise Visual Commands
----------------------------------------

_When we use the dot command to repeat a change made to a visual seletion, it
repeats the change on the same range of text. In this tips, we'll make a change
to a line-wise selection and then repeat it with the dot command._

When we execute a command from Visual mode, we are dropped back into Normal
mode and the range of text that was marked out in Visual mode is unselected. So
what should we do if we want to perform another Visual mode command on the same
range of text?

Suppose that we had the following excerpt of mal-formatted python.

```
visual_mode/fibonacci-malformed.py
def fib(n):
    a,b = 0,1
    while a < n:
print a,
a, b = b, a + b
fib(42)
```

This code sample uses four spaces per indentation. First, we'll have to
configure Vim to match this style.


Preparation
-----------

To make the `<` and `>` commands work properly, we should set the `shiftwidth`
and `softtabstop` settings to 4 and enable `expandtab`. If you want to
understand how these settings work together, check out the "Taps and Spaces"
episode on Vimcasts.org. This one-liner does the trick:

```
:set shiftwidth=4 softtabstop=4 expandtab
```

Indent Once, Then Repeat
------------------------

In our malformatted python excerpt, the two lines below the while keyword
should be indented further by two levels. We could fix it by visually selecting
the text and triggering the `>` command to indent it. But that would only
increase the indentation by one level before dropping us back to Normal mode.


