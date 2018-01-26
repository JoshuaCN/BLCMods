Apocalyptech's Borderlands 2 Mod(s)
===================================

BL2 Better Loot Mod
-------------------

At the moment, this is my only mod in here.  Its general goal is to make
loot drops in Borderlands 2 "better", as in skewing very much towards the
rarer loot.  Legendaries/Uniques/Pearls/Seraphs will drop far more
frequently than they do in vanilla B2, etc.

It's essentially a cheat mod, intended for those BL2 players like myself who
tend to play in Normal most of the time, dislike grinding, get bored easily by
the uninteresting and drab loot that typically gets dropped in-game, and who
often ends up just resorting to Gibbed to be able to play around with some
better gear.  The README in the mod dir itself should provide a lot more info.

Utilities
=========

The statements used in Borderlands mod files are often fairly gigantic, and
difficult to understand quickly without loading them into a text editor and
inserting a bunch of linebreaks to get a feel for the overall structure.
Then if you want to *edit* those structures, you'd have to undo all the
linebreaks, or just make do with editing the middle of the gigantic strings.

Well, I figured to hell with that, and wrote a couple of quick-n-dirty
utilities in Python to automate that kind of thing for me, so I could edit
to my heart's content in a format which was easy to deal with, and then just
export to the "real" version which Borderlands / FilterTool can understand.

Both of these utilities are written in Python, and probably require Python 3.
They're intended to just be run from a commandline, which may pose some
logistical problems for folks on Windows/Mac who may not be used to doing that.
(Also, Python probably isn't already installed by default on those platforms.)
Folks running Linux, like myself, should be able to just run 'em as per usual
from a terminal.

Also note that neither of these utilities attempt to process any hotfix-style
mods - they only really support the more straightforward "`set`" style patches.
Both *should* be nice and leave hotfix lines alone, though be sure to
doublecheck the output if you use them on any files with hotfixes in 'em.

conv_to_human.py
----------------

This utility can take an existing Borderlands patch/mod file, or the output
from an `obj dump <foo>` from the Borderlands console, and convert it into a
much easier-to-read-and-edit multiline file.  For instance, if you've got a
file which contains the following:

    BalancedItems(0)=(ItmPoolDefinition=None,InvBalanceDefinition=InventoryBalanceDefinition'GD_Artifacts.A_Item.A_Vitality_Rare',Probability=(BaseValueConstant=1.000000,BaseValueAttribute=None,InitializationDefinition=None,BaseValueScaleConstant=1.000000),bDropOnDeath=True)

... this utility would convert it to something like:

    BalancedItems(
        0
    )=(
        ItmPoolDefinition=None,
        InvBalanceDefinition=InventoryBalanceDefinition'GD_Artifacts.A_Item.A_Vitality_Rare',
        Probability=(
            BaseValueConstant=1.000000,
            BaseValueAttribute=None,
            InitializationDefinition=None,
            BaseValueScaleConstant=1.000000
        ),
        bDropOnDeath=True
    )

Much nicer!  For instance, to convert the main UCP patch to something more
readable, you could do:

    $ ./conv_to_human.py Patch.txt Patch-unpacked.txt

Or whatever.  If you don't specify any filenames, this util will read/write
to STDIN/STDOUT.  You an also use `-` as either of the filenames, if you
wanted to use STDIN/STDOUT for one end but not the other.

The utility will ask you to overwrite the output file, if it's specified and
already exists.  You can use the `-f` or `--force` option to automatically
overwrite without confirmation.  You can also use `-h` or `--help` as you'd
hope, though there's no features not already mentioned here.

conv_to_mod.py
--------------

Conversely, this is the utility to turn one of those nicely-human-editable
files into something which Borderlands/FilterTool can understand.  It'll just
do the reverse of `conv_to_human.py`.

Unlike `conv_to_human.py`, this utility will not read from STDIN/STDOUT,
enforces some conventions about the filenames being used, and only accepts a
single filename in the argument list.  The source file it reads from is required
to have a suffix of `-source.txt`, so for instance my own Better Lood Mod source
filename is `BL2 Better Loot Mod by Apocalyptech-source.txt`.

The destination file it uses will be identical to the source filename, minus the
`-source.txt` suffix, so for my own mod, the output filename will be plain ol'
`BL2 Better Loot Mod by Apocalyptech`.

For the filename argument, you can specify either the source or destination file,
and the utility will figure out which one you mean.  So, the following two
commands will do the exact same thing:

    $ ./conv_to_mod.py "BL2 Better Loot Mod by Apocalyptech-source.txt"
    $ ./conv_to_mod.py "BL2 Better Loot Mod by Apocalyptech"

In general I just tab-complete and whichever gets picked works fine.

As with `conv_to_human.py`, this will ask you to overwrite the destination file,
if it already exists.  You can use the `-f` or `--force` option to automatically
overwrite without confirmation.  You can also use `-h` or `--help` as you'd hope,
though there's no features not already mentioned here.

Resources
=========

This directory contains a couple of text files which is mostly just the output
from various `obj dump <foo>` commands for classes/objects I was interested in
modding.