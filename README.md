# WeakAuras 2 — WotLK (3.3.5a)  
## DBM Timer Fix for DBM-Warmane (Warmane-compatible)

This repository contains a **WotLK 3.3.5a** compatible WeakAuras build and includes a small compatibility fix for **DBM-Warmane** pull timers.

---

## ✅ What problem does this fix solve?

On some WotLK 3.3.5a setups (especially with **DBM-Warmane**), **WeakAuras 4.0.0** may throw a Lua error when using the trigger:

> **Other Addons → DBM Timer**

Example error (after `/dbm pull 10`):


DBM: Error while executing callback function ... for event DBM_TimerStart:
WeakAuras\GenericTrigger.lua:... attempt to index field 'Bars' (a nil value)

As a result, any aura relying on DBM Timer triggers may fail to activate.

This fork patches WeakAuras to safely fetch DBM bar options without assuming DBM.Bars exists on DBM-Warmane.
🔧 What was changed?

File modified:

    WeakAuras/GenericTrigger.lua

Fix summary:

    Adds safe fallbacks for DBM timer bar option access:
        Prefer DBT.Options when available
        Otherwise use DBM.Bars.options (if present)
        Otherwise use DBM.Options or an empty table

This prevents the DBM_TimerStart callback from crashing WeakAuras.
⭐ WeakAuras Features (short)

WeakAuras is a powerful and flexible framework for creating highly customizable UI displays to track:

    Buffs / debuffs
    Cooldowns
    Combat events
    Items / procs
    Resources (mana, rage, runes, holy power, etc.)
    Many other triggers

📦 Installation (WotLK 3.3.5a)

   1. Download or clone this repository.

   2. Copy the WeakAuras folder into:
    World of Warcraft 3.3.5a/Interface/AddOns/

   3. Restart the game or type:
    /reload

🚀 Quick Start

Open the WeakAuras options window:

    /wa

    or

    /weakauras

🧪 How to verify the DBM Timer fix

    Install DBM-Warmane (or any DBM build that supports /dbm pull).

    Create or import any aura that uses:
        Other Addons → DBM Timer

    In-game, run:

    /dbm pull 10

✅ If the fix is working:

    The aura triggers correctly
    No Lua errors related to DBM_TimerStart / DBM.Bars appear

📝 Notes

    This fix is intended for WotLK 3.3.5a DBM variants where internal structures differ from modern DBM builds.
    If your DBM build exposes different option fields, additional fallbacks may be required.
    Please open an issue and include:
        Your DBM version
        The full Lua error message

📚 Upstream Documentation

Official WeakAuras wiki:
https://github.com/WeakAuras/WeakAuras2/wiki