EmacsUtils
==========

Handy Emacs utilities

I've been using Gnu Emacs since it was publicly available (1985?), and have contributed some packages which are included with Emacs, notably the [Allout outliner](http://myriadicity.net/software-and-systems/craft/emacs-allout), [icomplete mode](http://www.emacswiki.org/emacs/IcompleteMode), and python-mode's [pdbtrack functionality](http://myriadicity.net/software-and-systems/craft/crafty-hacks#section-1). Like many long-time Emacs users, I've use some custom code, some of which I wouldn't do without. Here's a few items that I particularly like, and think might be useful to others - I hope to include more, as time allows.

* **[poptoshell.el](./poptoshell.el)**

  I use the emacs shell a lot. I bind this to Meta-space to make it easy to:

    * Return to the current primary shell, in an alternate window
    * When within a shell buffer, get to the input prompt
    * Start alternate shells, and easily choose between any that are going:
      * With one universal argument, prompt for the name of the shell
      * with completion on existing names,
      * and new names to start a new shells.
    * Prefix names of new shells with paths, to specify starting directory
    * For a remote shell, use tramp-style remote path!
      * Without an explicit name following the last slash, the host name is
        used as the shell name. But the trailing name makes it easy to
        distinguish, eg, root shells: `/ssh:myserver.net|sudo:root@myserver.net:/#myserver`
      * Since the shell's current directory is used by default:
        * If the remote shell has been disconnected, it's reconnected by default, in the same directory where you left off
          * (So I exit remote shells I'm done with, but keep the buffers around - I just resume by Meta-space <shell-name>.)
        * Visiting files from a remote shell buffer visits relative to the remote host!
    * Change which shell is the session default by using a doubled
      universal argument.
      * Handy for a kind of current-project modality, easily changing
        which shell is the default as you change project focus.

* **[xsel.el](./xsel.el)**

  X copy and paste emacs region from emacs tty sessions, using a shell command.

  If xsel or linux or cygwin equivalent is installed, and DISPLAY is
  working, use `klm:xsel-copy` to copy the region to the X clipboard and
  `klm:xsel-paste` to paste the contents of the clipboard at point.

  One benefit is that `klm:xsel-paste` pastes are single units, rather than
  a sequence of individual keystrokes that constitute regular X pastes to a
  terminal. This avoids layers of parsing, indenting, auto-paren insertion,
  and so forth. (You can always do a regular X paste on occasions when you
  want that processing.)

* **[pdbtrack.el](./pdbtrack.el)**

  [I've moved my standalone version of pdbtrack aside. I hadn't realized 
  that the version that I derived this code from lacks my source-buffer 
  fallback provisions. It looks like I'm going to have to do some
  unraveling to reconstruct the best basis.]

  Add sensitivity to comint shells so the source file lines are automatically
  presented in a separate window when the Python PDB debugger steps to them.

  This is derived from the pdb tracking code, which I originally wrote, and
  which has been included in (various) official Emacs Python modes. I wanted
  a version that I could more easily tweak and maintain, independently of
  the python-mode code.

  It would be nice to eventually generalize this code, to work for things
  like the node.js debugger. We'll see if I (or anyone) ever gets around to
  that.
