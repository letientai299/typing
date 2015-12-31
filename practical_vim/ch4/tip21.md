Tip 21: Define a Visual Selection
=================================

_Visual mode's three submodes deal wth different kinds of text. In this tip,
we'll look at the ways of enabling each visual submode, as well as how to
switch between them._

Vim has three kinds of Visual mode. In _character-wise Vsual mode_, we can
select anything from a single character up to a range of characters within a
line or spanning multiple lines. This is suitable for working at the level of
individual words or phrases. If we want to operate on entire lines, we can use
_line-wise_ visual mode instead. Finally, _block-wise__ Visual mode allows us
to work with columnar regions of the document. Block-wise Visual mode s quite
special, so we'll discuss it at greatedr length in Tip 24, on page 45, Tip 25,
on page 47, and Tip 26, on page 48.


Enabling Visual Modes
---------------------

The `v` key is our gateway into Visual Mode. From Normal mode, we can press `v`
by itself to enable characte-wise Visual mode. Line-wise Visual mode is enabled
by pressing `V`, and block-wise Visual mode by pressing `<c-v>`. These commands
are summaized in the following table.

Command         | Effect
----------------|-------
`v`             | Enable character-wise Visual mode
`V`             | Enable line-wise Visual mode
`<c-V>`         | Enable block-wise Visual mode
`gv`            | Reselect the last visual selection

The `gv` command is a useful little shortcut. It reselects the range of text
that was last selected in Visual mode. No matter whether the previous selection
was character-wise, line-wise, or bloc-wise, the `gv` command is if the last
selection has since been deleted.


Toggling the Free End of a Selection
------------------------------------

The range of a Visua mode selction is marked by two ends: one end is fixed and
the other moves freely with our cursor. We can use the `o` key to toggle the
free end. This is really handy if halfway through defining a selection we
realize that we started in the wrong place. Rather than leaving Visual mode and
starting afresh, we can just hit `o` and redefine the bounds of the selection.
The following demonstrates how we can use this teachnique:

Keystrokes      Buffer Contents
`{start}`       Select from here to `h`ere.
`vbb`           Select from `here to h`ere.
`o`             Select from `here to h`ere.
`e`             Select from `here to here`.
