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

![gif](https://cloud.githubusercontent.com/assets/674812/5926281/bcae01a8-a68b-11e4-9aef-3299189185ca.gif)

You can use Shift+Insert now
============================

How many times you do following sequence in vim?

```
<C-O>"*p
```

Or, even worse, this one?

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

Installation
============

Under archlinux, just install package from
[AUR](https://aur.archlinux.org/packages/urxvt-vim-insert/).

Under any other distro, just copy [vim-insert](vim-insert) into rxvt-unicode extensions directory.
