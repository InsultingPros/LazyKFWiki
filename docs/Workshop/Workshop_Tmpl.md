Fancy, laconic and contains all crucial info:

- What it does in few words.
- Whitelist status.
- Detailed technical info - package, class names, config files, specific settings.
- Compatibility info.
- Installation info for clients (because Workshop may and will [**fail**](../Workshop/Workshop_Issues.md)) / server admins.
- Download links for admins / clients.
- Credits and other links.

I always use this template and it's slight variations for my uploads. Check [Weapon DLC Unlocker](https://steamcommunity.com/sharedfiles/filedetails/?id=834746972) for example.

![img](./../_media/workshop_tmpl_1.png ':size=300')
![img](./../_media/workshop_tmpl_2.png ':size=300')

```js
[h1][b]General Information[/b][/h1]
This mutator unlocks all DLC and achievement dependent weapons. Original version was outdated and didn't support Neon weapons, which I fixed here.

[h1][b]GREYLISTED![/b][/h1]
Dedicated servers, Listened servers or Solo, doesn't matter, your perk stats won't save. If you are sad about this fact gtfo, consider this as a demo test before buying.

[h1][b]Weapon List:[/b][/h1]
[list]
[*]Flare Revolver
[*]Scythe
[*]ThompsonSMG
[*]Crossbuzzsaw
[*]Golden Katana
[*]Golden AK47
[*]Golden M79
[*]Golden Benelli Shotgun
[*]Golden Flamethrower
[*]Golden Deagle
[*]Golden Chainsaw
[*]Golden AA12
[*]ZED Gun
[*]Dwarf Axe
[*]Multichamber zed thrower
[*]Orca Grenade Launcher
[*]SP Musket
[*]SP Thompson SMG
[*]Thompson Drum SMG
[*]Blower Thrower
[*]Seal Squeal Harpoon Bomber
[*]Seeker Six Rocket Launcher
[*]ZED MKII Weapon
[*]Camo M32 Grenade Launcher
[*]Camo M4
[*]Camo MP5M Medic Gun
[*]Camo Shotgun
[*]Neon AK47
[*]Neon SCARMK17
[*]Neon KrissM Medic Gun
[*]Neon KSG Shotgun
[/list]

[h1][b]Technical Information[/b][/h1]
This is a [b][i]Server-Client[/i][/b] mutator. So server owners, don't forget about redirect.

[h3][b]Mutator Classname[/b][/h3]
[code]
CleanAppIDMut.CleanAppIDMut
[/code]

[h3][b]Compatibility[/b][/h3]
Works with everything.

[h1][b]INSTALLATION[/b][/h1]
If you read this you are a terrible person who don't want to spend 5 minutes in google. So enjoy my wasted 5 mins.
[olist]
    [*] Double check you have less than 50 active subscriptions in KF Workshop.
    [*] Subscribe.
    [*] Start the game and check for download notification in top right corner.
    [*] If it's not there start a solo game / join somewhere and leave back to main menu.
    [*] If it's still not there, congrats, you encountered infamous KF related bug. Use my download link to get the files and follow this [url=http://forums.tripwireinteractive.com/forum/killing-floor/killing-floor-modifications/general-modding-discussion-aa/51396-%7Bhow-to%7D-install-a-mod]instruction[/url] to properly install it.
    [*] Start the game, press on '[b]Solo[/b]' or '[b]Host Game[/b]'.
    [*] Open '[b]Mutators[/b]' tab and add '[b]CleanAppIDMut[/b]' to the list. Start the game.
    [*] ....
[/olist]
If you have a Dedicated server you know what to do. Else delete it and quit KF.

[h1][b]Download Link for Lazy Admins:[/b][/h1]
[url=https://github.com/InsultingPros/CleanAppIDMut/releases]GitHub[/url]

[h1][b]Forum Link to an outdated original:[/b][/h1]
[url=http://killing-floor.ru/mutator/249-mutator-dlc-unlocked-clean-id.html]CleanAppIDMut[/url]
Author - [url=http://steamcommunity.com/profiles/76561198051378449]Flame[/url]
```

## WhiteList status

Yeah, it's 2022 and people still care for stats. Always inform your users how your mod affects perk progression.

```js
[h1][b]Whitelist Status[/b][/h1]
[list]
[*] Dedicated server: all clients will level up, get achievs.
[*] Listened server: except the host itself, all clients will level up, get achievs.
[*] Solo: greylisted. No regrets.
[/list]
```

## Credits

If you want to link steam accounts always convert `../id/SteamProfileCustomFancyName/` URL's to `../profiles/steamID64/`, with <https://steamid.io/> or similar services. People tend to change steam profile names 10 times per day, but ID never changes.

```js
[h3][b]Credits[/b][/h3]
ArtWork - [url=https://www.deviantart.com/brainstorm-bw-style/art/Fleshpound-Rage-colors-453220493]Brainstorm-bw-style[/url]
Testers - [url=http://steamcommunity.com/profiles/76561198200384791]Shino[/url], [url=http://steamcommunity.com/profiles/76561198027407094]Joabyy[/url].
```
