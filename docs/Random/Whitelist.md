[v.1043]: https://store.steampowered.com/news/app/1250/view/2918851646648830122
[v.1064]: https://store.steampowered.com/news/app/1250/view/2918851646648764272
[FakedPlus]: https://github.com/InsultingPros/FakedPlus
[`bUsedCheats`]: https://github.com/InsultingPros/KillingFloor/blob/main/Engine/Classes/SteamStatsAndAchievementsBase.uc#L54
[Perk Replacement]: https://forums.tripwireinteractive.com/index.php?threads/kfmodsperkreplacement1011-level-6.38882/
[GUID hax guide]: https://steamcommunity.com/sharedfiles/filedetails/?id=1372430901
[golden LAR]: https://steamcommunity.com/sharedfiles/filedetails/?id=1355949688
[wiki old list]: https://kf-wiki.com/wiki/List_of_whitelisted_mutators
[DMN666 steam list]: https://steamcommunity.com/workshop/filedetails/?id=117038038
[TWI WL thread]: https://forums.tripwireinteractive.com/index.php?threads/all-whitelisted-packages.103899/
[TWI WL old thread]: https://forums.tripwireinteractive.com/index.php?threads/current-killing-floor-mutator-white-list.35187/
[submission thread]: https://forums.tripwireinteractive.com/index.php?threads/kf-mutator-whitelist-and-fix-submission-thread.94259/
[submission old thread]: https://forums.tripwireinteractive.com/index.php?threads/kf-whitelist-mutator-suggestion-list.34001/

?> The moment you play with greylisted mod, your stat gaining stops. You need to **restart** the game to fix it.

## Glossary

- **Blacklisted**: whole perk system is disabled. Was a thing at very early patches, now it's completely replaced by Greylisting.
- **Greylisted**: game modification that disallows any perk progression. It may or may not show appropriate warning in perk / esc menus, highly depends on what you use.

![img](./../_media/greylisted_warning.png ':size=300')

- **Whitelisted**: game modification that allows to gain perk progression.
- **Serverside**: mods that run only on server and client's do not download them.
- **Clientside**: mods that run on both server-client / only on client.

## General Info

**Whitelist** is a system that was initially created to sanction mods and maps, where people can play and gain in game stats (headshots, weld point, etc.). Mod makers had to submit their creations to TWI ([submission thread], [submission old thread]) for their approval.

Sanctioning was time-consuming, painful, not guaranteed and many mod makers even avoided it because few patches later you had to repeat the whole process due to game code changes.

After [v.1043] custom maps stopped requiring sanctioning from TWI. Around that time blacklisting was removed (no more [Perk Replacement] if you wanted to play some non-whitelisted mod).

But the most important change comes from [v.1064]. Whitelist system was changed (or more likely bugged, knowing how TWI codes). Now it allows most serverside mods to be Whitelisted.

## Serverside mods

Dedicated servers:

- All clients will gain stats. Server log will show warnings `STEAMSTATS: SECURITY CHECK FAILED - ../System/YourCustomServerMod.u` but in 99.99% cases that means nothing. There can be extreme rare exceptions, like when you use 9000 fakes with [FakedPlus] or trigger functions that explicitly enable greylist, for example [`bUsedCheats`] flag.

Listen servers:

- Works same as described above with the exception for host. He will be greylisted for mods that are not whitelisted.

## Non-Serverside mods

Server-client:

- There are only few de facto whitelisted mods, and that list changed over time as well. Actual list lies here [DMN666 steam list] | [TWI WL thread]. And for historical reasons, here are some links to old threads: [TWI WL old thread] | [wiki old list].
- Everything else will disable your stat gaining, and you need to restart the game to fix it.

Client only:

- Re-textures, sound modifications, etc can be made online compatible and whitelisted if mod maker follows this [GUID hax guide]. For example, [golden LAR].
