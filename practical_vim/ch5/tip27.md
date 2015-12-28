Tip 27: Meet Vim's Command Line
===============================
 _Command-Line mode prompts us to enter an Ex command, a search pattern, or an
expression. In this tip, we'll meet a selection of Ex commands that operator
on a text in a buffer, and we'll about some of the special key mapping that can
be used in this mode._

When we press the `:` key, Vim switches into Command-Line mode. This mode has
some resemblance to the command line that we use in the shell. We can type the
name of a command and then execute it by pressing `<cr>`. At any time, we can
switch from Command-Line mode back to Normal mode by pressing `<esc>`.

For historical reasons, the commands that we execute from Command-Line mode are
called _Ex commands_ (see On the Etymology of Vim (and Family), on page 53).
Command-Line mode is also enabled when we press `/` to bring up a search
prompt or `<c-r>=` to access the expression register (see Tip 16, on page 31).
Some of the tricks in this chapter are applicable with each of these different
prompts, but for the most part we'll focus on Ex commands.

Command                      Effect
`:[range]delete[x]`          Delete specified lines in to register x
`:[range]yank[x]`            Yank specified lines in to register x
`:[line]put[x]`              Put the text from register x after the specified line
`:[range]copy{address}`      Copy the specified lines to below the line specified by {address}
`:[range]move {address}`     Move the specified lines to below the line specified by {address}
`:[range]join`               Join the specified lines
`:[range]normal {commands}`  Execute Normal mode {commands} on each specified line.
`:[range]substiture/{pattern}/{string}/[flags]}` Replace occurrences of {pattern} with {string} on each specified line
`:[range]global/{pattern}/[cmd]` Execute the Ex command [cmd] on al specified lines where the {pattern} matches.


We can use Ex commands to read the write files (:edit and :write), to create
tabs (:tabnew) or split windows (:split), or to interact with the argument list
(:prev/:next) or the buffer list (:bprev/:bnext). In fact, Vim has an Ex
command for just about everything (see :h ex-cmd-index for the full list).

In this chapter, we'll focus mainly on the handful of Ex commands we can use to
edit text. Table 9, Ex commands that operator on the text in a buffer, on page
53, shows a selection of some of the most useful ones.

Mos of these commands can accept a range. We'll find out what this means  in
Tip 28, on page 54. The `:copy` command is great for quickly duplicating a
line, as we'll see in Duplicate Lines with the `:t` Command, on page 9. The
`:normal` command provides a convenient way to make the same change on a range
of lines, as we'll see in Tip 30, on page 61.

We'll learn more about `:delete`, `:yank`, and `:put` commands in Chapter 10,
Copy and Paste, no page 141. The `:substitute` and `:global` commands are very
powerful, so they each get a chapter of their own. See Chapter 14,
Substitution, on page 214, and Chapter 15, Global Commands, on page 237.



Special Keys in Vim's Command-Line Mode
---------------------------------------

Command-Line mode is similar to Insert mode in that most of the buttons on the
keyboard simply enter a character. In Insert-mode, the text goes into a buffer,
whereas in Command-Line mode the text appears at the prompt. In both of these
modes, we can use control key chords to trigger commands.

Some of these commands are shared between Insert mode and Command-Line mode.
For example, `<c-w>` and `<c-u>` delete backward to the start of the previous
word or to the start of line, respectively. We can use `<c-v>` or
`<c-k>{register}` command, just as we saw in Tip 15, on page 29. Some
Command-Line mode mappings are not found in Insert mode. We'll meet a few of
these in Tip 33, on page 66.

At the command-line prompt, we are limited in the range of motions that we can
use. The `<left>` and `<right>` arrow keys move our cursor one character at a
time in either direction. Compared to the rich set of motions that we're used
to using in Normal mode, this can feel quite limiting. But as we'll see in Tip
34 34, on page 68, Vim's command-line window provides all of the editing
power that we could want for composing complex commands at the prompt.


Ex Commands Strike Far and Wide
-------------------------------

It can sometimes be quicker to use an Ex commands than to get the same job done
with Vim's Normal commands. For example, Normal commands tend to act on the
current character of the current line, whereas an Ex command can be executed
anywhere. This means that we can use Ex commands to make changes without having
to move our cursor. But the greatest feature that distinguishes Ex commands is
their ability to be executed across many lines at the same time.

As a general rule, we could say that Ex commands are long range and have the
capacity to modify many lines in a single move. Or to condense that even
further: Ex commands strike far and wide.

On the Etymology of Vim (and Family)
------------------------------------

`ed` was the original Unix text editor. It was written  as the time when a
video displays were uncommon. Source code was usually printed onto a roll of
paper and edited on a teletype terminal. Commands entered at the terminal would
be sent to a mainframe computer for processing, and the output from each
command would be printed. In those days, the connection between a terminal and
a mainframe was slow, so much so that a quick typist could outpace the network,
entering commands faster than they could be sent for processing. In this
context, it was vital that ed provide a terse syntax. Consider how `p` prints
the current line, while `%p` prints the entire file.

`ed` went through several generations of improvements, including `em` (dubbed
the "editor for mortals"), `en` and eventually `ex`. By this time, video
displays were more common. `ex` added a feature that turned the terminal
screen into an interactive window that showed the contents of a file. Now it
was possible to see changes as they were made in real time. The screen-editing
mode was activated by entering the `:visual` command, or just `:vi` for short.
And that is where the name `vi` comes from.

Vim stands for `vi improved`. That's an understatement - I can't stand to use
regular `vi!`. Look up `:h vi-differences` for a list of Vim features that are
unavailable in vi. Vim's enhancements are essential, but it still owes much to
its heritage. The constraints that guided the design of Vim's ancestors have
endowed us with highly efficient command set that's still valuable today.

