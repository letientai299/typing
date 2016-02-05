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


