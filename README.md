# Chalise's CK3 Mods

Personal Crusader Kings III mods for achievement hunting.

## Mods

### [Set Up for Success](set_up_for_success/)

A quality-of-life boost mod for time-saving. Adds a one-time Decision that gives your starting ruler (and their spouse) a significant head start without using debug mode or console commands.

**What the decision gives you:**

| Category | Bonus |
|---|---|
| All skills | +20 each |
| Traits | Beautiful, Herculean, Genius, Pure-Blooded, Fecund |
| Lifestyle XP | 1,500 XP in each of the 5 trees (~12+ perk points) |
| Gold | +10,000 |
| Legitimacy | +100 |
| Dynasty Renown | +15,000 (enough for 10+ legacy picks) |
| Domain Limit | +5 |
| Knight Limit | +5 |
| Vassal Limit | +50 |
| Duchy Limit | +5 (hold up to 8 duchies before penalties) |

Spouse gets: all skills, all traits, and all lifestyle XP.

**One-time use per character** - resets on succession so each new ruler can use it once.

**Achievement compatible** - no debug mode, no console commands. As of CK3 patch 1.9+, loading mods no longer disables achievements.

---

## Repo Structure

```
ck3-mods/
├── README.md
├── .gitignore
└── set_up_for_success/          # SUFS Mod
    ├── descriptor.mod
    ├── common/
    │   ├── decisions/
    │   │   └── sufs_decisions.txt
    │   ├── modifiers/
    │   │   └── sufs_modifiers.txt
    │   └── scripted_triggers/
    │       └── 00_title_triggers.txt   # overrides duchy limit globally
    └── localization/
        └── english/
            └── sufs_l_english.yml
```

The outer `<mod_name>.mod` launcher file is **not tracked** (it contains an absolute path specific to the local machine). See Installation below.

---

## Installation

1. Clone this repo:
   ```bash
   git clone git@github.com:chalisegrogan/CK3-Mods-For-Achievement-Hunting.git
   ```

2. For each mod, create a launcher `.mod` file in your CK3 mod folder. The CK3 mod folder is typically:
   - **macOS:** `~/Documents/Paradox Interactive/Crusader Kings III/mod/`
   - **Windows:** `%USERPROFILE%\Documents\Paradox Interactive\Crusader Kings III\mod\`

3. Create `set_up_for_success.mod` in that folder with:
   ```
   name="Set Up for Success"
   version="1.0.0"
   tags={
       "Gameplay"
   }
   supported_version="*.*.*"
   path="/absolute/path/to/ck3-mods/set_up_for_success"
   ```
   Replace `path=` with the actual absolute path to the mod folder in your clone.

4. Enable the mod in the CK3 launcher.

**Tip:** You can symlink the mod folder into the CK3 mod directory instead of copying it, so edits are live immediately:
```bash
ln -s /path/to/ck3-mods/set_up_for_success \
  ~/Documents/Paradox\ Interactive/Crusader\ Kings\ III/mod/set_up_for_success
```

---

## Notes

- **Duchy limit** is implemented as a global override of `has_too_many_held_duchies_trigger` (raises threshold from 3 to 8). This applies to all characters including AI. There's no character-scoped duchy limit.
- **Debug mode behavior:** In debug mode, CK3 shows all decisions regardless of `is_shown` conditions, so the one-time-use gate may appear broken during testing. It works correctly in normal play.
- Tested on CK3 `1.14.x`.
