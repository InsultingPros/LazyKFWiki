!> Respect mod authors and credit them. This is not a guide for stealing.

Some of the mods strip their source code, which prevents community from modifying or learning from them. Each mod author has their own reasons and you can read some relevant discussion [here](https://wiki.beyondunreal.com/Legacy:Trystan/Code_Protection). Whatever your opinion on decompilation is - we won't try to argue about it in this document and simply tell you how to do it. Two main ways of decompiling mutator with stripped code are:

* [Eliot's](https://github.com/EliotVU/Unreal-Library) [**UE Explorer**](https://eliotvu.com/portfolio/view/21/ue-explorer). Best variant and all later text will be about it.

## Bytecode vs UnrealScript

UE Explorer *guesses* exported scripts from the package bytecode, and some statements differ in bytecode. So don't be confused when you find no `for` loops, no `else if` and so on. For most part you will be able to compile exported code without issues, and result will be the same. But you really want to make the code more human readable, at least for yourself and later modificatons.

## Additional Requirements

These will greatly help you in source file editing. Apps may differ for you, we just advice most user friendly and stable variant.

* [VSCode](https://code.visualstudio.com/).
* [VSCode UnrealScript extension](https://marketplace.visualstudio.com/items?itemName=EliotVU.uc).
* [KF SDK](https://steamdb.info/app/1260/), or better download more complete sources from [Killing Floor Git](https://github.com/InsultingPros/KillingFloor).
* [UnCodex](https://sourceforge.net/projects/uncodex/) for easy package dependancy check.

### Code Comments

`stripsourcecommandlet` removes all your code from package, including comments. You have to read and guess the exported code on your own. And add your own comments!

For UE Explorer's comments (aka `// End:0x69 [Loop If]`, `//return;` and so on) you can suppress them in application options, but they are helpful and make editing visually easier, better leave them until the very end.

### FOR loops

You wont find any FOR loops in stripped package. Compiler replaces it with [labels](https://wiki.beyondunreal.com/States#State_Labels_and_Latent_Functions) and [goto statements](https://wiki.beyondunreal.com/GoTo_statement).

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

Looks pretty and understandable, right?

If you see `// [Explicit Break]` replace with [break statement](https://wiki.beyondunreal.com/Break_statement), and for `// [Explicit Continue]` : [continue statement](https://wiki.beyondunreal.com/Continue_statement).

### Replicaion Blocks

Everything will be exported fine, except unreal script's break lines: `;`.

```clike
replication
{
  // Pos:0x000
  reliable if(bNetInitial && Role == ROLE_Authority)
    CsHDRI
}
```

Add them and replace UE Explorer comments.

```clike
replication
{
  reliable if (bNetInitial && Role == ROLE_Authority)
    CsHDRI;
}
```

### Defaultproperties

You can view them in UE Explorer, but they are not guaranteed to be correct due to [some issues](https://github.com/EliotVU/Unreal-Library/issues/40#issuecomment-907320329). We highly advice you to decompile / `batchexport` the stripped package to get `defaultproperties` blocks and manually copy-paste them into UE Explorer exported code.

Here are some examples of wrong UE Explorer output.

```clike
defaultproperties
{
  FireModeClass=class'W_DualMK23Fire'
}
```

`FireModeClass` is a static array defined in [Weapon](https://github.com/InsultingPros/KillingFloor/blob/main/Engine/Classes/Weapon.uc#L33). If you compile in this way, you will crash at weapon firing attempt. Correct code is:

```clike
defaultproperties
{
  FireModeClass(0)=class'W_DualMK23Fire'
}
```

In other cases we can't even wiew the arrays.

```clike
defaultproperties
{
  PanelClass=/* Array type was not detected. */
  // should be "CsHDMut.GUI_BuyMenuTab"
}
```

And there are huge issues with [subobjects](https://wiki.beyondunreal.com/Subobjects#Subobjects_in_exported_source_code).

```clike
defaultproperties
{
  begin object name=SaleBox class=GUI_BuyMenuSaleListBox
    OnCreateComponent=InternalOnCreateComponent
    ...
  object end
  // Reference: GUI_BuyMenuSaleListBox'GUI_BuyMenuTab.SaleBox'
  SaleSelect=SaleBox
}
```

This must be converted (or better copy-pasted from usual `batchexport`) into:

```clike
defaultproperties
{
  Begin Object Class=GUI_BuyMenuSaleListBox Name=SaleBox
    OnCreateComponent=SaleBox.InternalOnCreateComponent
    ...
  End Object
  SaleSelect=GUI_BuyMenuSaleListBox'CsHDMut.GUI_BuyMenuTab.SaleBox'
}
```

### ElseIF Statements

UE Explorer will print only usual IF statements and avoid [ElseIF](https://wiki.beyondunreal.com/If_statement#.22ElseIf.22_statement)'s.

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

Make it more human readable.

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

### Class Modifiers

UE Explorer will add some [class modifiers](https://wiki.beyondunreal.com/Classes#Editor-related_modifiers) that wont break anything but you actually don't need them.

```clike
class Vet_Commando extends KFVetCommando
  abstract
  hidecategories(Movement,Collision,Lighting,LightColor,Karma,Force);
  // ^ whole line can be removed
```

Be cautious with `dependson` lines, very rarely they can be required. But most time you are free to cleanup.

### Enumeration Detection

In some cases you will notice that UE Explorer shows `int`'s instead of enumerations. That's mostly fine, but you have to check the parent classes to understand what enum is that, so better fix that parts.

```clike
Level.NetMode == 3
// source: https://github.com/InsultingPros/KillingFloor/blob/main/Engine/Classes/LevelInfo.uc#L188
Level.NetMode == NM_Client

RemoteRole = 2
// source: https://github.com/InsultingPros/KillingFloor/blob/main/Engine/Classes/Actor.uc#L224
RemoteRole = ROLE_SimulatedProxy

etc.
```

If you have any IDE installed just check the variable definitions. It's not that hard.

## Notable Mention

There are few decompilation guides around, but one of the KF orientated ones in [kazachidla's](http://steamcommunity.com/profiles/76561198012931650) **UT Package Tool** [guide](https://steamcommunity.com/sharedfiles/filedetails/?id=314459304).
