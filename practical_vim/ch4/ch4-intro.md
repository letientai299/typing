Visual Mode
===========

Vim's Visual mode allows us to define a selection of text and then operate upon
it. This should feel pretty intuitive, since it is the model that most editing
software follows. But Vim's take is characteristically different, so we'll
start by making sure we grok Visual Mode (Tip 20, on page 37).

Vim has three variants of Visual mode involving working with characters lines,
or rectangular blocks of text. We'll explore ways of switching between these
modes as well as some useful tricks for modifying the bounds of a selection
(Tip 21, on page 39).

We'll see that the dot command can be used to repeat Visual mode commands, but
that it's especially effective when operating on line-wise regions. When
working with charater-wise selections, the dot command can sometimes fall short
of our expectations. We'll see that in these scenarios, operator commands may
be preferable.

Visual-Block mode is rather special in that it allows us to operate on
rectangular columns of text. You'll find many uses for this feature, but we'll
focus on three tips that demonstrate some of its capabilities.
