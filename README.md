# RedWizard KIT v1.1.0

**RedWizard KIT** extracts and adapts the Red Wizard (Conjurer) implementation from **The Artisan's Kitpack** into an independent WeiDU mod for BG:EE, BG2:EE and EET.

The main design change is deliberate: the Red Wizard keeps the normal Conjurer prohibited school (**Divination**) but **does not gain Illusion as an additional prohibited school**.

## Edwin alternate portrait

![Edwin alternate portrait by The Artisan](https://raw.githubusercontent.com/TheArtisanBG/The-Artisans-Corner/c2a7e79923210d3e78b4e0c33256f47cf7bfed2d/assets/img/clipboard-image-37.png)

Optional component 200 installs the Edwin portrait shown above. The portrait is the same artwork displayed on **The Artisan's Corner** for The Artisan's Kitpack and is credited to **The Artisan / TheArtisanBG**.

The release provides standard Enhanced Edition L/M/S portrait sizes as 24-bit BMP files and installs both Edwin naming sets:

- BG:EE / BG1-style: `EDWINL`, `EDWINM`, `EDWINS`
- BG2:EE / BG2-style: `NEDWINL`, `NEDWINM`, `NEDWINS`

This makes the component compatible with BG:EE, BG2:EE and both portions of EET. It requires no CRE edit, so it also replaces Edwin's portrait in existing saves. The standard portrait resrefs and L/M/S sizes work with both the vanilla Enhanced Edition UI and Infinity UI++ without a UI-specific portrait patch.

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
- Does **not** modify, replace, clone or redirect `MISC89.ITM` or any other Edwin item.

For reliable testing of component 100, start a new game or use a save made before Edwin has been instantiated/recruited.

### 200 — Install alternate portrait for Edwin
- Independent optional component; component 0/100 is not required.
- Installs the supplied portrait in standard EE Large/Medium/Small sizes: 210×330, 169×266 and 54×84.
- Installs both `EDWIN*` and `NEDWIN*` portrait names for BG:EE, BG2:EE and EET compatibility.
- Uses ordinary game portrait resrefs, so no `UI.MENU` patch is needed for either vanilla UI or Infinity UI++.
- Works with existing saves because the portrait resources themselves are overridden rather than changing Edwin's CRE portrait fields.

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

The original Artisan Edwin-only component replaces `MISC89.ITM` with a custom version containing nine opcode 42 effects that grant the Red Wizard's extra wizard spell slots.

RedWizard KIT moves this Red Wizard class benefit into `S9RWSLOT.SPL`, applied by the kit CLAB, so CHARNAME and Edwin receive the same intrinsic Red Wizard bonus. Component 100 therefore leaves Edwin's currently installed amulet completely untouched.

A level-31 CHARNAME runtime-save audit confirmed the normal specialist slot progression separately from the nine intrinsic `S9RWSLOT` +1 effects. An Edwin runtime-save audit also confirmed that his native BG2 amulet slot bonuses remain intact while the Red Wizard slot bonus is applied separately.

## Specialist Defense and Spell Power validation

Runtime-save inspection of a level-31 Red Wizard confirmed:

- `S9RWBASE`: opcode 346, +2 saves vs Conjuration;
- five `S9RWDEF` opcode 346 effects, +1 each, from the level 1/4/8/12/16 progression;
- total conditional saving-throw bonus at level 16+: **+7 vs Conjuration**;
- `S9RWPWR`: opcode 191 with value 5 at level 31, matching the intended Spell Power progression;
- `S9RWBASE` also carries the repeating `S9RWAUR` effect used by Enhanced Specialization.

The conditional school-specific saving-throw modifiers are not expected to alter the generic Save vs. Spell number shown on the character record screen.

## SCS / Infinity UI++ compatibility

Infinity UI++ displays the specialist-spell requirement through `SPECIALIST_SPELL_REQ`, whose `<SCHOOLTOKEN>` is resolved inside `rgChooseSpellsMenuOnOpen()`. Stock specialist kits are recognized by their stock kit names. `S9REDWIZ` is mechanically a Conjurer but has its own kit name, so without a compatibility mapping the UI can display the raw `<SCHOOLTOKEN>` placeholder even though spell availability itself is correct.

RedWizard KIT explicitly maps `S9REDWIZ` to Infinity UI++'s own localized `CONJURATION_SCHOOL_TOKEN` at that token-resolution point. The fix was audited against the actual installed `UI.MENU` and verified in-game: Red Wizard displays `Select at least one conjuration spell to proceed.`, while stock specialists such as Abjurer and Diviner continue displaying their own correct school names.

When SCS/SFO's externalized spell UI (`m_dw_ssd.lua`) is present, RedWizard KIT also supports its `dwKitSpecLearnLine` extension point.

A separate cosmetic issue where class names expose strings such as `{K=0,C=1}` is a known SCS + Infinity UI++ UI-filtering problem and is intentionally not patched by RedWizard KIT.

## Validation status

`v1.1.0` adds only the optional Edwin portrait component to the fully validated `v1.0.0` gameplay implementation. Components 0 and 100 are unchanged apart from the mod version string.

Validation completed for the gameplay components includes:

- real WeiDU 249.00 installation on a heavily modded EET setup with components 0 and 100;
- zero installer errors and zero warnings in the validated installation;
- CHARNAME character-generation and runtime-save inspection;
- Edwin inspection from a real `BALDUR.gam` save;
- Illusion availability and normal Conjurer Divination prohibition;
- extra spell-slot progression;
- Spell Power and Specialist Defense effects;
- Enhanced Specialization aura;
- Infinity UI++ specialist-school prompt for Red Wizard and stock specialists.

## Compatibility

Supported games:
- Baldur's Gate: Enhanced Edition
- Baldur's Gate II: Enhanced Edition
- Enhanced Edition Trilogy (EET)

Do not install together with **The Artisan's Kitpack NPC component #5102 — Red Wizard Mage Kit for Edwin**. The installer explicitly forbids that combination for components 0/100.

The package uses the exact project-reference **WeiDU 249.00** executable supplied for this mod. `ADD_KIT_EX` v0.6.3 requires WeiDU 247 or later.

## Installation

1. Extract the release archive directly into the game directory.
2. Run `Setup-RedWizardKIT.exe`.
3. Install component 0 for the playable Red Wizard kit.
4. Optionally install component 100 to apply the kit to Edwin.
5. Optionally install component 200 to replace Edwin's portrait.

> **Source checkout note:** install from a GitHub Release rather than directly from a source checkout. Release packaging restores the pinned `ADD_KIT_EX` dependency, the binary projectile and the portrait files, then adds the project-reference WeiDU 249.00 executable. Release archives are self-contained.

## Credits

- **The Artisan / [TheArtisanBG](https://github.com/TheArtisanBG)** — original Red Wizard design, implementation and binary assets from [The Artisan's Kitpack](https://github.com/TheArtisanBG/The-Artisan-s-Kitpack), and the Edwin portrait displayed on [The Artisan's Corner](https://theartisanbg.github.io/The-Artisans-Corner/kitpack).
- **Argent77** — `ADD_KIT_EX` (the bundled library declares itself public domain).
- **Sauler89** — RedWizard KIT extraction, adaptation, compatibility work and requested design changes.

## Attribution and redistribution note

RedWizard KIT is a derivative adaptation of the Red Wizard material from The Artisan's Kitpack. The upstream repository reports no repository-level license for those original assets. The original work, including the Edwin portrait used by component 200, is explicitly credited above; this repository does not claim ownership of The Artisan's original content.
