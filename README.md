SE Server Maintenance Utility
==============

Space Engineers Server Maintenance Utility

_"Damn, there's so much space junk that my server is running turtle-slow. Ah well, time to delete the world and start again."_

**Don't be "that admin" anymore!**

At heart, this is a simple Python script that performs the following:

**Object Cleanup**
- Junk
Removes all objects that don't have a reactor, regardless of how much fuel they have or if they're turned on.

- Dead
Removes all objects that don't have a reactor that's turned on and fueled. Aimed at removing things that are either junk, derelicts or ships that've been turned off and forgotten.

- Beacon
Inspired by Borg8401. Removes everything does doesn't have a fueled & active reactor and a beacon, at least an unfinished or disabled beacon. Good way to trim the fat, good for +16 player servers. If you want to keep it? Put a beacon on it.

**Note:** Currently doesn't factor in solar panels, too tricky to account for. Even if you check if they're facing the right way, can't detect if something's in the way. Besides, what are you doing flying around without a reactor?

**Free-Floating Item Cleanup**

As the name says, this removes any free-floating items like bits of ore or components. Doesn't do corpses just yet, that's more complicated as it's tied into the player tables and needs some more research.

**Faction Pruning**

Since the introduction of factions, almost every server has about 5 pages of dead factions. This tool will remove factions that;
Don't have any players
All faction members don't own anything, destitute.

I did think of pruning leaderless factions, however that would place players in a situation where they were getting on without a leader and after dissolving the faction, turrets that used to be friendly are now hostile. They'll have to sort it out on their own.

**Player Pruning**

Every time you respawn, you create a new "player" entry. This is how SE handles "if you die, you start from scratch". After a few player deaths, this list can get HUGE. Player Pruning removes all player entries that don't own anything.

**Usage**

The utility is purely command-line based and is meant to be included into server daemon scripts. e.g.

```
:start
run-server
taskkill /IM spaceengineersdedicated.exe
maintenance.py .\ --cleanup-objects beacon --prune-factions
goto start
```

Usage is pretty simple and if you're not sure, run the program with "--help". Dedicated server saves are usually located in `C:\Users\<username>\AppData\Roaming\SpaceEngineersDedicated\Saves\`

Ideally I'd like to this be run regularly as part of a script, but without a server API or commands you'd irritate players because;

* Without the ability to send notifications (e.g. Server says: we are about to restart), the server would just 'die' to the client without warning.
* Without the ability to force a save, the save that you open back up might be up to 10mins out of date.

Still, it's nice to be able to fix things instead of starting from scratch.

This is my first major release of anything, feel free to tell me where I've gone wrong.

The ultimate goal of this utility is to become obsolete with its functions being done by Space Engineers itself. Until then, this is way to do it.

## Version History

**V 1.1.1**

- Fixed up Player pruning. Removes player from the FactionPlayer and FactionRequests tables
- Fixed up Faction pruning. Stopped removing factions who's members don't own anything, will only clear away empty factions now. The player pruner should make this more viable. Also removes factions from FactionRelations & FactionRequests tables

**V 1.1**

- Added Junk mode, removing everything without a reaction, regardless of fuel or status.
- Considered pruning factions without a leader but you might get into strife over factions getting along without a leader, suddenly having base turrets turn on friendlies. Won't do that.
- Added function to remove all free-floating objects. Doesn't do corpses though, they are more complicated
- Added whatif mode, like MS Powershell, doesn't make any changes but tells you what it'll do. Good for debugging
- Added function to remove junk players, players that don't own anything. Also removes them from factions

**V 1.0**

- Release

[Author's Forum Thread](http://forums.keenswh.com/post/se-server-maintenance-utility-6985610)
