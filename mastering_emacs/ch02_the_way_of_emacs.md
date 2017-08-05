# Chapter 2: The Way of Emacs #

> "The purpose of a windowing system is to put some amusing fluff
> around your one almighty emacs window." - Mark, _gnu.emacs.help_

if you imagine the span of the modern computing era beginning in the
1960s, then Emacs has been there longer than just about anything
else. It was first written by Richard Stallman as a set of macros on
top of another editor, called TECO, back in 1976. TESO is now mostly
remembered for being even more obtuse and hard to understand than
Emacs and DOS-era WordPerfect combined. Since then, there have been
many competing implementations of Emacs but today you're only likely
to encounter XEmacs and GNU Emacs.

This book will only concern ifself with GNU Emacs. Once upon a time
XEmacs was the more advanced and feature rich editor, but this is no
longer the case: from Emacs 22 onwards GNU Emacs is the best Emacs out
there. The history of XEmacs and GNU Emacs is an interesting one. It
was one of the first major forks in a free software project and both
XEmacs and GNU Emacs are developed in parallel to this day.

**Note** To almost everyone, the word _Emacs_ refers specifically to
  GNY Emacs. I will only spell out the full name when I am
  distingguishing between different implementations. When I mention
  _Emacs_, I always talk about GNU Emacs.

Because of Emacs's age there are a number of... oddities. Weird
choices of terminology and historical anachronisms persist because in
most cases Emacs was _ahead_ of the editor-IDE curve for many decades
and thus had to invent its own terminology for things. There are talks
of replacing Emacs's own vernacular with words familiar to everyone,
but that is still a long way off.

Despite the lack of marketing, a smal core of Emacs developers, the
anachronisms and terminology that predates the modern Personal
Computing-era, there are many people out there just _love using
Emacs_. When _Sublime Text_ showed off its mini-map feature (a
miniature display of the source code) someone immediately coded up a
minimap package doing the same thing in Emacs. In fact, it is this
extensibility that attracts some to - and repels others from - Emacs.

This chapter will talk about the _Way of Emacs_: the terminology and
what Emacs means to a lot of people, and why understanding where Emacs
comes form will make it easier to adopt it.


## Guilding Philosophy ##

Emacs is a tinkerer's editor. Plain and simple. People who hack on
Emacs do it because almost every facet of it is extensible. It is the
original extensible, customizable, self-documenting editor. If you
come from other text editors, the idea of being able to change
_anything_ may seem like an unnecessary distration from your work -
and indeed, a lot of Emacs hacking does happen at the expense of one's
real job - but once you relize that you can shape your editor to do
what _you_ want it to do, it opens up a world of possibilities.

That means you can trly rebind all of Emacs's keys to your liking; you
are not hidebound by your IDE's undocumented and buggy API nor the
limitations that would follow if you did change things - such as your
custom navigation keys not working in, say, the search & replace
window or in the internal help files. Truly, in Emacs, you can change
everything - and people do. Vim users are migrating to Emacs because,
well, Emacs is often a better Vim than Vim.

Emacs pulls you in. Once you start using Emacs for the editing, you
relize that using Emacs for IRC, email, databse access, command-line
shells, compiling your code or surfing the Internet is just as editing
text - and you get to keep your key bindings, theme and all the power
of Emacs and elisp to configure or alter the behavior of _everything_.

And when everything is seamlessly tied together you avoid the usual
context switches of going from application to applicatin: most Emacs
user use little more than the editor, a browser and maybe a dedicated
terminal application.

> **Emacs's history**
> Emacs's source code repository (not in Git) streches back over 30
> years and has more than 130000 commits and nearly 600 committers.

If you want to modify Emacs, or any of the myriad packages available
to you, _Emacs Lisp_ (also know informally as _elisp_) is what you
will have to write. There have been a few attempts to graft other
languages onto elisp and Emacs but with no lasting effect. As it turns
out, LISP is actually a perfect abstraction for a very advanted tool
like Emacs. And most modern languages wouldn't necessarily stand the
test of time: TCL was briefly considered in the 90s as it was popular
at the time - but that has the distinction of being even more obscure
than LISP, nowadays.

The only downside is that diffling with your Emacs configuration is
somehting you will have to learn to live with (and in LISP no less,
but as I explain in the next part that's actually a good thing.)
That's why I reinforced the point that it's a tinkerer's editor. If
you hate the idea of tweaking *anything* and wnat everything out of
the box, you have two options left:

**Use a starter kit** There are many free starter kits that come
  exuiqpped with additional packages and what the author thinks are
  sensible default sttings. They can be a good way to start out but
  with the caveat that you don't know where Emacs ends and the starter
  kits' added functionaility begins.

  I recommend you look at one of the following starter kits widely
  used:
  - Steve Purcel's _.emacs.d_
  - Bozhidar batzov's _Prelude_

**Use the defauls** Certainly an option but Emacs, I would say, is
  rather lacking out of the box. You are expected to configure Emacs
  to your liking or use a starter kit. For an exditor that is so
  radically different from mainstream editos, the maintainers are
  surprisingly conservative about changing the defaults for fear of
  upsettings the old guard (who, of all people, should know how to
  configure Emacs.)


## LIPS? ##

Emacs is powered by its own LISP implementation called _Emacs Lisp_ or
just *elisp*. Many are put off or intimidated by this esoteric
language; that's a shame, because it's a practical and fun way to
learn LISP in an editor built up around the idea of LISP. Every part
of Emacs can be inspected, evaluated or modified because the editor is
approximately 95 percent elisp and 5 percent C code. It's also a
practical way to learn a radical paradigm: that code and data are
interchangeable; that the language, owing to its simple syntax, is
trivially extensible with _macros_.

Unfortunately, there's no getting around learning elisp at some
point. In this book, I will talk about the _Customize_ interface: a
dynamically generated interface of customizable options in
Emacs. However, something as simple as rebinding a key means you'll
have to interact with elisp. But it's not all bad. Most of the
problems you're likely to encounter have already been solved by
someone else a long time ago; it's a simple matter of searching the
Internet for a solution to your problems.

Despite the relative unpopularity of elisp _versus_ more "modern"
language like Python, Ruby and JavaScript, I doubt Emacs would have
had the same power of extensibility if a more traditional
imperative/object-oriented language had been used. What makes LISP
such a fantastic language is that source code and data structures are
intrinsically one and the same: the LISP source code you read as a
human is almost identical to how the code is manipulated as a data
structure by LISP - the distinction between the questions "What is
data?" and "What is code?" are nil.

The data-as-code, the macro system and the ability to "advise"
arbitrary functions - meaning you can modify the behavior of existing
code without copying and modifying the original - give you an
unprecedented ability to alter Emacs to suit your needs. What would in
most software projects be considered code smells or poor architecture
is actually a major benefit in Emacs: you can hook, replace or alter
existing routines in Emacs to suit your needs without rewriting large
swathes of someone else's source code.

This book will not teach elisp in any great detail: Emacs has a
built-in elisp introduction and I highly recommend it if your are
curious - and honestly you should be. LISP is _fun_ and this is a
great way to learn and use a powerful language in a practical
environment. Don't let the parentheses scare you; they are actually
its greatest strength.


### Emacs as an Operating System ###

When you run Emacs you are in fact launching a tiny C core responsible
for the low-level interactions with your operating system's ABI. That
includes mundane things like file-system and network access; drawing
things to the screen or printing control codes to the terminal.

The cornerstone of Emacs though is the elisp interpreter - without it,
there is not Emacs. The interpreter is creaky and old; it's
struggling. Modern Emacs users expect a lot from their humble
interpreter: speed and asynchrony are the two main issue. The
interpreter runs in a single thread and intensive tasks will lock the
UI thread. But there are workarounds; the issues, manifold though they
are, do not deter people from writing ever-more sophisticated
packages.

When you write elisp you are not just writing snippets of code run in
a sandbox, isolated from everything - you are altering a living
system; an operating system running on an operating system. Every
variable you alter and every function you call is carried out by the
very same interpreter you use when you edit text.

Emacs is a hacker's dream because it is one giant, mutable state. Its
simplicity is both a blessing and a curse. You can re-define live
functions; change variables left and right; an you can query the system
for its state at any - state that changes with every key stoke as
Emacs responds to events from your keyboard to your network
stack. Emacs is self-documenting because it _is_ the document. There
are no other editors that can do that. No editor comes close.

And yet Emacs never crashes - not really, anyway. Emacs has an uptime
counter to prove that it doesn't (`M-x emacs-uptime`) - multi-month
uptimes are not uncommon.

So when you ask Emacs a question - as I will show you how to do
later - you are asking _your_ Emacs what _its_state is. Because of
this, Emacs has an excellent elisp debugger and unlimited access to
every facet of Emacs's own interpreter and state - so it has excellent
code completion too. Any time you encounter a LISP expression you can
tell Emacs to evaluate it, and it will: from adding numbers to
settings variables to downloading packages.


## Extensibility ##

Extensibility is important, but emphasizing that importance is
difficult if you don't know the scope of possibilities in Emacs. I've
included just a few examples of what Emacs can do - or more
importantly still, what Emacs can enable people to do - here.


**A speech interface for the blind** For 20 years, Emacspeak has
  offered blind or visually imparted Emacs users a way of interacting
  with Emacs, and the world, through a speed interface that
  understands the content of what appears on your screen. Emacspeak
  will change the voice characteristics of the speech engine to
  reflect different syntactic elements in source code, or to emphasize
  layout, fonts or graphical icons. For blind Emacs users, Emacspeak
  is a lifeline that has enabled them to continue working by using
  Emacs's many tools, such as e-mail or web browsing.

  The fact that this functionality has been around for 20 years is in
  itself impressive, but Emacs's ability to support this sort of
  transformational software is beyond inspiring.

**Remote file editing** Emacs's TRAMP seamlessly lets you edit remote
  files using a variety of network protocols, including SSH, FTP,
  rsync, and more, as though the files were local.

**Shell access** Emacs has a built-int ANSI-capable Terminal emulator;
  an Emacs wrapper around shells, such as bash; and a full-blown shell
  called _Eshell_ written entirely in elisp.

**ORG mode** A to-do, agenda, project planner, literate programming,
  note-taking (and more!) application. It is widely considered
  _the best text-based organizer ever_ a feat only surpassed by the
  fact that people _switch to Emacs just to use it_.

**And much more** Official or unofficial support for almost every
  programming environment; built-in man page and info reader; a very
  sophisticated directory and file manager; seamless support for
  almost every major version control system; and thousands of other
  features, large or small.


## Important Conventions ##

There are some important Emacs conventions that I need to talk about
before we continue. It's quite important that you memorize them or at
least refer back to this page if you're in doubt. They will crop up
again and again in the book and elsewhere and knowing them is
paramount if you want to make use of Emacs's extensive, internal
documentation. This is _not_ an exhaustive list of conventions used
in Emacs or even in this book. I will introduce specific terms and
concepts throughout the book though some terms transcend specific
topics and are therefore important to know beforehand.

### The Buffer ###

Most text editors and IDEs are file based: they display text from a
file, and they save the text _to_ a file. That's it.

In Emacs, all files are buffers, but not all  buffers are files. If
you want a throw-away are to temporarily store snippets from a log
file, or manipulate text, or whatever your reason - you just create
and name a new buffer. Emacs won't hassle you for a
filename. The buffer will exist in Emacs and only Emacs. You have to
explicitly save it to a file on disk to make it persist.

Emacs uses these buffers for more than just editing text. It can also
act like an I/O device and talk to another process, such as a shell
like *bash* or even *Python*.

Almost all of Emacs's own commands act on buffers. So when you tell
Emacs to, for example, search & replace it will _actually_ search and
replace on a buffer - maybe the active buffer you're writing in, or
perhaps a temporary duplicate - and not an internal data structure
like you might think. In Emacs, _the buffer is the data
structure_. This is an extremely powerful concept because the very same
commands you use to move around and edit in Emacs are almost always
the same ones you use behind-the-scenes in elisp. So once you
memorize Emacs's own user commands, you can use them in a simple
function call to mimic what you'd do by hand.

### The Window and the Frame ###

When you look at a buffer on the screen it is displayed in a
_window_. But in Emacs, a _window_ is just a tiled portion of the
*frame*, which is what most window managers call a window. In Emacs,
it is the other way around; and yes, it's very confusing.

If you look at the screenshot above, you will see _two windows_ and
_one_ frame. each frame can have one or more windows, and each window
can have *exactly* on buffer.

So, a buffer must be viewed in a _window_ in order to be displayed to
the user, and for the _window_ to be visible to the user it must be in
a frame.

**Note** Think of it as a physical window having a frame, each frame
made up of window panes.

In Emacs, you are free to create as many frames as you like, and in
each frame you're free to split and tile that frame into multiple
windows. If you use a large screen monitor (and who doesn't, these
days), it is very beneficial to use Emacs's tiling system to show
multiple buffers on the screen.


### Modeline, Echo Area, and Minibuffer ###

The figure above is an example of a Terminal Emacs session. Emacs uses
the modeline to communicate facts about Emacs and the buffer you're
in. The modeline looks like this:

```
-UUU:**--F3    *scratch*    All    L4   (Lisp Interaction) --
```

There's a lot of information conveyed in a fairly small area. What you
should care about to begin with are the _name_ and _modes_. In this
cae, the buffer is named `*scratch*`and the major mode is LISP
Interaction. Most editors have a similar concept known as a status
bar.

All sorts of optional information can be displayed in the modeline:
laptop battery power, the current function or class you're in, what
source control revision or branch you're using, and much more.

The minibuffer is directly below the modeline and it is where errors
and general information are shown.

In this case, I have triggered Emacs's _extended command_
functionality - indicated by the `M-x` symbol, a concept that I will
talk about in _the chapter on keys_ - and I've typed the command
`insert-hello-word` into the `M-x` prompt.

The echo area and the minibuffer share the same spot on the
screen. The minibuffer is nearly identical to a normal buffer: you
can use most of your editing commands, and the oneline minibuffer will
expand to multiple lines if necessary. It is how you communicate with
Emacs: if you want to search for a string you write the string you
want to search for in the minibuffer. It supports a variety of
complex completion mechanisms to hep you find what you need and is a
tool you will use often.
