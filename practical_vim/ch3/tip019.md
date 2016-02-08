Tip 19: Overwrite Existing Text with Replace Mode
=================================================

_Replace mode is identical to Insert Mode, except that it overwrites existing
text in the document._

Suppose that we had an excerpt of text such as this:

```
insert_mode/replace.txt
Typing in Insert mode extends the line. But in Replace mode the line length
doesn't change.
```

Instead of using two separate sentences, we'te going to run this together into
a single sentence by changing the period to a comma. We also have to downcase
the "B" in the word "But." This example shows how we could do this using
Replace mode.

Keystrokes  | Buffer Contents
------------|----------------
`{start}`   | Typing in the Insert mode extends the line. But in Replace
            | mode the line length doesn't change.
`f.`        | Typing in the Insert mode extends the line. But in Repalce
            | mode the line length doesn't change.
`R, b<esc>`  | Typing in the Insert mode extends the line, but in Replace
            | mode the line length doesn't change.

From Normal mode, we can engate Replace mode with the `R` commands. As the
example demonstrates, typing `, b` overwirtes the existing ". B" characters.
And when we're finished with Replace mode, we can hit the `<esc>`key to return
to Normal mode. Not all keyboards have an `<Insert>` key, but if yours does,
then you can use it to gogle between Insert and Replace modes.


Overwrite Tab Characters with Virual Replace Mode.
--------------------------------------------------

Some characters can complicate matters for Replace mode. Consider the tab
character. This is represented by a single character in the file, but onscreen
it expands to fill several columns, as defined by the `tabstop` setting (see
`:h tapstop`). If we placed our cursor on a tab stop and initiated Replace
mode, then the next character we typed would overwrite the tab character.
Supposing that the `tabstop` option was set to 8 (the default), this would
appear to replace eight characters with one, causing a drastic reduction in the
length of the current line.

Vim has a second variant of Replace mode. _Virtual Replace mode_ is triggered
with `gR` and treats the tab character as though it consisted of spaces.
Suppose that we position the cursor on a tap stop spanning eight columns of
screen real estate. If we switch to Virtual Replace mode, we could type up to
seven characters, each of which would be inserted in front of the tab
character. Finally, if we typed an eighth character, it would replace the tab
stop.

In Virtual Replace mode, we overwrite characters of screen estate rather than
dealing with the actual characters that would eventually be saved in a file.
This tends to produce fewer surprises, so I would recommed using Virtual
Replace mode whenever possible.

Vim also provides a single-shot version of Replace mode and Virtual Replace
mode. The `r{char}` and `gr{char}` commands allow us to overwrite a single
character before switching straight back to Normal mode (`:h r`).


