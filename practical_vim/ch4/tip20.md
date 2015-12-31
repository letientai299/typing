Tip 20: Grok Visual Mode
========================

_Visual mode allows us to select a range of text and then operate upon it.
However intuitive this might seem, Vim's perspective on selecting text is
different from other text editors._

Suppose for a minute that we're not working with Vim but instead filling out a
text area on a web page. We're written the word "March," but it should read
"April," so using the mouse, we double-click the word to select it. Having
highlighted the word, we could hit the backspace key to delete it and then type
out the correct month as a replacement.

You probably already now that there's no need to hit the backspace key in this
example. With the word "March" selected, we would only have to type the letter
"A" and it would replace the selection, preparing the way so that we could type
out the rest of the word "April." It's not much, but a keystroke saved is a
keystroke earned.

If you expect this behavior to carry over to Vim's Visual mode, you're in for a
surprise. The clue is right there in the name: Visual mode is just another
mode, which means that each key performs a different function.

Many of the commands that you are familiar with from Normal mode work just the
same in Visual mode We can still use h, j, k, and l as cursor keys. We can use
`f{char}` to jump to a character on the current line and then repeat or reverse
the jump with the `;` and `,` commands, respectively. We can even use the
search command (and `n`/`N`) to jump to pattern matches. Each time we move our
cursor in Visual mode, we change the bounds of the selection.

Some Visual mode commands perform the same basic function as in Normal mode but
with a slight twist. For example, the `c` command is consistent in both modes
in taht iit deletes the specified text and then switches to Insert mode. The
different is in how we specify the range on which to act. From Normal mode,
we trigger the change command first and then specify the range as a motion.
This, if you'll remember from Tip 12, on page 24, is called an operator
command. Whereas in Visual mode, we start off by making the selection and then
trigger the change command. This inversion of control can be generalized for
all operator commands (see Table 2, Vim's Operator Commands, on page 25). For
most people, the Visual mode approach feels more intuitive.

Let's revisit the simple example where we wanted to change the word "March" to
"April." This time, suppose that we have left the confines of the text area on
a web page and we're comfortably back inside Vim. We place our cursor somewhere
on the word "March" and run `viw` to vsually select the word. Now, we can't
just type the word "April" because that would trigger the `A` command and
append the text "pril"! Instead, we'll use the `c` command to change the
selection, deleting the word and dropping us into Insert mode, where we can
type out the word "April" in full. This pattern of usage is similar to our
original example, except that we use the `c` key instead of backspace.

> Meet Select Mode
> ----------------
>
> In a typical text editing environment, selected text is deleted when we type
> any printable character. Vim's Visual mode doesn't follow this convention -
> but Select mode does. According to Vim's built-in documentation, it
> "resembles the selection mode in Mirosoft Windows" (see `:h Select-mode`).
> Printable characters cause the selection to be deleted. Vim enters Insert
> mode, and the typed character is inserted.
>
> We can toggle between Visual and Select modes by pressing `<C-g>`. The only
> visible difference is the message at the bottom of screen, which switches
> between ` -- VISUAL --` and `--SELECT--`. But if we type any printable
> character in select mode, it will replace the selection and switch to Insert
> mode. Of course, from Visual mode you could just asa well use the `c` key to
> change the selection.
>
> If you are happy to embrace the modal nature of Vim, then you should find
> little use for Select mode, which holds the hand of users who want to make
> Vim behave more like other text editors. I can think of only one place where
> I consistenly use Select mode: when using a plugn that emulates TextMate's
> snippet functionaliity, Select mode highlights the active placeholder.
