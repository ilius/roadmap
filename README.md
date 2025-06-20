# Roadmap

## PyGlossary 6.0 (2026 or 2027)

- Drop all deprecated API:

  - Remove `glossary.py` and `tests/deprecated/`
    - `pyglossary.Glossary` will become `glossary_v2.Glossary`
  - Add `info: dict[str, Any] | None = None` argument to `Glossary()`
  - Support for `format` variable in plugins:
    - Users must rename it to `name`
  - `Glossary`: `format` arguments to `read`, `directRead` and `write` methods are deprecated
    - Users must rename it to `formatName`

- Switch to `$XDG_CONFIG_HOME/pyglossary` as config dir on Linux/BSD (`core.py`)

- Use `$XDG_CACHE_HOME/pyglossary` (if `XDG_CACHE_HOME` is set) as cache dir on Linux/BSD (`core.py`)

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

- `GlossaryInfo`: add `__getattr__` and `__setattr__` methods

- Add `glossary_v3.py`, turn `glossary_v2.py` into a wrapper around it

  - Do not inherit from `GlossaryInfo`, add `self.info = GlossaryInfo()`

    - `glos.setInfo(key, value)` -> `glos.info[key] = value`
    - `glos.getInfo(key)` -> `glos.info[key]`
    - `glos.getExtraInfos(excludeKeys)` -> `glos.info - excludeKeys`
    - `glos.author` -> `glos.info.author`
    - `glos.sourceLang` -> `glos.info.sourceLang`
    - `glos.targetLang` -> `glos.info.targetLang`
    - `glos.sourceLangName` -> `glos.info.sourceLangName`
    - `glos.targetLangName` -> `glos.info.targetLangName`
    - `glos.titleTag` -> `glos.info.titleTag`
    - `glos.detectLangsFromName` -> `glos.info.detectLangsFromName`

  - Break `Glossary` class functionality up into several classes, for example

    - `GlossaryConvertor`
    - `GlossaryCreator`
    - `MemoryLoadedGlossary`
    - `SQLiteLoadedGlossary`

## StarCalendar 4.0 (2025 or 2026)

- Rename `scal3` package to `scal4`

- Migrate from `sha1` to `sha256` for event object hashes

- Rename Jalali calendar to Persian calendar

- Organize/move config parameters into namespaces / classes

  - Rename `labelBox` (Year & Month Bar) main win item/module to `yearMonthBar`
  - Changes in `Font` objects:
    - Replace bold (bool) property with weight (int)
      - `Pango.Weight` ranges from 100 to 1000 (400=NORMAL), let's divide that by 10
    - Save/load as dict (currently it's list)
  - Move `activeCalTypes` and `inactiveCalTypes` config params out of `core.py`
    - Save/load in `scal3.cal_types` module in `cal_types.toml` file

- Migrate from `bson` to `msgpack` for event object files

  - Package `u-msgpack-python`: **pure Python, platform-independent**

    - Size (kB): whl=18, deb:trixie=10, ub:oracular=8.3, arch=22
    - LOC (main folder, no empty lines): 1037 (in one file)
    - [Github](https://github.com/vsergeev/u-msgpack-python)
    - [PyPI](https://pypi.org/project/u-msgpack-python/)
    - [Debian stable](https://packages.debian.org/bookworm/python3-u-msgpack)
    - [Ubuntu](https://packages.ubuntu.com/oracular/python3-u-msgpack)
    - [ArchLinux](https://archlinux.org/packages/extra/any/python-u-msgpack/)

  - Package `msgpack-python`: **platform-dependent**

    - Size (kB, amd64): whl=400, deb:trixie=82, ub:oracular=78, arch=95, fedora=107
    - LOC (main folder, no empty lines): 1020 Python + 1620 C (.h)
    - Many architectures in repos of Debian, Ubuntu, Fedora
    - ArchLinux: **only x86_64**
    - [PyPI](https://pypi.org/project/msgpack/)
    - [Github](https://github.com/msgpack/msgpack-python)
    - [Debian](https://packages.debian.org/bookworm/python3-msgpack)
    - [Ubuntu](https://packages.ubuntu.com/oracular/python3-msgpack)
    - [Fedora](https://packages.fedoraproject.org/pkgs/python-msgpack/python3-msgpack/)
    - [ArchLinux](https://archlinux.org/packages/extra/x86_64/python-msgpack/)

  - Both modules have `packb` and `unpackb` funcs. Their API for extended types seem to be different. But we already convert everything to/from basic types (bool, int, float, str, list, dict) for saving/loading json. So it's probably fine to support both modules.

- Migrate from `json` to `toml` for config files

  - Package `tomlkit`: Style-preserving, can parse and dump/encode

    - Size (kB): whl=38, deb:trixie=41, ub:oracular=36, arch=102, fedora=112
    - [PyPI](https://pypi.org/project/tomlkit)
    - [Github](https://github.com/python-poetry/tomlkit)
    - [Debian](https://packages.debian.org/bookworm/python3-tomlkit)
    - [Ubuntu](https://packages.ubuntu.com/oracular/python3-tomlkit)
    - [Fedora](https://packages.fedoraproject.org/pkgs/python-tomlkit/python3-tomlkit/)
    - [ArchLinux](https://archlinux.org/packages/extra/any/python-tomlkit/)

- Script to migrate from `~/.starcal3` to `~/.starcal4`

  - Export all event groups, accounts and trash to JSON file, then import them to starcal4

- Rename `pixmaps` directory to `images`

## AyanDict v3.0 (2025 or 2026)

- Migrate to [miqt](https://github.com/mappu/miqt) and Qt6 (ready)
  - Need Github action for building for Mac OS (ARM)
  - Need Github action for building for Windows (AMD64 and ARM)

## `starcal-server`

- Migrate to GraphQL
- Try switching from MongoDB to [FerretDB](https://github.com/FerretDB/FerretDB)
