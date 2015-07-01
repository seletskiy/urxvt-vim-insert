Try to insert following text into your fully configured vim using `Shift-Insert`:

```
{
    {
        {
            # madness!
        }
    }
}
```

Then, compare with following gif.

![gif](https://cloud.githubusercontent.com/assets/674812/5927093/15b527c6-a692-11e4-85c1-fbe4a49c4ebc.gif)


You can use Shift+Insert now
============================

How many times you do following sequence in vim?

```
<C-O>"*p
```

Or, if you smart one, this one?

```
<C-R>*
```

However, remote vim leaves you no choice.

```
:set paste
<S-Insert>
:set nopaste
```

urxvt-vim-insert into the rescue
================================

Just install this urxvt perl plugin, restart urxvt and all following
Shift-Inserts will paste text as it expected to be done in XXI century.

It will also work onto remote server vim. Waow.


How about pasting multiline text directly into the shell?
=========================================================

Seen this site?

http://thejh.net/misc/website-terminal-copy-paste

Your browser will happily copy any hidden text into clipboard, and guess what
happens if you paste some hidden text that contains `rm -rf /usr/` into terminal
on the production server? :peach:

Hopefully, there is a solution.

## :tada: TADA! :tada:
![tada](https://cloud.githubusercontent.com/assets/674812/8426710/6d059906-1f01-11e5-8000-ba3a470630c1.gif)

Also, you need to specify program, that will be used to edit clipboard and send
result back.

This command is specified via `URxvt.safe-paste.command` param. See more in the
next section.

For example, I'm using setup with urxvt+tmux+vim, so my safe-paste command is:

```
URxvt.safe-paste.command: vim-safe-paste
```

`vim-safe-paste`:

```sh
tmux_pid=$(pgrep -P$1 tmux)
session_name=$(grep -zFxA1 -- '-s' < /proc/$tmux_pid/cmdline | cut -b3-)

tmux neww -t $session_name "$(cat <<EOF
    $EDITOR $2;
    tmux loadb $2 \; pasteb -t $session_name:-1 ;
    rm $2 ;
EOF
)"
```

Little bit complicated (due stupid tmux API). When I will press `Shift+Insert`
to paste something not into vim and clipboard contains more than one line, it
will popup new vim instance with clipboard contents, so I can edit it before
pasting.

Result of using that simple script can be seen on the gif above.

### URxvt.safe-paste.command

This parameter is mandatory and should point on the executable, that will be
launched by urxvt **synchronously**, so it should fork to not to hang your
terminal.

That executable will get two parameters:

* urxvt PID for the first parameter (`$1`).
* temporary file name with current clipboard contents as it's second parameter
  (`$2`). This file should be removed by executable when editing is complete.

Installation
============

Under archlinux, just install package from
[AUR](https://aur.archlinux.org/packages/urxvt-vim-insert/).

Under any other distro, just copy [vim-insert](vim-insert) into rxvt-unicode
extensions directory.

Then, add `vim-insert` at the end of the `URxvt.perl-ext-common` list:

``` URxvt.perl-ext-common: ...,vim-insert ```


Integration
===========

This plugin plays nice with other things:

* [marvex](https://github.com/reconquest/marvex), which is a terminal
  bookkeeper for tile window manager called i3.

* [mcabber-external-editor](https://github.com/kovetskiy/mcabber-external-editor),
  which is a missing feature of editing multiline messages in mcabber.

  `safe-paste.command` script, located in the `example/` directory is designed
  to work with `marvex` and `mcabber-external-editor`.
