

# Missing MapVote Page on some servers

If you are pressing your bind / mapvote key in Esc Menu and nothing happens, most likely:

1. Server is not using Marco's [Voting Handler Fix](https://forums.tripwireinteractive.com/index.php?threads/mod-voting-handler-fix.43202/).
2. Your `user.ini` has messed up menu page settings.

```clike
[KFGui.KFGUIController]
MapVotingMenu=KFMapVoteV2.KFMapVotingPageX
```

Your client tries to open non existing menu on servers that doesn't use that mandatory mod. This can be easily fixed with:

```clike
[KFGui.KFGUIController]
MapVotingMenu=KFGUI.KFMapVotingPage
```

OR remove that section, you are ok without it.

## Roots of the Issue

[Voting Handler Fix](https://github.com/InsultingPros/KFMapVoteV3/blob/main/Classes/MVLevelCleanup.uc) sets its own MapVote page at game start and sets it back to default at the end, without touching the config. In theory this should't break anything for you, but there is a low chance other mutator (or you) saves `user.ini` midgame, and those modified lines are gonna stay and cause the issue.
