# RedWizard KIT v0.1.0-alpha6

This alpha follows a runtime-save audit of both a level-31 player-created Red Wizard and Edwin in a real heavily modded EET game.

## What changed
- Fixed the raw `<SCHOOLTOKEN>` placeholder shown during specialist spell selection when SCS/SFO's externalized spell UI is installed.
- RedWizard KIT now registers a localized custom `dwKitSpecLearnLine` for `S9REDWIZ` through SCS's own extension point when that system is detected.
- The fix is display-only: it does not alter spell availability, specialist restrictions or the underlying spell-selection rules.

## Runtime validation
- CHARNAME is correctly assigned `S9REDWIZ`.
- Illusion remains available while the normal Conjurer Divination prohibition is preserved.
- Level-31 CHARNAME has the normal specialist spell-slot progression and the separate intrinsic Red Wizard +1 slot for spell levels 1-9.
- Specialist Defense is present with the exact intended stack: +2 base vs Conjuration plus five +1 increments, for **+7 vs Conjuration at level 16+**.
- Spell Power is present at +5 caster levels at level 31.
- The repeating Enhanced Specialization aura is present.
- Edwin is correctly assigned `S9REDWIZ`.
- Edwin keeps `MISC89`, his native BG2 amulet slot bonuses, and separately receives the Red Wizard intrinsic slot bonus.
- Edwin retains the Illusion spells that the original Artisan component removed, including memorized Illusion spells.

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
