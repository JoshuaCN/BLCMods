BL2 Better Loot Mod by Apocalyptech
===================================

This mod aims to make loot in Borderlands 2 "better" in general.  It's
essentially a cheat mod, intended for those BL2 players like myself who
tend to play in Normal most of the time, dislike grinding, get bored easily
by the uninteresting and drab loot that typically gets dropped in-game, and
who often ends up just resorting to Gibbed to be able to play around with
some better gear.  The goal, personally, was to get the loot drops in-game
to a point where I never felt tempted to open up Gibbed.

This patch is set up to play nicely with FilterTool, and basically
everything in here can be toggled on or off inside FilterTool as you'd
hope, on an item-by-item basis.  Basically every bullet point in here is
its own "folder" once imported into FilterTool.

To add this mod to FilterTool, use the base file
`BL2 Better Loot Mod by Apocalyptech` (without any extensions, etc).  You
could alternatively rename that file to anything more easy-to-type in the
console, and then just `exec <filename>` from the console to load it on its
own.  It works quite well by itself.

Mod Overview
------------

Specifically, this mod does the following:

* Adds all legendaries/uniques/pearls/seraph items (weapons, grenade mods,
  class mods, shields, relics) into the global "legendary" loot pools, so
  you'll start seeing those much more frequently.
* Loot will skew much more rare, in general.  You should expect to see
  those legendaries/uniques/pearls/seraphs far more frequently than in
  vanilla BL2.
* "Regular" treasure chests will always provide at least blue-rarity gear,
  and has a decent chance of including stuff from the legendary pools.
* "Epic" treasure chests have an extremely high probability of dropping
  from the legendary pools.
* When lockers spawn gear, they will always be blue-rarity.  *(Previously
  lockers had a chance to spawn even legendaries, so some could potentially
  see this as a drawback)*
* Adds the "Alignment" Class Mods from the Dragon Keep DLC into the global
  Class Mod drop pools (and makes those COMs always drop at at least blue
  rarity).
* Adds Gemstone-rarity weapons into the E-Tech weapon pools.
* Omits Darts, Spikers, and Bandit BlASSters from the E-Tech pools.  *(I
  suspect this might annoy some folks; I could be convinced to put those
  back in)*
* Makes Eridium drop 3x more often
* Bosses are guaranteed to drop their legendaries/uniques
  * If a boss has more than one legendary/unique in their drop pool, they
    are guaranteed to drop that many items.  You may get duplicates rather
    than one of each, of course, but there's at least a chance to get all
    of them.
  * Normalized the chances of boss-item drops, for the handful of bosses
    whose loot probabilities weren't already equal.
* Remove early-game loot restrictions.  This is actually a superset of the
  similar feature already present in UCP 4.0.  The additions here are that
  both Relics and Class Mods will spawn from the beginning, as well.  Both
  this and the UCP 4.0 "Remove Loot restriction in the beginning areas"
  mods can be active at the same time with no ill effects -- it'll just
  mean that the relevant commands get executed twice.  Note that if you
  *don't* have either this or UCP enabled on your game, the early game will
  end up dropping *no* gear, due to our rarity changes.
* Optionally, I've left in some statements which cause all enemies to
  always drop gear, and always drop five items rather than just one.  This
  is disabled by default and would have to be enabled manually via FilterTool
  -- I'd basically just been using them to test out my custom loot pools by
  having a larger sample size.

Compatibility
-------------

As far as I know, this is totally compatible with UCP 4.0, and won't overwrite
anything that's done in there, though I have yet to do a thorough
look to make sure.  One possible source of conflicts with UCP would be in
UCP's "Specific Loot Changes" folder.  I'll be looking into that in a bit.

Obviously this will conflict with other mods which play with the same
variables.  I know that Hemaxhu's "Better White Chests" would conflict with
this, for instance, and possibly other mods in Hemaxhu's "Chest Mods"
folder.  FromDarkHell's collection in the "Loot Drops" folder likewise will
probably conflict.

In terms of loot compatibility, I'm pretty sure that this mod makes the
"Vault Hunter's Relic" completely useless, but if you're using this mod,
you certainly won't miss it.

Loot Purposefully Excluded from Pools
-------------------------------------

There's some gear which I felt shouldn't be in the pools at all.  I am
quite willing to hear counterarguments; my mind could probably be pretty
easily persuaded otherwise if someone feels strongly about it.

* Lame (IMO) E-Tech gear:
  * Darts
  * Spikers
  * Bandit BlASSters
* Cracked Sash (Shield)
* GOTY/Preorder/Whatever starting game loot:
  * "Gearbox" themed guns (AR/SMG/Sniper)
  * Contraband Sky Rocket
  * Vault Hunter's Relic
* Captain Blade's Midnight Star
* Blue-rarity Magic Missile *(purple rarity will still spawn -- they're
  technically different items)*
* Possibly one or two other guns as well -- I didn't think to keep track at
  first.

TODO
----

* Test interactions with UCP - make sure we're not stepping on any toes.
* Balancing!  This mod is obviously very cheaty/OP, but I don't want it to
  be completely ludicrous.  I'd like it to still feel a bit special when
  the Very Good loot gets dropped, while at the same time providing a steady
  supply of fun gear.  Obviously this is very much down to personal
  preference.  Regardless, I've done extremely little actual playtesting
  with the current drop weights.
* Boss drop counts for DLC bosses
* Can we increase boss drop counts depending on player count?
* I'm not actually terribly interested in changing this, but I'd love to
  know how the gear is allocated for the miscellaneous smaller containers
  throughout the game, such as those regular "white" chests (which
  more often than not just have ammo), cardboard boxes, washing machines,
  toilets, etc.  Nothing I've found seems to affect them.  Given the rest
  of what this mod does, it hardly matters, but my curiosity remains
  piqued.  I do know how to update dumpsters, but I left them alone on
  purpose.

Mod Construction / Implementation Details
-----------------------------------------

I actually generate this mod using a simple little Python script named
`generate-source.py`, which enables me to do things like set the rarity
drop levels from a single location at the top of the file, and have it
apply to a number of different objects throughout the game.  That script
outputs to a very human-readable multiline text file which can't actually
be read directly by FilterTool/Borderlands, and must then be processed by
my `conv_to_mod.py` script which you'll find in the parent directory.

To generate the end result file, I actually run the small shell script
`create.sh` in this directory, which just does the following:

    ./generate-source.py && ../conv_to_mod.py -f "BL2 Better Loot Mod by Apocalyptech"