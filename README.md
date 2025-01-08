# Roadmap

## PyGlossary 6.0 (2026 or 2027)

- Drop all deprecated API:

  - Remove `glossary.py`
    - `pyglossary.Glossary` will become `glossary_v2.Glossary`
  - `info=` argument to `Glossary()`
  - Support for `format` variable in plugins:
    - Users must rename it to `name`
  - `Glossary`: `format` arguments to `read`, `directRead` and `write` methods are deprecated
    - Users must rename it to `formatName`

- Switch to `$XDG_CONFIG_HOME/pyglossary` as config dir on Linux/BSD (`core.py`)

- Switch to `toml` for config file (ship with a small `toml` library)

- Aard2 Writer: remove `.slob` file (if exists) before write (to avoid error).

- Kobo Writer: create zip file automatically (in place of the folder, without giving `.zip` extension)

- Add `glossary_v3.py`: break `Glossary` class functionality up into several classes, for example

  - `GlossaryConvertor`
  - `GlossaryCreator`
  - `MemoryLoadedGlossary`
  - `SQLiteLoadedGlossary`

## StarCalendar 4.0 (2025 or 2026)

- Migrate from Gtk3 to Gtk4
- Migrate from `json` to `toml` for config files
- Migrate from `bson` to `msgpack` for event object files
- Script to migrate from `~/.starcal3` to `~/.starcal4`

## AyanDict v3.0 (2025 or 2026)

- Migrate to [miqt](https://github.com/mappu/miqt) and Qt6 (WIP)

## `starcal-server`

- Migrate to GraphQL
- Try switching from MongoDB to [FerretDB](https://github.com/FerretDB/FerretDB)
