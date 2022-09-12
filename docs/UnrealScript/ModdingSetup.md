!> This list is for people who understand what is a binary file, what is a directory, how to differentiate files with different extensions, how to download and copy-paste files into game's folder, etc.

## Essentials

No matter what you plan to do (coding, modeling, mapping, etc.) KF1 SDK ([steamdb](https://steamdb.info/app/1260/)) is your starting point and main tool.

- [**KF1 SDK**](steam://run/1260/) - contains the editor, game sources and `UCC.exe`.

## Optional

Everything in this list are not required for modding Killing Floor 1, but they can help you to save huge amount of time on specific operations.

Source code:

- [**KF1 Unrealscript Sources**](https://github.com/InsultingPros/KillingFloor) - must be downloaded and installed on top of SDK if you want to get the complete sources.

Viewing binaries and file structures:

- [**UE Explorer**](https://eliotvu.com/portfolio/view/21/ue-explorer) - allows you to directly open binaries (`*.u` files) without decompilation and view their source code. Even for [stripped mods](../UnrealScript/Decompilation.md).
- [**UnCodex**](https://sourceforge.net/projects/uncodex/) - easy package dependency check. It shows a nice graph and works fast. Faster than you can open classes in editor to check the parent-child chain.

File operations:

- [**UZ2 Tool**](https://www.moddb.com/games/killing-floor/downloads/kftools-uz2) - especially handy when you create clientside mods, and you provide redirect files (`*.uz2`) for your users. Allows you to drag-n-drop directories and files for quick compression.
- [**KF Cache Extractor**](https://github.com/InsultingPros/LazyKFWiki/blob/main/docs/_content/KFCacheExtractor.exe) - [jaek](https://forums.tripwireinteractive.com/index.php?members/jaek.14402/)'s modification of ut2004 CacheExtractor. Put it inside game's main directory. Allows to easily rip files from cache and then check them in UE Explorer, decompile, whatever.

Debug:

- [**ueScriptProfiler.exe**](https://github.com/InsultingPros/LazyKFWiki/blob/main/docs/_content/ueScriptProfiler.exe): Script profiler binary. If you want to [find bottlenecks](../UnrealScript/Profiling.md) in your code this tool is the ultimate solution.

## Compilation Scripts

The minimal script that starts the compilations is:

```clike
// delete old versions of our mod, otherwise compiler won't do anything
del MYMUTATOR.u
// start the actual compilation
UCC make
// this file creates every time and it doesn't allow you to join to any server
// DO NOT FORGET TO DELETE IT!!!
del steam_appid.txt
// freeze the window so you can check the errors-successful output
pause
```

If you want to automate most actions (move files between client-server, auto create redirect files, create an output folder, etc.):

- [**KFCompileTool**](https://github.com/InsultingPros/KFCompileTool) - the most feature rich, python script. Even allows keeping the source files in a weird directory style and outside of game's folder.
- [**KFCmdlet**](https://github.com/InsultingPros/KFCmdlet) - obsolete package, but you can check it's [cmd](https://github.com/InsultingPros/KFCmdlet/tree/main/Batch_CMD) / [ps](https://github.com/InsultingPros/KFCmdlet/tree/main/Batch_PowerShell) scripts for inspiration for your own project.

## Editors

!> VSCode is the most feature rich and stable variant. And it has lots of extensions that other editors lack.

You can use whatever editor you like, but these have working unreal script extensions, and they make your coding experience much better:

- [**VSCode**](https://code.visualstudio.com/) with [Eliot's UnrealScript extension](https://marketplace.visualstudio.com/items?itemName=EliotVU.uc) / [unrealscript snippet](https://github.com/InsultingPros/LazyKFWiki/blob/main/docs/_content/unrealscript.json).
- [**SublimeText**](https://www.sublimetext.com/) with [UnrealScriptIDE extension](https://packagecontrol.io/packages/UnrealScriptIDE).
- [**Notepad++**](https://notepad-plus-plus.org/) with [UDL1](https://gist.github.com/khasky/9bcbf0cfc7594a38e5206ae0b702c061) / [UDL2](https://romerounrealscript.blogspot.com/2011/10/setting-up-notepad-for-unrealscript.html) ([how to install UDL](https://npp-user-manual.org/docs/user-defined-language-system/)).
