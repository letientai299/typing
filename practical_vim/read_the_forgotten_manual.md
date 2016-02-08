Read the Forgotten Manual
=========================

In _Practical Vim_, I demonstrate by showing examples rather than by describing
them. That's not easy to do with the written word. To show the steps taken
during an interactive editing session, I've adapted a simple notation that
illustrates the keystrokes and the contents of a Vim buffer side by side.

If you're keen to jump to the action, you can safely skip this chapter for now.
It describes each of the conventions used throughout _Practical Vim_, many of
which you'll find to be self-explanatory. At some point, you'll probably come
across a symbol and wonder what it stands for. When that happens, turn back and
consult this chapter for the answer.


Get to Know Vim's Built-in Documentation
----------------------------------------

The best way to get to know Vim's documentation is by spending time in it. To
help out, I've included "hyperlinks" for entries in Vim's documentation. For
example, here's the "hyperlink" for the Vim tutor `:h vimtutor`.

The icon has a dual function. First, it serves as a signpost, drawing the eye
to these helpful references. Second, if you're reading this on an electronic
device that's connected to the Internet, you can click the icon and it will
take you to the relevant entry in Vim's online documentation. In this sense, it
truly is a hyperlink.

But what if you're reading the paper edition of the book? Not to worry. If you
have an installation of Vim within reach, simply enter the command as it
appears in front of the icon.

For example, type `:h vimtutor`(`:h` is an abbreviation for the `:help` command).
Consider this is a unique address for the documentation on vimtutor: a URL of
sorts. In this sense, the help reference is a kind of hyperlink to Vim's
build-in documentation.


Notation for Simulating Vim on the Page
---------------------------------------

Vim's modal interface sets it apart from most other text editors. To make a
musical analogy, let's compare the Qwerty and the piano keyboards. A pianist
can pick out a melody by playing one note at a time or he or she can hold down
several keys at once to sound a chord. In most text editors, keyboards shortcuts
are triggered by pressing a key while holding down one or more modifier
buttons, such as the control and command keys. This is the Qwerty equivalent of
playing a chord on the piano keyboard.

Some of Vim's commands are also triggered by playing chords, but Normal mode
commands are designed to be typed as a sequence of keystrokes. It's the Qwerty
equivalent of playing a melody on the piano keyboard.

`Ctrl-s` is common convention for representing chordal key commands. It means
"Press the Control key and the `s` key at the same time." But this convention
isn't well suited to describing Vim's modal command set. In this section, we'll
meet the notation used throughout _Practical Vim_ to illustrate Vim usage.


Playing Melodies
----------------

In Normal mode, we compose commands by typing one or more keystrokes in
sequence. These commands appear as follows:

Notation | Meaning
---      | ---
`x`      | press `x` once
`dw`     | In sequence, press `d`, then `w`
`dap`    | In sequence, press `d`, `a`, then `p`

Most of these sequences involve two or three keystrokes, but some are longer.
Deciphering the meaning of Vim's Normal mode command sequences can be
challenging, but you'll get better at it with practice.


Playing Chords
--------------

When you see a keystroke such as `<C-p>`, it doesn't mean "Press `<`, then `C`,
then `.`, and so on." The `<C-p>` notation is equivalent to `<Ctrl-p>`, which
means "Press the `<Ctrl>` and `p` keys at the same time."

I didn't choose this notation without good reason. Vim's documentation uses
it (`:h key-notation`), and we can also use it in defining custom key mappings.
Some of Vim's commands are formed by combining chords and keystrokes in
sequence, and this notation handles them well. Consider these examples:

Notation     | Meaning
------------ | --------
`<C-n>`      | Press `<Ctrl>` and `n` at the same time
`g<C-]>`     | Press `g`, followed by `<Ctrl>` and `]` at the same time
`<C-r>0`     | Press `<Ctrl>` and `r` at the same time, then `0`
`<C-w><C-=>` | Press `<Ctrl>` and `w` at the same time, then `<Ctrl>` and `=` at the same time


Placeholders
------------

Many of Vim's commands require two or more keystrokes to be entered in
sequence. Some commands must be followed by a particular kind of keystroke,
while other commands can be followed by any key on the keyboard. I use curly
braces to denote the set of valid keystrokes that can follow a command. Here
are some examples:

Notation          | Meaning
------------      | --------
`f{char}`         | Press `f`, followed by any other character
```{a-z}``        | Press `` ` ``, followed by any lowercase letter.
`m{a-zA-Z}`       | Press `m`, followed by any lowercase or uppercase letter.
`d{motion}`       | Press `d`, followed by any motion command
`<C-r>{register}` | Press <Ctrl> and `r` at the same time, followed by the address of a register


Showing Special Keys
--------------------

Some keys are called by name. This table shows a selection of them:

Notation  | Meaning
--------- | --------
`<ESC>`   | Press the Escape key
`<CR>`    | Press the carriage return key (also known as `<Enter>`)
`<Ctrl>`  | Press the Control key
`<Tab>`   | Press the Tab key
`<Shift>` | Press the Shift key
`<S-Tab>` | Press the `<Shift>` and the `<tab>` keys at the same time
`<Up>`    | Press the up arrow key
`<Down>`  | Press the down arrow key
`␣`       | Press the space bar


Note that the space bar is represented as `␣`. This could be combined with the
`f{char}` command to form `f␣`.


Switching Modes Midcommand
--------------------------

When operating Vim,it's common to switch from Normal to Insert mode and back
again. Each keystroke could mean something different, depending on which mode
is active. I've used an alternative style to represent keystrokes entered in
Insert mode, which makes it easy to differentiate them from Normal mode
keystrokes.

Consider this example: `cw`_replacement<ESC>. The Normal mode `cw` command
deletes to the end of the current word and Switches to Insert mode. Then we
type the word "_replacement_" in Insert mode and press `<ESC>` to switch back
to Normal mode again.

The Normal mode styling is also used for Visual mode keystrokes, while the
Insert mode styling can indicate keystrokes entered in Command-Line mode and
Replace mode. Which mode is active should be clear from context.


Interacting with the Command line.
----------------------------------

In some tips we'll execute a command line, either in the shell or from inside
Vim. This is what it looks like when we execute the `grep` command in the
shell:

```bash
$ grep -n Waldo *
```

And this is how it looks when we execute Vim's built-in `:grep` command:

```
:grep Waldo *
```

In _Practical Vim_, the `$` symbol indicates that a command line is to be
executed in an external shell, whereas the `:` prompt indicates that the
command line is to be executed internally from Command-Line mode. Occasionally
we'll see other prompts, including these:


Prompt  | Meaning
------- | --------
`$`     | Enter the command line in an external shell
`:`     | Use Command-Line mode to execute an Ex command
`/`     | Use Command-Line mode to perform a forward search
`?`     | Use Command-Line mode to perform a backward search
`=`     | Use Command-Line mode to evaluate a Vim script expression


Any time you see an Ex command listed inline, such as `:write`, you can assume
that the `<CR>` key is pressed to execute the command. Nothing happens
otherwise, so you can consider `<CR>` to be implicit.

By contrast, Vim's search command allows us to preview the first match before
pressing `<CR>` (see Tip 81, on page 202). When you see a search command listed
inline, such as `/pattern<CR>`, the `<CR>` keystroke is listed explicitly. If
the `<CR>` is omitted, that's intentional, and it means you shouldn't press
the Enter key just yet.


Showing the Cursor Position in a Buffer
---------------------------------------

When showing the contents of a buffer, it's useful to be able to indicate where
the cursor is positioned. In this example,you should see that the cursor is
placed on the first letter of the word "One":

```
One two three
```

When we make a change that involves several steps, the contents of the buffer
pass through intermediate states. To illustrate the process, I use a table
showing the commands executed in the left column and the contents of the buffer
in the right column. Here's a simple example:

Keystrokes   | Buffer Contents
------------ | ----------------
`{start}`    | One two three
`dw`         | two three


In row 2 we run the `dw` command to delete the word under the cursor. We can
see how the buffer looks immediately after running this command by looking at
the contents of the buffer in the same row.


Highlighting Search Matches
---------------------------

When demonstrating Vim's search command, it's helpful to be able to highlight
any matches that occur in the buffer. In this example,search for the string
"the" causes four occurrences of the pattern to be highlighted:

Keystrokes  | Buffer Contents
------------|----------------
`{start}`   | `t`he problem with these new recruits is that they don't keep their boots clean.
`/the<CR>`  | the problem with `t`hese new recruits is that they don't keep their boots clean.

Skip ahead to Tip 80, on page 201, to find out how to enable search
highlighting in Vim.


Selecting Text in Visual Mode
-----------------------------

Visual mode allows us to select text in the buffer and then operate on the
selection. In this example, we use the `it` text object to select the contents
of the `<a>` tag:

Keystrokes  | Buffer Contents
----------- | ----------------
`{start}`   | <a hrep="http://pragprog.com/dnvim">Practical Vim</a>
`vit`       | <a hrep="http://pragprog.com/dnvim">`Practical Vim`</a>


Note that the styling for a Visual selection is the same for highlighted search
matches. When you see this style, it should be clear from context whether it
represents a search match or a Visual selection.


Downloading the Examples
------------------------

The examples in _Practical Vim_ usually begin by showing the contents of a file
_before_ we change it. These code listings include the file path:

```
macros/incremental.txt
----------------------
partridge in a pear tree
turtle doves
French hens
calling birds
golden rings
```

Each times you see file listed with is file path in this manner, it means that
you can download the example. I recommend that you open the file in Vim and try
out the exercises for yourself. It's the best way to learn!

To follow along, download all the examples and source code from the Pragmatic
Bookshelf. If you're reading on an electronic device that's connected to the
Internet, you can also fetch each file one by one by clicking on the filename.
Try it with the example above.


Use Vim's Factory Settings
--------------------------

Vim is highly configurable. If you don't like the defaults, then you can change
them. That's a good thing, but it could cause confusion if you follow the
examples in this book using a customized version of Vim. You may find that some
thing don't work for you the way that they are described in the text. If you
suspect that your customizations are causing interferences, here's a quick
test. Try quitting Vim and then launching it with these options:

```bash
$ vim -u NONE -N
```

The `-u NONE` flag tells Vim not to source your `vimrc` on startup. That way,
your customizations won't be applied and plugins will disabled. When Vim starts
up without loading a `vimrc` file, it reverts to `vi` compatible mode, which
causes many useful features to be disabled. The `-N` flag prevents this by
setting the `'nocompatible'` option.

For most examples in _Practical Vim_, the `Vim -u NONE -N` trick should
guarantee that you get the same experience as described, but there are a couple
of exceptions. Some of Vim's built-in features are implemented with Vim
script, which means that they will only work when plugins are enabled. This
file contains the absolute minimum configuration that is required to activate
Vim's built-in plugins:

```vim
" essential.vim
set nocompatible
filetype plugin on
```

When launching Vim, you can use this file instead of your `vimrc` by running
the following:

```bash
$ vim -u code/essential.vim
```


You'll have to adjust the `code/essential.vim` path accordingly. With Vim's
built-in plugins enabled, you'll be able to use features such as `netw` (Tip
43, on page 98) and omni-completion (Tip 117, on page 285), as well as many
others. I consider Vim's factory settings to mean built-in plugins enabled and
`vi` compatibility disabled.

Look out for subsections titled "Preparation" at the top of a tip. To follow
along with the material in these tips, you'll need to configured Vim
accordingly. If you start up with Vim's factory settings and then apply the
customizations on the fly, you should be able to reproduce the steps from these
tips without any problems.

If you're still having problems, see Sections 6, _On Vim Versions_, on page
xxiv.


On the Role of Vim Script
-------------------------

Vim script enables us to add new functionality to Vim or to change existing
functionality. It's a complete scripting language itself and a subject worthy
of a book of its own. _Practical Vim_ is not that book.

But we won't steer clear of the subject entirely. Vim script is always just
below the surface, ready to do our bidding. We'll see a few examples of how it
can be used for everyday tasks in Tip 16, on page 31; Tip 70, on page 174; Tip
94, on page 229; and Tip 95, on page 230.

_Practical Vim_ shows you how to get by with Vim's core functionality. In other
words, no third-party plugins assumed. I've made an exception for Tip 86, on
page 212, and Tip 96, on page 233. In each case, the plugin I've recommended
adds a feature that I find indispensable. And in each case, the plugin requires
very little code - less than ten lines of Vim script. Both examples demonstrate
how easily Vim's functionality can be extended. The implementation of
`visalstart.vim` and `Qargs.vim` is presented inline without explanation. This
should give you an idea of what Vim script looks like and what you can
accomplish with it. If it piques your interest, then so much the better.


On Vim Versions
---------------

All examples in _Practical Vim_ were tested on the latest version of Vim, which
was 7.3 at the time of writing. That said, most examples should work find on
any 7.x release, and many of the features discussed are also available in 6.x.

Some of Vim's functionality can be disabled during compilation. For example,
when configuring the build, we could provide the `--with-features=tiny` option,
which would disable all but the most fundamental features (there are also
feature sets labeled `small`, `normal`, `bug`, and `huge`). You can browse the
feature list by looking up `:h +feature-list`.

If you find that you're missing a feature discussed in this book, you might be
using a minimal Vim build. Check whether or not the feature is available to
you with the `:version` command:

```
:version
...
```

On a modern computer, there's no reason to use anything less than Vim's `hude`
feature set!


Vim in the Terminal or Vim with a GUI? You Choose!
--------------------------------------------------

Traditionally, Vim runs inside of the terminal, with not graphical user
interface (GUI). We could say instead that Vim has a TUI: a text user
interface. If you spend most of your day at the command line, this will feel
natural.

If you're accustomed to using a GUI-based text editor, then GVim or (MacVim on
OS X) will provide a helpful bridge into the world of Vim (see `:h gui`). GVim
supports more fonts and more colors for syntax highlighting. Also, you can use
the mouse. And some of the conventions of the operating system are honored.
For example, in MacVim you can interact with the system clipboard using `Cmd-X`
and `Cmd-v`, save a document with `Cmd-S`, or close a window with `Cmd-W`. Use
these while you find your bearings, but be aware that there's always a better
way.


For the purposes of this book, it doesn't matter whether you run Vim in the
terminal or as GVim. We'll focus on core commands that work just as well in
either. We'll learn how to do thing _the Vim way_.
