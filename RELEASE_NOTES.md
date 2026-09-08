# RedWizard KIT v0.1.0-alpha8

This alpha replaces the previous generic Infinity UI++ prompt workaround with a fix based on the user's actual installed `UI.MENU`.

## Exact cause found
The supplied Infinity UI++ UI file shows that the specialist-spell banner is rendered as:

```lua
text lua "dwFilterKitDesc(getUiString('SPECIALIST_SPELL_REQ'))"
```

The `<SCHOOLTOKEN>` value is not resolved by that label. It is set earlier inside `rgChooseSpellsMenuOnOpen()`, where Infinity UI++ compares the current kit name against the stock specialist names and calls `setStringTokenLua()` for the corresponding school.

The stock Conjurer branch is:

```lua
elseif currentKitName == rgGetGameEngineString(25320,25320,2179,2179) then
    setStringTokenLua('<SCHOOLTOKEN>',getUiString('CONJURATION_SCHOOL_TOKEN'))
```

`S9REDWIZ` is mechanically a Conjurer but has its own kit name, so it never matches that stock-name branch. The spell-selection rule still works, but the UI token remains unresolved.

## What changed
- Removed the ineffective alpha7 label-level fallback.
- Added a precise Infinity UI++ mapping at the actual token-resolution point in `rgChooseSpellsMenuOnOpen()`.
- When the selected kit ID is `S9REDWIZ`, the UI now explicitly calls Infinity UI++'s own localized `CONJURATION_SCHOOL_TOKEN` path.
- The original stock Abjurer/Conjurer/Diviner/etc. branches remain unchanged and continue handling every vanilla specialist normally.
- The existing SCS/SFO `dwKitSpecLearnLine` path is retained for installations that actually provide that subsystem.
- No gameplay mechanics changed.

## Gameplay status
Previous runtime save auditing already confirmed:
- CHARNAME is correctly assigned `S9REDWIZ`.
- Illusion remains available while the normal Conjurer Divination prohibition is preserved.
- CHARNAME receives the normal specialist spell-slot progression plus the separate intrinsic Red Wizard +1 slot for spell levels 1-9.
- Specialist Defense is present with the exact intended stack: +2 base vs Conjuration plus five +1 increments, for **+7 vs Conjuration at level 16+**.
- Spell Power reaches +5 caster levels at level 12+.
- The repeating Enhanced Specialization aura is present.
- Edwin is correctly assigned `S9REDWIZ`, keeps his existing amulet, and retains Illusion spells.

## Known external UI issue
A class-name artifact such as `{K=0,C=1}` can be exposed by the interaction between SCS's class/kit signalling system and Infinity UI++. This is a known external UI-filtering issue and is intentionally not patched by RedWizard KIT.

## Compatibility
BG:EE, BG2:EE and EET.

Do not install together with The Artisan's Kitpack NPC component #5102 (Red Wizard Mage Kit for Edwin).

## Credits
Special thanks and full credit to **The Artisan / TheArtisanBG** for the original Red Wizard design, implementation and assets from **The Artisan's Kitpack**:
https://github.com/TheArtisanBG/The-Artisan-s-Kitpack

`ADD_KIT_EX` is by Argent77.

RedWizard KIT extraction, adaptation and compatibility work: **Sauler89**.
