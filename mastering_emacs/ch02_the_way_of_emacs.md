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
