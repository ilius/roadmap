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

- Require Python 3.11 or later

- Switch to `toml` for config file (use `tomllib` from standard lib)

- Config: replace `skip_resources` with `resources`:

  - `--skip-resources` flag becomes `--no-resources`

- Config: replace `color.*` keys with new keys

  - `color.enable.cmd.unix` -> `cmd.color.enable.unix`
  - `color.enable.cmd.windows` -> `cmd.color.enable.windows`
  - `color.cmd.critical` -> `cmd.color.critical`
  - `color.cmd.error` -> `cmd.color.error`
  - `color.cmd.warning` -> `cmd.color.warning`

- Aard2 Writer: remove `.slob` file (if exists) before write (to avoid error).

- Kobo Writer: create zip file automatically (in place of the folder, without giving `.zip` extension)

- AppleDict writer: rename option `indexes` to `index_lang`

- Add `glossary_v3.py`: break `Glossary` class functionality up into several classes, for example

  - `GlossaryConvertor`
  - `GlossaryCreator`
  - `MemoryLoadedGlossary`
  - `SQLiteLoadedGlossary`

## StarCalendar 4.0 (2025 or 2026)

- Migrate from Gtk3 to Gtk4
- Migrate from `json` to `toml` for config files
  - Use or ship with [toml](https://pypi.org/project/toml/) to dependencies
    - `tomllib` from Python 3.11+ can only parse, not encode/dump
    - Debian: `python3-toml` since Debian 10
    - Ubuntu: `python3-toml` since Ubuntu 20.04 LTS
    - ArchLinux: `python-toml` since 2018
- Migrate from `bson` to `msgpack` for event object files
- Rename Jalali calendar to Persian calendar
- Script to migrate from `~/.starcal3` to `~/.starcal4`

## AyanDict v3.0 (2025 or 2026)

- Migrate to [miqt](https://github.com/mappu/miqt) and Qt6 (ready)
  - Need Github action for building for Mac OS (ARM)
  - Need Github action for building for Windows (AMD64 and ARM)

## `starcal-server`

- Migrate to GraphQL
- Try switching from MongoDB to [FerretDB](https://github.com/FerretDB/FerretDB)
