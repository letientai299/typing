Tip 9: Compose repeatable changes
==================================

_Vim is optimized for repetition. In order to exploit this, we have to be
mindful of how we compose our changes._

In Vim, we always have more than one way of doing something. In evaluating
which way is best, the most obvious metric is efficiency: which technique
requires the fewest keystrokes (a.K.a. VimGolf). But how should we pick a
winner in the event of a tie?

Suppose that our cursor is positioned on the "h" at the end of this line of
text, and we want to delete the word "night."

```
normal_mode/the_end.txt
The end is nigh.
```


Delete Backward
---------------

Since our cursor is already at the end of the word, we might begin by deleting
backward.

Keystrokes |     Buffer Contents
-----------|--------------------
`{start}`  |     The end is nigh
`db`       |     The end is `h`
`x`        |     The end is ` `

Pressing `db` deletes from the cursor's starting position to the beginning of
the word, but it leaves the final "h" intact. We can delete this rogue
character by pressing `x`. That gives us a Vim golf score of 3.


Delete Forward
--------------

This time, let's try deleting forward instead.

Keystrokes |     Buffer Contents
-----------|--------------------
`{start}`  |     The end is nigh
`b`        |     The end is `h`
`x`        |     The end is ` `

We have to start by maneuvering our cursor into positioin with the `b` motion.
Once it's in place, we can excise the word with a single `dw` command. Once
again, our Vim golf score is 3.


Delete an Entire Word
---------------------

Both of our solutions so far have involved some kind of preparation or cleanup.
We can be more surgical by using the `aw` text object instead of a motion (see
`:h aw`):

Keystrokes |     Buffer Contents
-----------|--------------------
`{start}`  |     The end is nigh
`daw`      |     The end i`s`

The `daw` command is easily remembered by the mnemonic _delete a word_. We'll
go into more detail on text objects in Tip 51, on page 120, and Tip 52, on page
124.


Tie-Breaker: Which Is Most Repeatable?
--------------------------------------

We're tried three techniques for deleting a word: `dbx`, `dbw` and `daw`. In
each case, our Vim golf score is 3. So how can we settle the question of which
is best?

Remember, Vim is optimized for repetition. Let's go through these techniques
again. This time, we'll finish by invoking the dot command and see what
happens. I urge you try these out for your self.

The backward deletion technique involves two operations: `db` deletes to the
start of the word and then `x` deletes a single character. If we invoke the dot
command, it repeats the single charater deletion (`.` == `x`). That's not what
I would call a big win.

The forward deletion technique also involves two steps. This time, `b` is just
a plain motion, while `dw`makes a change. The dot command repeats `dw`,
deleting from the cursor position to the beginning of the next word. It so
happens that we've already as the end of the line. There is no "next word", so
in this context the dot command isn't useful. But at least it's the shorthand
for something longer (`.` == `dw`).

The final solution only invokes a single operation: `daw`. This technique
doesn't just remove the word, it also deletes a whitespace charater. As a
result, our cursor ends up on the last character of the word "is". If we invoke
the dot command, it will repeat the instruction to delete a word. This time,
the dot command does something truly useful (`.` == `daw`).


Discussion
----------

The `daw` technique invests the most power into the dot command, So I declare
it the winner of this round.

Making effective use of the dot command often requires some forethought,. If
you notice that you have to make the same small change in a handful of places,
you can attempt to compose your changes in such a way that they can be repeated
with the dot command. Recognizing those opportunitites takes practice. But if
you develop a habit of making your changes repeatable wherever possble, then
Vim will reward you for it.

Sometimes, I won't see an opportunity to use the dot command. After making a
change - and finding that I need to perform an identical edit - I realize that
the dot command is primed and ready to do th e work for me. It makes me grin
every time.
