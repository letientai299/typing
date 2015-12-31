Tip 31: Repeat the Last Ex Command
==================================

_While the `.` command can be used to repeat our most recent Normal mode
command, we have to use `@:` instead if we want to repeat the last Ex command.
Knowing how to reverse the last command iis always useful, so we'll consider
that, too, in our discussion._

In Chapter 1, The Vim way, on page 1, we saw how the `.` command can be used to
repeat the last change. But the dot command won't replay changes made from
Vim's command line. Instead, we can repeat the last Ex command by pressing `@:`
(see `:h @:`).

For example, this command can be useful when iterating through items in the
buffer list. We can step forward through the list with the `:bn` command and
backward with the `:bp` command (Tip 36, on page 77, discusses the buffer list
in more detail). Suppose that we had a dozen or so items in the buffer list,
and we wanted to take a look at each one of them. We could type this command
once: `:bnext`

Then we use the `@:` to repeat the command. Note the similarity between this
and the method for executing a macro (Play back a sequence of commands by
executing a macro, on page 159). Also note that the `:` register always holds
the most recently executed command line (see `:h quote_:`). After running `@:`
for the first time, we can subsequently repeat it with the `@@` command.

Suppose that we got trigger-happy and fired `@:` command too many times,
overshooting our mark. How would we change direction then? We could execute the
`:bp` command. But think about what would happen if we were to use the `@:`
command again. It would go backward through the buffer list, which is the exact
opposite of what it did before. That could be confusing.

In this case, a better option would be to use the `<c-o>` command (see Tip 55,
on page 131). Each time we run `:bn` (or repeat it with the `@:` command), it
adds a record to the jump list. The `<c-o>` command goes back to the previous
record in the jump list.

We could run `:bn` once and then repeat it as often as we like using the `@:`
command. If we needed to back up, we could do so using `<c-o>` command. Then,
if we wanted to continue going forward through the buffer list, we could go
back to using the `@:` command. Remember our mantra from Tip 4, one page 8,
act, repeat, reverse.

Vim provides an Ex command for just about everything. While it's always
possible to repeat the last Ex command by pressing `@:`, it's not always
straightforward to reverse the effects. The `<c-o>` trick covered in this tip
also works for reversing the effects on `:next`, `:cnext`, and `:tnext` commands
(and so on). Whereas, for each of the items in Table  9, Ex Commands That
Operate on the Text in a Buffer, on page 52, we could undo their effects by
pressing `u`.
