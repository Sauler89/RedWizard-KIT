# RedWizard KIT v1.0.0

This is the first stable release of **RedWizard KIT**.

It promotes the fully validated `v0.1.0-beta1` implementation without changing gameplay mechanics.

## Stable milestone
The alpha and beta validation cycle is complete. Real installation, character-generation, runtime-save and UI testing confirmed the full Red Wizard implementation on a heavily modded EET setup using WeiDU 249.00.

## Confirmed in-game
- Red Wizard is selectable by CHARNAME.
- Illusion spells remain available.
- The normal Conjurer prohibition against Divination remains active.
- The normal specialist spell-slot progression is preserved.
- The Red Wizard receives its separate intrinsic +1 wizard spell slot for spell levels 1-9.
- Spell Power reaches +5 caster levels at level 12+.
- Specialist Defense is present as +2 base vs Conjuration plus five +1 increments, for **+7 vs Conjuration at level 16+**.
- The repeating Enhanced Specialization aura is present.
- Edwin is correctly assigned `S9REDWIZ`, retains his existing amulet and keeps Illusion spells.
- Both components install successfully with zero WeiDU errors and zero warnings in the validated installation.

## Infinity UI++ specialist prompt — verified fixed
The exact `UI.MENU` used during testing showed that `<SCHOOLTOKEN>` is resolved inside `rgChooseSpellsMenuOnOpen()`, where stock specialist kits are identified by their stock names.

Because `S9REDWIZ` has its own kit name, it did not enter the vanilla Conjurer branch even though it is mechanically Conjurer-based. RedWizard KIT explicitly maps `S9REDWIZ` to Infinity UI++'s own localized `CONJURATION_SCHOOL_TOKEN` at that exact token-resolution point.

In-game verification confirmed:
- **Red Wizard:** `Select at least one conjuration spell to proceed.`
- **Diviner:** `Select at least one divination spell to proceed.`
- **Abjurer:** `Select at least one abjuration spell to proceed.`

The Red Wizard fix therefore works without changing the normal specialist prompts.

## Components
- **0 — Red Wizard (Conjurer) kit**
- **100 — Apply the Red Wizard kit to Edwin**

## Compatibility
Supported games:
- Baldur's Gate: Enhanced Edition
- Baldur's Gate II: Enhanced Edition
- Enhanced Edition Trilogy (EET)

Do not install together with **The Artisan's Kitpack NPC component #5102 — Red Wizard Mage Kit for Edwin**.

The release package is self-contained and uses the project-reference **WeiDU 249.00** executable.

## Known external UI issue
A class-name artifact such as `{K=0,C=1}` can be exposed by the interaction between SCS's class/kit signalling system and Infinity UI++. This is a known external UI-filtering issue and is intentionally not patched by RedWizard KIT.

## Credits
Special thanks and full credit to **The Artisan / TheArtisanBG** for the original Red Wizard design, implementation and assets from **The Artisan's Kitpack**:
https://github.com/TheArtisanBG/The-Artisan-s-Kitpack

`ADD_KIT_EX` is by Argent77.

RedWizard KIT extraction, adaptation, compatibility work and requested design changes: **Sauler89**.
