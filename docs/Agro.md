!> WORK IN PROGRESS

## Gloassary

- **LOS** - line of sight. Can zed see you or not.
- **Breaking the LOS** - going behind corners, map objects so zed stopps physically looking at you.
- **Kiting** - play style that involves moving around the map in organized, well thought circles.
- **Camping** - play style that involves holding the ground aka standing and chilling in any spot.

## Genaral Information

You can divide KF playerbase into 2 groups:

- People who do NOT know what agro means or how it works. In this case all your dozens, hundreds or even thousands hours in KF mean nothing, you've skipped a huge part of gameplay, combos and in general you've played this game in a very inefficient and boring way. If this hurts you, I'm not sorry. Plain facts and everything will be proven in this article.
- People who know what is it and can abuse it to some degree. If this is you - you may skip to technical section for source code explanation and advanced stuff.

You can define Agro as **Zed's attraction to you**. If some zed is agroed on you - you are the zed's target, he looks at you, he moves after you, he rotates after you, he reaches to you and hits you.

This part is simple and most people kinda guess when some zed has an agro on him. What people do not know is how zed changes his targets and how it can be used to avoid most dangerous situations game can throw at you.

Zeds that will always switch to you if you hug-bump them:

- dkanus, i dunno D: well steves and pat, but you can block all other zeds freely?? I need your testing skills.

## Vanilla (`KF-` maps)

Have you ever interested what does happen when game decides to spawn a zed?

- Game picks a random `squad` to spawn.
- Game picks a suitable `ZombieVolume` - this can be behind the wall, outside of your view angle, or at your face if the map is cheaply made.
- Game picks a random `controller` from alive players (this can be you).
- Game does several loops, trying to spawn all zeds from picked `squad` and assigns a target that picked `controller` (which again can be you).
- Zed starts his slow walk towards his target, this can be 200m away (hi MTPass lovers!) or whatever close-far-behind obstacles-behind your ass.

## Objective Mode (`KFO-` maps)

<!-- TODO Does almost the same thing + KFHumanPawn's `assetthreatto` changes -->

**tldr**: Zeds **ALWAYS** go for the closest player.

**tlmr**: In theory map makers can control it more precisely with special inventory item and NPC settings. Gas can, transmitter parts (Frightyard) and explosive (i.e. in Transit) make you x1.5 more attractive to zeds. And Lockheart and breaker boxes (Steamland) attract them much better than players.

But still zeds prioritize distance more and this only works when players are extremely cramped. If you use some basic knowledge to spread and control the zeds in vast majority of times you can ignore these variables.

## Mods that affect Agro

<!-- TODO Scrn + tactical AI based on its code, links, explanation -->

## Basic Abusing

<!-- TODO lots of **gif**'s (better **mp4**) maybe? -->
Most important part to check - what game mode are you playing.

**Vanilla**:

- Always do the distance check to zeds initial agro won't be on you - always keep a player between you and possible zed appearance spot.
- If you want to change zed's agro on someone else (on a compliance right?)
  - If that person doesn't know how to drag the agro - make sure you are further than him and simply break the LOS.
  - If that person knows how to do it, check if you are out of danger, have a space to do it and move in the opposite direction of that player, so he will reach to zed much faster and drag the agro by damaging him.

This ofc works in the other way around if you are the one who want to take the agro / have it initially on you.

**Objective Mode**:

Do you want to get rid of a zed?

- Add a distance between you and the zed, so other players will be closer than you. Zed will change the target immediately.
- Ideally you want to do this on existing NPC's, breaker boxes, etc, to minimize the possible harm. Or maximize depending on your tactics...

**SCrN and based modes**:

In theory those have advanced and more complicated 

## Zeds that will give you a trouble

We really could not not warn you xD

Vanilla zeds work fine for most cases, for most mods. And most of custom zeds also do that. BUT there are 2 very exceptional zeds which will troll you to death in the worst situations that you expect.

### Brutes + Jasons == rip and tear

Original \ ScrN zed pack (tho this is the worst because Poosh thought why not spawn up to 6 brutes at same time!) or any other existing variants, no matter what these 2 zeds will be very picky on following the global agro rules. And that pickiness is fully random and luck based.

- If you used 1 additional spoon of sugar for your coffee, brute can charge up to your face, do a 180 degree turn and go murder your teammate, who was much further than you and did nothing to him.
  - Or start to run around and hit everyone without any logic.
- Brute easily can get mad at some zeds and make them fly to your face across the map. If thats a bloat not much of an issue, but mostly it will be a fleshpound, a jason or an other brute... have fun dealing with it.
- Depending on a sun orientation Jason can charge person A, hit him several times but don't kill, make a sharp turn and come kill you who afk's behind everyone.
  - Or turn around and go roam around the map in a rage mode, until he will fall at your head from nowhere.

We can post many more cases that may happen to poor you, but you got the idea. 

If you see one of these zeds (or much worse - squads of them) they are TOP priority to kill. If you fail to do it in time, it will lead to ~70-99% team wipes. Only 3-4 fleshpounds can deal more harm to your team, but even that is a more controllable danger.

And the last note if you are brave enough to handle the brute/jason heat - on maps with bad-broken pathing these quirks will happen more frequantly. But don't think that on good maps you will be safe and loose concentration. Big brute is watching you!
