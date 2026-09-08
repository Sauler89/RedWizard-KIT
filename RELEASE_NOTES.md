# RedWizard KIT v1.1.0

This release adds a new optional Edwin portrait component while keeping the validated Red Wizard gameplay implementation from v1.0.0 unchanged.

## New component 200 — Alternate portrait for Edwin
- Installs the Edwin portrait displayed on **The Artisan's Corner** for The Artisan's Kitpack.
- Full portrait credit goes to **The Artisan / TheArtisanBG**.
- Provides standard Enhanced Edition 24-bit BMP portrait sizes:
  - Large: 210×330
  - Medium: 169×266
  - Small: 54×84
- Installs both Edwin portrait naming sets:
  - `EDWINL/M/S` for BG:EE / BG1-style resources
  - `NEDWINL/M/S` for BG2:EE / BG2-style resources
- This makes the portrait work in BG:EE, BG2:EE and across EET.
- The component replaces the portrait resources directly, so it works with existing saves and does not need to patch Edwin's CRE files.
- Uses the normal EE portrait resrefs and L/M/S files, so it is compatible with both the vanilla game UI and Infinity UI++ without a UI-specific portrait patch.
- Component 200 is independent: components 0 and 100 are not required.

## Portrait source and attribution
The portrait source is pinned to The Artisan's Corner repository at commit:

`c2a7e79923210d3e78b4e0c33256f47cf7bfed2d`

Source asset:

`assets/img/clipboard-image-37.png`

The release workflow verifies the source image SHA-256 before generating the EE BMP variants.

## Gameplay status
Components 0 and 100 are unchanged from the validated v1.0.0 implementation except for the mod version string. Existing validation remains applicable:
- Red Wizard is selectable by CHARNAME.
- Illusion remains available while the normal Conjurer Divination prohibition remains active.
- Normal specialist slots plus the intrinsic Red Wizard +1 slot for spell levels 1–9 are preserved.
- Spell Power reaches +5 caster levels at level 12+.
- Specialist Defense reaches +7 vs Conjuration at level 16+.
- Enhanced Specialization aura is present.
- Edwin can be assigned `S9REDWIZ`, retains his existing amulet and keeps Illusion spells.
- The Infinity UI++ specialist-school prompt fix remains verified.

## Components
- **0 — Red Wizard (Conjurer) kit**
- **100 — Apply the Red Wizard kit to Edwin**
- **200 — Install alternate portrait for Edwin**

## Compatibility
Supported games:
- Baldur's Gate: Enhanced Edition
- Baldur's Gate II: Enhanced Edition
- Enhanced Edition Trilogy (EET)

Components 0/100 must not be installed together with **The Artisan's Kitpack NPC component #5102 — Red Wizard Mage Kit for Edwin**. Component 200 is independent.

The release package is self-contained and uses the project-reference **WeiDU 249.00** executable.

## Credits
Special thanks and full credit to **The Artisan / TheArtisanBG** for the original Red Wizard design, implementation and assets from **The Artisan's Kitpack**, and for the Edwin portrait used by component 200:
https://theartisanbg.github.io/The-Artisans-Corner/kitpack

`ADD_KIT_EX` is by Argent77.

RedWizard KIT extraction, adaptation, compatibility work and requested design changes: **Sauler89**.
