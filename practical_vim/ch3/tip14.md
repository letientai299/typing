Tip 14: Get Back to Normal Mode
===============================

_Insert mode is specialized for one task - Entering text - whereas Normal mode
is where we spend most of our time (as the name suggests). So it's immportant
to be abl eto switch quickly between them. This tip demonstrates a couple of
tricks that reduce the friction of mode switching._

The classic way of getting back to Normal mode is with the `<esc>` key, but on
many keyboards that can seem like a long reach. Alternatively, we can press
`<C-[>`, which has exactly the same effect (see `:h i_Ctrl-[`)

Keystrokes    |  Effect
--------------|------------------------------
`<esc>`       |  Switch to Normal mode
`<c-[>`       |  Switch to Normal mode
`<c-o>`       |  Switch to Insert Normal mode

Vim novices frequently become fatigued by the constant need to switch modes,
but with practice it starts to feel more natural. Vim's modal nature can feel
awkward in one particular scenario: when we're in Insert mode and we want to
run only one Normal command and then continue where we left off in Insert mode.
Vim has neat solution to ease the friction caused by switching modes: _Insert
Normal mode_.

Here's an unfinished excerpt of text:

```
insert_mode/practical-vim.txt
Practical vim, by Drew Neil
Read Drew Neil's
```

> Remap the Caps Lock key -----------------------
>
> For Vim users, the Caps Lock key is a  menace. If Caps Lock is engaged and
> you try using the k and j keys to move the cursor around, you'll instead
> trigger the K and J commands. Briefly: K looks up the man page for the word
> under the cursor and J joins the current and next lines together. It's
> surprising how quickly you can mangle the text in your buffer by accidentally
> enabling the Caps Lock key!
>
> Many Vim users remaps the Caps Lock button to make it act like another key,
> such as `<esc>` or `<ctrl>`. ON modern keyboards, the `<esc>` key is
> difficult to reach, whereas the Caps lock key is handy. Mapping Caps Lock to
> behave as an `<esc>` key can save a lot of effort, especially since the
> `<esc>` key is so heavily used in Vim. I prefer to map the Caps Lock button
> to behave instead as `<ctrl>` key. The `<c-[>` mapping is synonymous with
> `<esc>`, and it's easier to type when the `<ctrl>` key is within easy reach.
> Additionally, the `<ctrl>` key can be used for many other mappings, both in
> Vim and other programs too.
>
> The simplest way to remap the Caps Lock key is to do it at the system level.
> The methods differ on OS X, Linux and Windows, so rather than reproducing
> instructions here for each system, I suggest that you consult Google. Note
> that this customization won't just affect Vim: it applies system-wide. If you
> take my advice, you'll throw away the Caps Lock key forever. You won't miss
> it. I promise.

We want to complete the last line by inserting the title of this book. Since
that text is already present at the start of the first line, we'll yank it into
a register and then append the text at the end of the next line in insert mode.

The command `yt,` yanks the words Practical Vim into the yank register (we'll
meet the `t{char}` motion in Tip 49, on page 114). In Insert mode, we can press
`<c-r>0` to paste the text that we just yanked at the current cursor position.
We'll discuss registers and the yank operation at greater length in Chapter 10,
Copy and Paste, on page 141.

The general format of the command  is `<c-r>{register}`, where `{register}` is
the address of the register we want to insert.

Use `<c-r>{register}` for Character-wise Registers
--------------------------------------------------

The `<c-r>{register}` command is convenient for pasting a few words from Insert
ode. If the register contains a lot of text, you might notice a slight delay
before the screen updates. That's because Vim inserts the text from the
register as if it were being typed one character at a time. If the `textwidth`
or `autoindent` options are enabled, you might end up unwanted line breaks or
extra indentation.

The `<c-r><c-p>{register}` command is smarter. It inserts text literally and
fixes any unintended indentation. But it's a bit of a handful! If I want to
paste a register containing multiple line of text, I prefer to switch to Normal
mode and use one of the put commands (see Tip 62, on page 151).
