Tip 30: Run Normal Mode Commands Across a Range
===============================================

_If we want to run a Normal mode command on a series of consecutive lines, we
can do so using the `:normal` command. When used in combination with the dot
command or a macro, we can perform repetitive tasks with very little effort._

Consider the example we met in Tip 2, on page 4. We wanted to append a
semicolon at the end of a series of lines. Using the Dor Formula allowed us to
complete the task rapidly, but in that example we needed to make the change
only on three consecutive lins. What if we had to make the same change fifty
times? Using the Dot Formula, we would have to press `j.` fifty times. That
makes a total of one hundred keystrokes!

There is a better way. To demonstrate, we'll append a semicolon at the end f
each line in this file. To save space, I've only included five lines, but if
you can imagine instead that there are fifty lines, then this teachnique will
seem more potent:

```
ex_mode/foobar.js

var foo = 1
var bar = 'a'
var baz = 'z'
var foobar = foo + bar
var foobarbaz = foo + bar + baz
```

We'll start off as we did before, by changing the first line:
```
...
```

We want to avoid executing the `.` command on each line one by one. Instead, we
can use the `:normal` Ex command to execute the dot command across a range of
lines:

```
...
```

The `:'<,'>normal .` command can be read as follows: "For each line in the
visual selection, execute the Normal mode `.` command." This technique works
just as well whether we're operating on five lines or fifty lines. The real
beauty of it is that we don't even have to count the lines - we can get away
with selecting them in visual mode.

In this case, we've used the `:normal` to execute the dot command, but we can
execute any Normal mode commands in the same way. For example, we could have
solved the problem above with this single command:

```
:%normal A;
```

The `%` symbol is used as a range representing the entire file. So `:%normal
A;` instructs Vim to append a semicolon at the end of every line of the file.
Making this change involves switching into Insert mode, but vim automatically
reverts to Normal mode afterward.

Before executing the specified Normal mode command on each line, Vim moves the
cursor to the begining of the line. So we don't hvae to worry about where the
cursor is positioined when execute the command. This single command could be
used to commend out an entire JavaScript file:


```
:%normal i//
```

While it's possible to use `:normal` wiith any normal command, I find it most
powerful when used in combination with one of Vim's repeat commands: either
`:normal .` for simple repeats or `:normal @q` for more complex tasks. Skip
ahead to Tip 67, on page 164, and Tip 69, on page 169, for a couple of
examples.

In Ex Commands Strike Far and Wike, on page 54, we noted that Ex commands can
change multiple lines at once. The `:normal` command allows us to combine the
expressive nature of Vim's Normal mode commands with the range of Ex commands.
It's a powerful combination!

For yet another alternative solution to the problem convered in this tip, refer
to Tip 26, on page 48.
