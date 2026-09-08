# RedWizard KIT v0.1.0-alpha7

This alpha corrects the remaining Infinity UI++ specialist-spell prompt issue discovered by auditing a real alpha6 WeiDU installation log.

## What changed
- Confirmed alpha6 installs both components successfully with zero WeiDU errors and zero warnings.
- The alpha6 SCS/SFO-only `<SCHOOLTOKEN>` fix did not execute in the tested EET setup because `m_dw_ssd.lua` was not present.
- Kept the SCS/SFO `dwKitSpecLearnLine` hook for installations where that subsystem exists.
- Added an Infinity UI++ fallback that replaces only the specialist prompt expression and only when the selected kit is `S9REDWIZ`.
- Red Wizard now receives the localized resolved prompt `Select at least one conjuration spell to proceed.` instead of the raw `<SCHOOLTOKEN>` template.
- Every stock specialist mage and every other kit keeps Infinity UI++'s original prompt logic unchanged.
- Added an explicit WeiDU message when the Infinity UI++ compatibility patch is detected and applied.

## Gameplay status
No gameplay mechanics changed from alpha6. Runtime save auditing already confirmed:
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
