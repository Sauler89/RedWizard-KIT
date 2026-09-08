# Changelog

## v0.1.0-alpha5
- Audited the first real EET installation DEBUG: both components installed successfully with zero WeiDU errors and zero warnings.
- Identified a logic flaw in alpha4's Edwin amulet de-stacking code.
- Confirmed from The Artisan's original `redwizard.tpa` that the source component replaces `MISC89.ITM` with its own 546-byte amulet containing nine opcode 42 spell-slot effects.
- Confirmed the user's current EET `MISC89.ITM` is the minimal 114-byte item and therefore does not contain those slot effects before RedWizard KIT is installed.
- Removed all `MISC89.ITM` cloning, opcode deletion and CRE item redirection from component 100.
- Edwin's currently installed amulet is now left completely untouched.
- The Red Wizard's +1 wizard spell slot at spell levels 1-9 remains intrinsic to the kit through `S9RWSLOT.SPL`.
- Component 100 now does only what is necessary: assign `S9REDWIZ` to Edwin's supported CRE variants while preserving Illusion spells and scripted Mirror Image.

## v0.1.0-alpha4
- Renamed the mod completely to **RedWizard KIT**.
- Renamed installer to `Setup-RedWizardKIT.exe`.
- Renamed mod folder and TP2 to `RedWizardKIT/RedWizardKIT.tp2`.
- Renamed WeiDU backup/group/metadata branding to RedWizard KIT.
- Added repository-ready README with explicit credit to **The Artisan / TheArtisanBG** and the original Kitpack repository.
- Kept all validated `S9*` technical resource identifiers unchanged to avoid unnecessary binary churn.
- No gameplay mechanics changed from alpha3.

## v0.1.0-alpha3
- Re-audited RedWizard KIT against the user-supplied Artisan's Kitpack master.
- Removed the alpha1-only Human-only restriction (`kittable = K_M_H`), which was not implemented by the original Red Wizard kit definition.
- Retained the source non-good alignment restriction.
- Reconfirmed `0x00001080 -> 0x00000080` as the mechanical removal of Edwin's additional Illusion prohibition while retaining Conjurer usability.
- Reconfirmed that no source Red Wizard spell mechanics changed beyond namespacing.
- Reconfirmed the intrinsic +1 spell-slot-per-level implementation for CHARNAME and the then-current Edwin amulet de-stacking logic.
- Added existing-save guidance for Edwin testing.
- Added redistribution/licensing caution for the original Red Wizard assets.
- Replaced the setup executable with the exact user-supplied WeiDU 249.00 binary.

## v0.1.0-alpha1
- Extracted the Red Wizard into an independent two-component WeiDU mod.
- Added CHARNAME-selectable Red Wizard (Conjurer).
- Removed the additional prohibited school by changing the kit usability mask from `0x00001080` to `0x00000080`.
- Preserved the normal Conjurer prohibited school.
- Added the Red Wizard's additional +1 wizard spell slot per spell level intrinsically to the kit.
- Added optional Edwin assignment component.
- Edwin keeps Illusion spells and scripted Mirror Image.
- Namespaced kit/resources with the `S9` prefix.
