on-parens
=========

What is it?
-----------

A wrapper for smart-parens to give smart-parens/paredit style commands for use
in evil-normal-state.

Why?
----

In vi/vim/evil-mode in normal-state, the cursor is viewed as being
ON a character rather than BETWEEN characters.  This breaks
smartparens particularly when it tries to put you past the last
character of the line, since normal-state will push point back one
character so it can be viewed as on the last character rather than
past it.  Additionally, most vim/evil movements go to the beginning
of a text object, with an alternative version that goes to the end.
Emacs tends to go past the end of things when it goes forward, but
to the beginning when it goes back.

This provides movements for normal-state that go forward and back
to specifically the beginning or end of sexps, as well as up or
down.

Commands
--------

For movement we have:

- on-parens-forward-sexp
- on-parens-forward-sexp-end
- on-parens-backward-sexp
- on-parens-backward-sexp-end
- on-parens-up-sexp
- on-parens-up-sexp-end
- on-parens-down-sexp
- on-parens-down-sexp-end
- on-parens-forward-sexp-in-supersexp
- on-parens-backward-sexp-in-supersexp

Editing commands:

- on-parens-forward-slurp
- on-parens-forward-barf
- on-parens-backward-slurp
- on-parens-backward-barf
- on-parens-splice
- on-parens-split-supersexp
- on-parens-join-neighbor-sexp
- on-parens-kill-sexp

The editing commands probably do what you expect, they only differ
from smartparens in which sexp they operate on when run on top of an
opening or closing delimiter.  `on-parens-kill-sexp` is actually
pretty useless in normal state, because we have
`d<your keybinding for on-parens-forward-sexp here>`, just like we would
use `dw`.  Numeric arguments work as expected.

Issues
------

There may be some, since I hacked this together really quickly because I was
sick of not using paredit or smartparens because I also love vim-style modal
editing.

Recommendations
---------------

Use this with
[emacs-repeatable-motion](https://github.com/willghatch/emacs-repeatable-motion)
to get repeatable versions, bind the repeat command to a single key, and the
movement commands to a two-key combo.

License
-------

GPLv3+

Enjoy
-----
