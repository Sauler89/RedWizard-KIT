# RedWizard KIT v0.1.0-alpha4

**RedWizard KIT** extracts and adapts the Red Wizard (Conjurer) implementation from **The Artisan's Kitpack** into an independent WeiDU mod for BG:EE, BG2:EE and EET.

The main design change is deliberate: the Red Wizard keeps the normal Conjurer prohibited school (**Divination**) but **does not gain Illusion as an additional prohibited school**.

## Components

### 0 — Red Wizard (Conjurer) kit
- Adds a playable Red Wizard kit for CHARNAME.
- Keeps the original non-good alignment restriction.
- Adds no new race restriction; character-generation availability follows the Mage races supported by the installed game/mod setup.
- Preserves the original Enhanced Specialization mechanics:
  - enemies within 30 ft. suffer -4 to saves vs Conjuration spells from all sources;
  - +1 extra wizard spell slot at each spell level, in addition to the normal specialist bonus;
  - Spell Power progression at levels 1/3/6/9/12;
  - Specialist Defense progression at levels 1/4/8/12/16.
- Preserves the normal Conjurer prohibited school: Divination.
- **Removes the additional prohibited school completely: Illusion remains usable.**

### 100 — Apply the Red Wizard kit to Edwin
- Requires component 0.
- Assigns the Red Wizard kit to the same Edwin BGEE/BG2EE/EET CRE variants patched by the source mod.
- Does **not** remove Illusion spells from Edwin.
- Does **not** remove Edwin's scripted Mirror Image special ability.
- Leaves the global `MISC89.ITM` untouched. A private clone (`S9RWAMU.ITM`) is created for Edwin and only its opcode 42 wizard-slot effects are removed, preventing duplicate Red Wizard spell slots while preserving compatibility with other item changes.

For reliable testing of component 100, start a new game or use a save made before Edwin has been instantiated/recruited.

## Technical change: additional prohibited school

The original Edwin implementation uses:

```text
unusable = 0x00001080
```

This combines the Conjurer usability bit (`0x00000080`) with the Necromancer usability bit (`0x00001000`). RedWizard KIT uses:

```text
unusable = 0x00000080
```

The Red Wizard therefore remains Conjurer-based and retains Divination as the normal prohibited school, while Illusion is no longer additionally prohibited. The Edwin component also omits the original explicit removal of Illusion spells and the `EDWIN.BCS` Mirror Image removal.

## Extra spell slots

The source Edwin-only implementation provides the Red Wizard's additional +1 wizard spell slot per spell level through `MISC89.ITM`. RedWizard KIT moves this class benefit into `S9RWSLOT.SPL`, applied by the kit CLAB, so CHARNAME receives the same Red Wizard advantage.

When component 100 is installed, the currently installed `MISC89.ITM` is cloned to `S9RWAMU.ITM`; only opcode 42 equipping effects are removed from that private clone and only Edwin's matching CRE item entries are redirected to it. The global `MISC89.ITM` remains untouched.

## Compatibility

Supported games:
- Baldur's Gate: Enhanced Edition
- Baldur's Gate II: Enhanced Edition
- Enhanced Edition Trilogy (EET)

Do not install together with **The Artisan's Kitpack NPC component #5102 — Red Wizard Mage Kit for Edwin**. The installer explicitly forbids that combination.

The package uses the exact project-reference **WeiDU 249.00** executable supplied for this mod. `ADD_KIT_EX` v0.6.3 requires WeiDU 247 or later.

## Installation

1. Extract the release archive directly into the game directory.
2. Run `Setup-RedWizardKIT.exe`.
3. Install component 0.
4. Optionally install component 100 to apply the kit to Edwin.

## Credits

- **The Artisan / [TheArtisanBG](https://github.com/TheArtisanBG)** — original Red Wizard design, implementation and binary assets from [The Artisan's Kitpack](https://github.com/TheArtisanBG/The-Artisan-s-Kitpack).
- **Argent77** — `ADD_KIT_EX` (the bundled library declares itself public domain).
- **Sauler89** — RedWizard KIT extraction, adaptation, compatibility work and requested design changes.

## Attribution and redistribution note

RedWizard KIT is a derivative adaptation of the Red Wizard material from The Artisan's Kitpack. The upstream repository reports no repository-level license for those original assets. The original work is explicitly credited above; this repository does not claim ownership of The Artisan's original Red Wizard content.
