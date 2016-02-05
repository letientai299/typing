Meet the Dot Command
====================

_The dot command let us repeat the last change. It is the most powerful and
versatile command in Vim._


Vim's documentation simply states that the dot command "repeats the last
change" (see `:h .`). It doesn't sound like much, but in that simple definition
we'll find the kernel of what makes Vim's modal editing model so effective.
First we have to ask, "What is a change?"

To understand the power of the dot command, we have to realize that the "last
change" could be one of many things. A change could act at the level of
individual characters, entire lines, or even the whole file.

To demonstrate, we'll use this snippet of text:

```
the_vim_way/0_mechanics.txt
---------------------------
Line one
Line two
Line three
Line four
```

The `x` command deletes the character under the cursor. When we use the dot
command in this context, "repeat last change" tells Vim to delete the character
under the cursor:



