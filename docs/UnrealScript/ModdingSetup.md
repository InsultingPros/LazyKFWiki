!> This mini-guide is intended for individuals who possess a solid understanding of concepts such as binary files, directories, distinguishing files with varying extensions, as well as the ability to download and copy-paste files into a game's folder. It aims to provide a starting point for those interested in creating mutators but unsure of where to begin.

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

- [KFRedirectTool](https://github.com/InsultingPros/KFRedirectTool) - especially handy when you create clientside mods, and you want to provide redirect files (`*.uz2`) for your admin users.
- [**KF Cache Extractor**](https://github.com/InsultingPros/LazyKFWiki/releases/download/1.0.0/KFCacheExtractor.exe) - [jaek](https://forums.tripwireinteractive.com/index.php?members/jaek.14402/)'s modification of ut2004 CacheExtractor. Put it inside game's main directory. Allows to easily rip files from cache and then check them in UE Explorer, decompile, whatever.

Debug:

- [**ueScriptProfiler.exe**](https://github.com/InsultingPros/LazyKFWiki/releases/download/1.0.0/ueScriptProfiler.exe): Script profiler binary. If you want to [find bottlenecks](../UnrealScript/Profiling.md) in your code this tool is the ultimate solution.

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

You can use whatever editor you like, even plain notepad. But if you want to have smooth coding experience, check these ones:

- [**VSCode**](https://code.visualstudio.com/) with Eliot's [UnrealScript](https://marketplace.visualstudio.com/items?itemName=EliotVU.uc) extension. Has the most [features](https://github.com/EliotVU/UnrealScript-Language-Service#features) among all available options and is the most stable.
- [**SublimeText**](https://www.sublimetext.com/) with [UnrealScriptIDE](https://packagecontrol.io/packages/UnrealScriptIDE) extension.
- [**Notepad++**](https://notepad-plus-plus.org/) with [UDL (khasky)](https://web.archive.org/web/20221005032637/https://gist.github.com/khasky/9bcbf0cfc7594a38e5206ae0b702c061) / [UDL (Romero)](https://romerounrealscript.blogspot.com/2011/10/setting-up-notepad-for-unrealscript.html). Check the [UDL installation guide](https://npp-user-manual.org/docs/user-defined-language-system/).
