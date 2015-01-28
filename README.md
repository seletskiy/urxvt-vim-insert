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

Installation
============

Under archlinux, just install package from
[AUR](https://aur.archlinux.org/packages/urxvt-vim-insert/).

Under any other distro, just copy [vim-insert](vim-insert) into rxvt-unicode extensions directory.
