Chapter 3: Insert mode
======================

Most of Vim's commands are triggered from other modes, but some functionality
is within easy reach from Insert mode. In this chapter, we'll explore these
commands. Although delete, yank, and put commands are all triggered from Normal
mode, we'll see that there is a convenient shortcut for pasting text from a
register without leaving Insert mode. We'll learn that Vim provides two easy
ways for inserting unusual characters that are not represented on the keyboard.

Replace mode is a special case of insert mode, which overwrites existing
characters in the document. We'll learn how to invoke this and consider some
scenarios where it proves useful. We'll also meet Insert Normal mode, a
sub-mode that lets us fire a single Normal mode command before dropping us back
into insert mode.

Autcompletion is the most advanced functionality available to us from Insert
mode. We'll cover it in depth in Chapter 19. Dial X for Autocompletion, on page
275.

Tip 13: Make Corrections Instantly from Insert Mode
===================================================

If we make mistake while composing text in Insert mode, we can fix it
immediately. There's no need to change modes. Besides the backspace key, we can
use a couple of other Insert mode commands to make quick corrections.

Touch typing is more than just not looking at the keyboard: it means doing it
by feel. When touch typists make an error, they know it even before their eyes
process the information on the screen in front of them. They feel it in their
fingers, like a misplaced step.
 When we make a typing error, we can use the backspace key to erase the mistake
and then make a correction. As long as the error appears near the end of the
word, this may be the quickest strategy for making amends. But what if the
mistake was at the start of the word?

Expert typists recommended drastic measures: delete the entire word, then type
it out again. If you can type at a rate above sixty words per minutes, retyping
a word from scratch will only take a second. If you can't type that fast,
consider this to be good practice! There are particular words that I
consistently mistype. Since I started following this advice, I've become more
aware of which words trip me up. As a result, I now make fewer mistakes.

Alternatively, you could switch to Normal mode, navigate to start of the word,
fix the error, then hit `A` to return where you left off in Insert mode. That
little dance could take longer than a second, and it would do nothing to
improve your touch-typing skills. Just because we can switch modes doesn't mean
that we should.

In Insert mode, the backspace key works  just as you would expect: it deletes
the character in front of the cursor. The following chords are also available
to us:

Keystrokes |     Effect
-----------|------------------------------------------
`<C-h>`    |     Delete back one character (backspace)
`<C-w>`    |     Delete back one word
`<C-u>`    |     Delete back to the start of line.

These commands are not unique to Insert mode or even Vim. We can also use them
in Vim's command line as well as in the bash shell.

