# Changelog

## v1.1.0
- Added optional component **200 — Install alternate portrait for Edwin**.
- Uses the Edwin portrait displayed on The Artisan's Corner for The Artisan's Kitpack, with explicit credit to **The Artisan / TheArtisanBG**.
- Added standard EE 24-bit BMP portrait variants: 210×330 Large, 169×266 Medium and 54×84 Small.
- Installs both `EDWINL/M/S` and `NEDWINL/M/S`, covering BG:EE, BG2:EE and both portions of EET.
- The portrait component overrides portrait resources directly and therefore works with existing saves without editing Edwin's CRE files.
- The L/M/S resource approach is compatible with both the vanilla Enhanced Edition UI and Infinity UI++ without a UI-specific portrait patch.
- Added the Edwin portrait as an image on the repository main README page.
- Components 0 and 100 retain the validated v1.0.0 gameplay implementation unchanged apart from the mod version string.

## v1.0.0
- First stable release of RedWizard KIT.
- Promoted the fully validated `v0.1.0-beta1` implementation with no gameplay-mechanics changes.
- Stable release retains the verified Infinity UI++ Conjuration school-token mapping for `S9REDWIZ`.
- Stable release retains the validated Red Wizard mechanics: Illusion available, normal Conjurer Divination prohibition, intrinsic extra spell slots, Spell Power, Specialist Defense, Enhanced Specialization aura, and Edwin integration.
- Stable release retains the validated WeiDU 249.00 packaging pipeline and self-contained release archive.
- `RedWizardKIT.tp2` is identical to `v0.1.0-beta1` except for the version string.

## v0.1.0-beta1
- Promoted the fully validated alpha8 code to the first beta with no gameplay-mechanics changes.
- Confirmed the alpha8 Infinity UI++ fix in-game: Red Wizard now displays `Select at least one conjuration spell to proceed.` instead of the raw `<SCHOOLTOKEN>` placeholder.
- Confirmed stock specialist prompts remain correct after the Red Wizard UI patch, including Diviner (`divination`) and Abjurer (`abjuration`).
- Confirmed the real alpha8 WeiDU installation log contains zero errors and zero warnings, installs both components successfully, registers `S9REDWIZ`, and reports the Infinity UI++ compatibility patch as applied.
- Retained all previously runtime-validated mechanics: Illusion availability, normal Conjurer Divination prohibition, intrinsic extra spell slots, Spell Power, Specialist Defense, Enhanced Specialization aura, and Edwin integration.
- `RedWizardKIT.tp2` is identical to the validated alpha8 implementation except for the version string.

## v0.1.0-alpha8
- Audited the user's actual installed `UI.MENU` instead of relying on upstream assumptions.
- Identified the exact Infinity UI++ code path that resolves `<SCHOOLTOKEN>`: `rgChooseSpellsMenuOnOpen()` compares `currentKitName` against the stock specialist kit names and calls `setStringTokenLua()` for each vanilla school.
- Confirmed the Red Wizard reaches the specialist-spell requirement correctly but never enters the stock Conjurer-name branch because `S9REDWIZ` has its own kit name.
- Replaced the ineffective alpha7 label-level fallback with a precise kit-ID mapping inserted immediately before Infinity UI++'s stock specialist mapping.
- `S9REDWIZ` now explicitly maps to `CONJURATION_SCHOOL_TOKEN` through Infinity UI++'s own localized `getUiString()` path.
- Stock specialist mages and all other kits retain the original Infinity UI++ logic unchanged.
- The patch is keyed to the actual `rgChooseSpellsMenuOnOpen()` / Abjurer mapping found in the supplied `UI.MENU`, and is applied only when that exact structure is present.
- No gameplay mechanics, spell availability, CLAB progression, Edwin handling, spell slots, Spell Power or Specialist Defense were changed.

## v0.1.0-alpha7
- Audited the real alpha6 WeiDU DEBUG: both components install successfully with zero errors and zero warnings.
- Discovered that the alpha6 `<SCHOOLTOKEN>` compatibility branch did not execute in the tested EET setup because `m_dw_ssd.lua` is not installed there.
- Kept the SCS/SFO `dwKitSpecLearnLine` hook for installations where that subsystem is actually present.
- Added a direct Infinity UI++ fallback that patches only the `SPECIALIST_SPELL_REQ` label and only changes its text when the currently selected kit is `S9REDWIZ`.
- All stock specialist mages and all other kits continue using Infinity UI++'s original prompt logic unchanged.
- Added an explicit WeiDU diagnostic message when the Infinity UI++ fallback is detected and applied, making the next DEBUG easy to verify.
- No gameplay mechanics, spell availability, CLAB progression, Edwin handling, spell slots, Spell Power or Specialist Defense were changed.

## v0.1.0-alpha6
- Audited a real level-31 Red Wizard `.CHR` and Edwin directly from a supplied `BALDUR.gam` save.
- Confirmed CHARNAME has the normal specialist spell-slot progression plus the separate nine-level `S9RWSLOT` Red Wizard bonus.
- Confirmed Specialist Defense is applied exactly as designed: one +2 Conjuration save effect from `S9RWBASE` plus five +1 `S9RWDEF` effects, for +7 vs Conjuration at level 16+.
- Confirmed level-31 Spell Power is present as opcode 191 with value +5 and the Enhanced Specialization repeating aura is present.
- Confirmed Edwin is assigned `S9REDWIZ`, keeps `MISC89`, keeps his native BG2 amulet slot bonuses, and separately receives the Red Wizard slot bonus.
- Confirmed Edwin retains all seven Illusion spells removed by the original Artisan component, including memorized Illusion spells.
- Added an SCS/SFO `dwKitSpecLearnLine` compatibility path for the raw `<SCHOOLTOKEN>` prompt; alpha7 extends this with the required Infinity UI++ fallback.
- The known `{K=...,C=...}` class-name artifact from SCS + Infinity UI++ is external to RedWizard KIT and is intentionally not patched here.

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
