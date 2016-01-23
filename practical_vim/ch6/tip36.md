Tip 36: Track Open Files with the Buffer List 
==============================================

_We can load multiple files during an editing session. Vim lets us manage them
using the buffer list._


Understand the Distinction Between Files and Buffers
-----------------------------------------------------

Just like any other text editor, Vim allows us to read files, edit them, and
save our changes. When we discuss our work flow, it's tempting to say that we're
editing a file, but that's not what we're actually doing. Instead, we're
editing an in-memory representation of a file, which is called a _buffer_ in
Vim's terminology. 

Files are stored on the disk, whereas buffers exist in memory. When we open a
file in Vim, its contents are read into a buffer, which takes the same name as
the file. Initially, the contents of the buffer will be identical to those of
the file, but the two will diverge as we make changes to the buffer. If we
decide that we want to keep our changes, we can write the contents of the buffer
back into the file. Most Vim commands operate on buffers, but a few operate on
files, including the `:write`, `:update`, and `"saveas` commands.


Meet the Buffer List
--------------------

Vim allows us to work with multiple buffers simultaneously. Let's open a few
files by running these commands in the shell:

```
cd code/files
vim *.txt
```

The `*.txt` wildcard matches two files in the current directory: `a.txt` and
`b.txt`. This command tells Vim to open both of those files. When Vim starts
up, it shows a single window with a buffer representing the first of the two
files. The other file isn't visible, but has been loaded into a buffer in the
background, as we can see be running the following:

```
:ls 
1 %a    "a.txt"                         line 1
2       "b.txt"                         line 0
```

The `:ls` command gives us a listing of all the buffers that have been loaded
into memory (`:h :ls`). We can switch to the next buffer in the list by
running the `:bnext` command:

```
:bnext
:ls
1 #     "a.txt"                         line 1
1 %a    "b.txt"                         line 1
```

The `%` symbol indicates which of the buffers is the visible in the current
window, while the `#` symbol represents the alternate file by pressing `<C-^>`.
Press it once, and we'll switch to `a.txt`; press it a second time, and we'll
get back to `b.txt`.


Use the Buffer List
-------------------

We can traverse the buffer list using four commands - `:bprev` and `:bnext` to
move backward and forward one at a time, and `:bfirs` and `:blast` to jump to
the start or end of the list. It's a good idea to map them to something easier
to reach. 

See Create Mapping to Quickly Traverse Vim's List, on page 79, for a
suggested mapping.

The `:ls` listing starts with a digit, which is assigned to each buffer
automatically on creation. We can jump directly to a buffer by number, using
the `:buffer N` command (see `:h :b`). Alternatively, we can use the more
intuitive form, `:buffer {bufname}`. The `{bufname}` need only contain enough
characters from the file path to uniquely identity the buffer. If we enter a
string that matches more than one of the items in the buffer list, we can use
tab-completion to choose between the options (see Tip 32, on page 65).

The `:bufdo` command allows us to execute an Ex command in all of the buffers
listed by `:ls` (`:h :bufdo`). In practice, I usually find that it's more
practical to use `:argdo` instead, which we'll meet in Tip 37, on page 80.


> Create Mappings to Quickly Traverse Vim's Lists
> -----------------------------------------------
> 
> Typing `:bn` and `:bp` can feel laborious. To speed things up a bit, I use
> these mappings from Tim Pope's umimpaired.vim plugin:
> 
> ```
> nnoremap <silent> [b :bprevious<CR>
> nnoremap <silent> ]b :bnext<CR>
> nnoremap <silent> [B :bfirst<CR>
> nnoremap <silent> ]b :blast<CR>
> ```
> 
> vim already uses the `[` and `]` keys as prefixes for a series of related
> commands (see `:h`), so these mappings have a consistent feel to them. The
> unimpaired.vim plugin provides similar mappings for scrolling through the
> argument (`[` and `]`), quick fix (`[q` and `]q`), location (`[l` and `]l`),
> and tag lists (`[t` and `]t`). Check it out.
> 
> https://github.com/tpope/vim-unimpaired


Deleting Buffers
----------------

Vim creates a new buffer any time we open a file, and we'll learn a few ways of
doing that in Chapter 7, Open Files and Save Them to Disk, on page 93. If we
want to delete a buffer, we can do so using the `:bdlelete` command. This
can take one of these forms:

```
:bdelete N1 N2 N3
:N,M bdelete
```

Note that deleting a buffer has no effect on its associated file; it simply
removes the in-memory representation. If we wanted to delete buffers numbered 5
through 10 inclusive, we could do so by running `:5,10 bd`. But if we wanted to
keep buffer number 8, then we'd insted have to run `:bd 5 6 7 9 10`.

Buffer numbers are automatically assigned by Vim, and we have no means of
changing them by hand. So if we want to delete one or more buffers,  we first
have to look them up to find out their numbers. This procedure is relatively
time-consuming. Unless I have a good reason to delete a buffer, I usually don't
bother. As a result, the `:ls` listing comes to represent all of the files that
I have opened in the course of an editing session.

Vim's built-in controls for managing the buffer list lack flexibility. If we
want to arranage buffers in way that makes sense for our work flow, attempting
to organize the buffer list is not the way to go. Instead, we're better off
diviing our workspace using split windows, tab pages, or the argument list. The
next few tips will show how.
