[![MELPA](http://melpa.org/packages/on-parens-badge.svg)](http://melpa.org/#/on-parens)

on-parens
=========

A wrapper for [smartparens](https://github.com/Fuco1/smartparens) to
give smartparens/paredit style commands for use in evil-normal-state.

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

As far as on-paren commands are concerned, if you are on a paren, you
are on that sexp, and not in it.  Therefore, `on-parens-forward-sexp`
will put you on the next open paren, open string delimiter, or start
of symbol on the same level.  `on-parens-up-sexp-end` will put you on
the close paren of the sexp you were inside of, etc.  () is an empty
list, so clearly your cursor isn't in it, it is on it.

These movements also make various insertion and deletion commands
convenient -- inserting at the start of the current level is
`<on-parens-up-sexp>a`, appending at the end of the current level is
`<on-parens-up-sexp-end>i`.  Deleting a balanced sexp on the current
level is `d<on-parens-forward-sexp>`.  Deleting to the end of the
level is `d<on-parens-up-sexp-end>`.

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

It doesn't play with strings as nicely -- some of the movement
commands get confused when run in strings.  There may be other issues
-- frankly I threw this together quickly just to get the functionality
for myself, and I employed a few hacks.  All the real legwork is done
in smartparens, however, so there is some mature code underneath this
plugin.  This plugin is mostly to alter the functionality of annoying
corner cases where the philosophies of emacs and vim/evil butt heads.

Recommendations
---------------

- Use this with
[emacs-repeatable-motion](https://github.com/willghatch/emacs-repeatable-motion)
to get repeatable versions, bind the repeat command to a single key,
and the movement commands to a two-key combo.  Also, since I already
had the framework in repeatable-motion to declare the motions with the
proper inclusivity for evil-mode, I didn't do that in this plugin (it
doesn't make a huge difference, but it's nice to have it working
right).
- I recommend adding
[evil-surround](https://github.com/timcharper/evil-surround) to deal
with wrapping expressions or the region in parens, or changing the
type of delimiter things are wrapped in.
- If you want to keep `dd`,
`D`, etc from killing your paren balance, you can try
[evil-smartparens](https://github.com/expez/evil-smartparens), which
does checking on such commands to be sure they play nice with the
parens.  Alternatively, instead of `D` you can use
`d<on-parens-up-sexp>` to accomplish the same, and still have `D`
around (sometimes obliterating paren balance and rebuilding can just
be easier, so it's nice to have the normal functionality too).

Install
-------

Install from Melpa or clone this repo into your load path and run
`(require 'on-parens)` in your initialization.

License
-------

GPLv3+

Enjoy
-----
