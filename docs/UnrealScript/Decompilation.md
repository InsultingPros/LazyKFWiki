!> Respect mod authors and credit them. This is not a guide for stealing.

Some of the mods strip their source code, which prevents community from modifying or learning from them. Each mod author has their own reasons and you can read some relevant discussion [here](https://wiki.beyondunreal.com/Legacy:Trystan/Code_Protection). Whatever your opinion on decompilation is - we won't try to argue about it in this document and simply tell you how to do it. 

## Requirements

In this guide we will discuss [Eliot's](https://github.com/EliotVU/Unreal-Library) [**UE Explorer**](https://eliotvu.com/portfolio/view/21/ue-explorer) with following tools:

* [VSCode](https://code.visualstudio.com/) with [UnrealScript extension](https://marketplace.visualstudio.com/items?itemName=EliotVU.uc).
* [KF SDK](https://steamdb.info/app/1260/) to get game sources and UCC.exe.
  * [Killing Floor Git](https://github.com/InsultingPros/KillingFloor) on top of it for complete sources.
* [UnCodex](https://sourceforge.net/projects/uncodex/) for easy package dependancy check.

## Bytecode vs UnrealScript

Mutator compilation turns UnrealScript into unreal engine-specific bytecode. This process is destructive: semantics of many of the UnrealScript syntax constructs (e.g. if/else blocks and loops) are lost during their translation into bytecode and decompilation cannot reliably reproduce them, usually outputting a more complex code (even if functionally identical). Below we will give you several examples of how "compilation -> decompilation" process might transform UnrealScript source code to help you revert some of those changes.

### FOR loops

UEExplorer won't recover `for` loops by himself. Code like this:

```clike
// modify zeds in special squads
function ModifySquadArray(out array<SpecialSquad> SquadArray)
{
  local int i, j;

  // for loop for SquadArray
  for (i = 0; i < SquadArray.Length; i++)
  {
    // for loop for SquadArray[i].ZedClass
    for (j = 0; j < SquadArray[i].ZedClass.Length; j++)
    {
      ReplaceMonsterClass(SquadArray[i].ZedClass[j]);
    }
  }
}
```

Will be translated into combination of [labels](https://wiki.beyondunreal.com/States#State_Labels_and_Latent_Functions) and [goto statements](https://wiki.beyondunreal.com/GoTo_statement):

```clike
function ModifySquadArray(out array<SpecialSquad> SquadArray)
{
  local int i, j;

  i = 0;
  J0x07:
  // End:0x69 [Loop If]
  if(i < SquadArray.Length)
  {
    j = 0;
    J0x1E:
    // End:0x5F [Loop If]
    if(j < SquadArray[i].ZedClass.Length)
    {
      ReplaceMonsterClass(SquadArray[i].ZedClass[j]);
      ++ j;
      // [Loop Continue]
      goto J0x1E;
    }
    ++ i;
    // [Loop Continue]
    goto J0x07;
  }
  //return;  
}
```

If you compile it, it will be perfectly fine. But this is hardly readable, especially when code is pretty big. Remove labels and convert goto's into FOR loops.

If you see any `// [Explicit Break]` replace with [break statement](https://wiki.beyondunreal.com/Break_statement), and for `// [Explicit Continue]` : [continue statement](https://wiki.beyondunreal.com/Continue_statement).

### Replicaion Blocks

Everything will be exported fine, except replication statements will miss required semicolons `;`. You need to add them manually:

```clike
replication
{
  // Pos:0x000
  reliable if(bNetInitial && Role == ROLE_Authority)
    CsHDRI
}
```

```clike
replication
{
  reliable if (bNetInitial && Role == ROLE_Authority)
    CsHDRI;
}
```

### Defaultproperties

You can view them in UE Explorer, but they are not guaranteed to be correct due to [some issues](https://github.com/EliotVU/Unreal-Library/issues/40#issuecomment-907320329) and unrealscript [factors](https://wiki.beyondunreal.com/Subobjects#Subobjects_in_exported_source_code).

We highly advice you to manually decompile the stripped package and copy-paste `defaultproperties` into UE Explorer export.

```clike
ucc.exe batchexport PACKAGENAME.u class uc ../DIRECTORY/
pause
```

### ElseIF Statements

UE Explorer will print only usual `if` statements and avoid [ElseIF](https://wiki.beyondunreal.com/If_statement#.22ElseIf.22_statement)'s:

```clike
static function AddDefaultInventory(KFPlayerReplicationInfo KFPRI, Pawn P)
{
  // End:0x44
  if(KFPRI.ClientVeteranSkillLevel == 5)
  {
    KFHumanPawn(P).CreateInventoryVeterancy("CsHDMut.W_Bullpup", default.StartingWeaponSellPriceLevel5);
  }
  // End:0x8E
  else
  {
    // End:0x8E
    if(KFPRI.ClientVeteranSkillLevel == 6)
    {
      KFHumanPawn(P).CreateInventoryVeterancy("CsHDMut.W_AK47AssaultRifle", default.StartingWeaponSellPriceLevel6);
    }
  }
  //return;  
}
```

Make it less cumbersome.

```clike
static function AddDefaultInventory(KFPlayerReplicationInfo KFPRI, Pawn P)
{
  if (KFPRI.ClientVeteranSkillLevel == 5)
  {
    KFHumanPawn(P).CreateInventoryVeterancy("CsHDMut.W_Bullpup", default.StartingWeaponSellPriceLevel5);
  }
  else if (KFPRI.ClientVeteranSkillLevel == 6)
  {
    KFHumanPawn(P).CreateInventoryVeterancy("CsHDMut.W_AK47AssaultRifle", default.StartingWeaponSellPriceLevel6);
  }
}
```

### Enumeration Detection

UE Explorer can turn enum values into numeric constants that represent them, which might make code hard to understand. If you want to fix these parts, you'll have to do it manually, by looking up enum definitions:

```clike
enum ENetMode
{
  //  Enum values are enumerated with integer values starting from 0:
  NM_Standalone,        // 0
  NM_DedicatedServer,   // 1
  NM_ListenServer,      // 2
  NM_Client             // 3
}

// examples
Level.NetMode == 3
// source: https://github.com/InsultingPros/KillingFloor/blob/main/Engine/Classes/LevelInfo.uc#L188
Level.NetMode == NM_Client

RemoteRole = 2
// source: https://github.com/InsultingPros/KillingFloor/blob/main/Engine/Classes/Actor.uc#L224
RemoteRole = ROLE_SimulatedProxy
```

Just check variable definitions in VSCode if you have any difficulties.

## Notable Mention

There are few decompilation guides around, but one of the KF orientated ones in [kazachidla's](http://steamcommunity.com/profiles/76561198012931650) **UT Package Tool** [guide](https://steamcommunity.com/sharedfiles/filedetails/?id=314459304).
