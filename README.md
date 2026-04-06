# WeakAuras 2 — WotLK (3.3.5a) with DBM Timer Fix

A WeakAuras 2 build optimized for WoW 3.3.5a, featuring a compatibility patch for DBM-Warmane pull timer triggers.

## Problem

On WotLK 3.3.5a servers running DBM-Warmane, WeakAuras may throw a Lua error when using the **Other Addons → DBM Timer** trigger:

```
DBM: Error while executing callback function ... for event DBM_TimerStart:
WeakAuras\GenericTrigger.lua:... attempt to index field 'Bars' (a nil value)
```

This occurs because DBM-Warmane does not expose `DBM.Bars` in the same way as modern DBM releases. Auras relying on the DBM Timer trigger fail to activate, and the error spams the chat frame.

## Solution

This fork patches `WeakAuras/GenericTrigger.lua` to safely retrieve DBM timer bar options without assuming `DBM.Bars` exists. The fix implements a fallback chain:

1. `DBT.Options` (preferred, if available)
2. `DBM.Bars.options` (legacy DBM structure)
3. `DBM.Options` or an empty table as a final fallback

This prevents the `DBM_TimerStart` callback from crashing and ensures timer-based auras function correctly.

## Features

- Full WeakAuras 2 functionality for WotLK 3.3.5a
- Patched DBM Timer trigger compatibility
- Optimized for private server environments
- No additional dependencies required

## Installation

1. Download the repository or latest release.
2. Extract the archive and place the `WeakAuras` folder into your WoW addons directory:
   ```
   World of Warcraft 3.3.5a/Interface/AddOns/WeakAuras/
   ```
3. Restart the client or type `/reload` in-game.
4. Verify the addon is enabled on the character selection screen.

## Usage

Open the configuration panel:
```
/wa
```
or
```
/weakauras
```

## Verification

To confirm the DBM Timer fix is working:

1. Ensure DBM-Warmane (or a compatible DBM build) is installed.
2. Create or import an aura using the trigger: `Other Addons` → `DBM Timer`.
3. Start a pull timer in-game:
   ```
   /dbm pull 10
   ```
4. Expected result: The aura triggers correctly, and no Lua errors appear in the chat frame.

## Notes

- This patch targets WotLK 3.3.5a DBM variants with modified internal structures.
- If your DBM build uses different option paths, additional fallbacks may be necessary.
- For bug reports, please include your DBM version, WeakAuras version, and the full Lua error message.

## Upstream Documentation

Official WeakAuras Wiki: https://github.com/WeakAuras/WeakAuras2/wiki