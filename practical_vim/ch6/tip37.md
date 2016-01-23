Tip 37: Group Buffers into a Collection with the Argument List
==============================================================

_The argument list is easily managed and can be useful for grouping together a
collection of files for easy navigation. We can run an Ex command on each item
in the argument list using the `:argdo` command._


Let's start by opening a handful of files in Vim:

```
cd code/files/letters
vim *.txt
5 files to edit
```

In Tip 36, on page 77, we saw that the `:ls` command provides a listing of
buffers. Now let's examine the argument list:
```
:args
[a.txt] b.txt c.txt d.txt e.txt
```

The argument list represents the list of files that was passed as an argument
when we ran the `vim` command. In our case, we provided a single argument,
`*.txt`, but our shell expanded the `*` wildcard, matching the files that we
see in our argument list. The `[]` characters indicate which of the files in
the argument list is active.

Compared to the listing provided by the`:ls` command, the output from running
`:args` look crude. It should come as no surprise to learn that the argument
list was a feature of `vi`, whereas the buffer list is an enhancement
introduced by Vim. But give the argument list a change, and you'll see that it
makes a fine complement to the buffer list.

Like many features in Vim, the functionality of the argument list has been
enhanced, wile the original name has stuck. We can change the contents of the
argument list at any time, which means that the `:args` listing doesn't
necessarily reflect the values that were passed to the `vim` command when we
launched the editor. Don't take the name literally! (Also, see ':compiler' and
':make' Are not just for Compiled languages, on page 268.)


Populate the Argument List
--------------------------

When the `:args` Ex commands is run without arguments, it prints the contents
of the argument list. We can also set the contents of the arguments list using
this form (`:h :args_f`):

```
:args {arglist}
```

The `{argist}` can include filenames, wildcard, or even the output from a
shell command. To demonstrate, we'll use the `files/mvc` directory, which you
can find it in the source files that come distributed with this book. If you
want to follow along, switch to that directory and launch Vim.

```
cd code/files/mvc
vim 
```

For an overview of the directory tree, refer to code listing on page 94.

Specify Files by Name
---------------------

The simplest way of populating the argument list is by specifying filenames one
by one:

```
:args index.html, app.js
:args
[index.html] app.js
```

This technique works fine if we only want to add a handful of buffers to our
set. It has the advantage that we can specify the order, but doing it by hand
can be laborious. If we want to add a lot of files to the arguments list, we
can get the job done faster by using wildcard.

Specify Files by Glob
---------------------

Wildcard is placeholders that can stand in for characters in the name of a file
or directory. The * symbol will match zero or more characters, but only in the
scope of the specified directory (`:h wildcard`). The ** wildcard also matches
zero or more characters, but it can recurse downward into directories below the
specified directory. (`:h starstar-wildcard`).








