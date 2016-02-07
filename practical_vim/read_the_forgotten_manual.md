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

```
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
