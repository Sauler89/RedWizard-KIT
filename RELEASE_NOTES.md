# RedWizard KIT v0.1.0-alpha5

This alpha is based on the first real EET installation test of RedWizard KIT.

## What changed
- Both components installed successfully in the supplied EET setup with **zero WeiDU errors and zero warnings**.
- Fixed the Edwin amulet logic introduced in alpha4.
- The original Artisan component replaces `MISC89.ITM` with a custom 546-byte amulet containing nine opcode 42 effects for the Red Wizard's extra wizard spell slots.
- RedWizard KIT already provides those extra slots intrinsically through `S9RWSLOT.SPL`, so component 100 now leaves Edwin's currently installed amulet completely untouched.
- Removed the `S9RWAMU.ITM` clone, opcode-42 deletion and CRE item redirection entirely.
- Component 100 now only assigns `S9REDWIZ` to Edwin's supported CRE variants.
- Edwin still keeps Illusion spells and scripted Mirror Image.

## Core design
- Playable Red Wizard (Conjurer) for CHARNAME.
- Optional Edwin component.
- Normal Conjurer prohibition on Divination is preserved.
- The additional Illusion prohibition is removed.
- Enhanced Specialization, Spell Power, Specialist Defense and +1 extra wizard spell slot per spell level are preserved.

## Compatibility
BG:EE, BG2:EE and EET.

Do not install together with The Artisan's Kitpack NPC component #5102 (Red Wizard Mage Kit for Edwin).

## Credits
Special thanks and full credit to **The Artisan / TheArtisanBG** for the original Red Wizard design, implementation and assets from **The Artisan's Kitpack**:
https://github.com/TheArtisanBG/The-Artisan-s-Kitpack

`ADD_KIT_EX` is by Argent77.

RedWizard KIT extraction, adaptation and compatibility work: **Sauler89**.

## Testing status
The WeiDU installation has now passed on a heavily modded EET installation. In-game CHARNAME/Edwin behavior should still be verified before promoting the project out of alpha status.
