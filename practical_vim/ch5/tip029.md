Tip 29: Duplicate or Move Lines Using `:t` and `:m` commands
============================================================

_The `:copy` command (and its shorthand `:t`) lets us duplicate one or more
lines from one part of the document to another, while the `:move` command lets
us place them somewhere else in the document._

For demonstration purposes, we'll use this shopping list:
```
Ex_mode/shopping-list.todo
Shopping list
    Hardware Store
        Buy new hammer
    Beauty Parlor
        Buy nail polish remover
        Buy nails
```

Duplicate Lines with the `:t` Command
-------------------------------------

Our shoping list is incomplete: we also need to buy nails at the hardware
store. To fix the list, we'll reuse the last line of the file, creating a copy
of it below "Hardware Store." We can easily do so using the `:copy` Ex command:

Keystrokes    |  Buffer Contents
--------------|-----------------
`{start}`     |  Shopping list
              |      Hardware Store
              |          Buy new hammer
              |      Beauty Parlor
              |          Buy nail polish remover
              |          Buy nails
`:6copy.`     |  Shopping list
              |      Hardware Store
              |          Buy new hammer
              |          Buy nails
              |      Beauty Parlor
              |          Buy nail polish remover
              |          Buy nails

The format of the copy command goes like this (see `:h copy`):
```
:[range]copy {address}
```

In our example, the `[rage]` was line 6. For our `{address}`, we used the `.`
symbol, which stands for the current line. So we can read the `:6copy.`
command as "Make a copy of line 6 and put it below the current line."

We could shorten the copy command only two letters, as `:co`. Or we can be even
more succinct by using the `:t` command, which is a synonym for `:copy`. As a
mnemonic, you can think of it as _copy TO_. This table shows a few examples of
the `:t` command in action:

Command        | Effect
---------------|-------
`:6t.`         | Copy line 6 to just below the current line
`:t6`          | Copy the current line to just below the line 6
`:t.`          | Duplicate the current line (similar to Normal mode `yyp`)
`:t$`          | Copy the current line to the end of the file
`:'<.'>'t0`    | Copy the visually selected lines to the start of the file.

Note that `:t.` duplicates the current line. Alternatively, we could achieve
the same effect using Normal mode yank and put commands (`yyp`). The one
notable difference between these two techniques for duplicating the current
line is that `yyp` uses a register, whereas `:t.` doesn't. I'll somtimes use
`:t.` to duplicate a line when I don't what to override the current value in
the default register.

In this example, we could have used a variant of `yyp` to duplicate the line we
wanted, but it would require some extra moving around. We would have to jump to
the line we wanted to copy (`6G`), yank it (yy), snap back to where we started
(`<c-o>`), and use the put command (`p`) to duplicate the line. When
duplicating a distant line, the `:t` command is usually more efficient.

In Ex Commands Strike Far and Wide, on page 54, we observed the general rule
that Normal commands act locally, whereas Ex commands ase long range. This
example demonstrates this princple in action.


Move lines with `:m` command
----------------------------

The `:move` command looks similar to the `:copy` command (see `:h move`):
```
:[range]move {address}
```
We can shorten it to a single letter `:m`. Suppose that we want to move the
Hardware Store section after the Beauty Parlor section. We could do so using
the `:move` command as shown in Table 10, Moving a Set of Lines with the `:m`
Command, on page 61.

Having made our visual selection, we simply have to run the command
`:'<,'>m$`. Alternatively, we could run `dGp`. This breaks down line this: `d`
to delete the visual selection, `G` to jump to the end of the file, and `p` to
paste the text that was deleted.

Remember that the `'<,'>` range stands for the visual selection. We could
easily make another visual selection and then repeat the `:'<,'>m$` command to
move the selected text to the end of the file. Repeating the last Ex command is
as easy as pressing `@:` (see Tip 31, on page 63, for another example)). so
this mehtod is more easily reproducible than using Normal mode commands.


