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

- Add `glossary_v3.py`: break `Glossary` class functionality up into several classes, for example

  - `GlossaryConvertor`
  - `GlossaryCreator`
  - `MemoryLoadedGlossary`
  - `SQLiteLoadedGlossary`

## StarCalendar 4.0 (2025 or 2026)

- Migrate from `json` to `toml` for config files

  - `tomllib` from Python 3.11+ can parse, but not encode/dump
  - Package [toml](https://pypi.org/project/toml/), Github: [@uiri/toml](https://github.com/uiri/toml/)
    - Github repo has no commit since 2023/10/11
    - Fedora: `python3-toml` package will be deprecated in Fedora 38. The upstream toml package is considered unmaintained (see description) and Python 3.11 contains a TOML-reading library in the standard library. Existing Fedora packages depend on python-toml, so we cannot remove it yet. Packagers are encouraged to work with upstreams to switch to tomllib/tomli for reading toml or tomli-w for writing it. But python-toml remains available until it is a leaf package, it will be removed then (possibly not yet in Fedora 38). See [source](https://fedoraproject.org/wiki/Changes/DeprecatePythonToml).
  - Packages [toml](https://pypi.org/project/tomli/) and [tomli-w](https://pypi.org/project/tomli-w/)
    - Github: https://github.com/hukkin/tomli
    - Comment-preserving round-trip parsing is NOT supported
    - Debian: `python3-tomli` and `python3-tomli-w` since Debian 12
    - Ubuntu: `python3-tomli` and `python3-tomli-w` since 22.04 LTS
    - Fedora: `python-tomli` and `python-tomli-w` since Fedora 43
    - ArchLinux: `python-tomli` and `python-tomli-w` since 2021
    - openSUSE: `python-tomli` and `python-tomli-w` in openSUSE Tumbleweed
      - No official repo package for Leap 15.5 or 15.6
      - https://software.opensuse.org/package/python-tomli
      - https://software.opensuse.org/package/python-tomli-w

- Migrate from `bson` to `msgpack` for event object files

  - [msgpack-python](https://github.com/msgpack/msgpack-python)

    - [Debian](https://packages.debian.org/bookworm/python3-msgpack), [Ubuntu](https://packages.ubuntu.com/oracular/python3-msgpack), [Fedora 41](https://packages.fedoraproject.org/pkgs/python-msgpack/python3-msgpack/): many architectures
    - [ArchLinux](https://archlinux.org/packages/extra/x86_64/python-msgpack/): **only x86_64**

  - [u-msgpack-python](https://github.com/vsergeev/u-msgpack-python)

    - [ArchLinux](https://archlinux.org/packages/extra/any/python-u-msgpack/): **platform-independant**
    - [Debian stable](https://packages.debian.org/bookworm/python3-u-msgpack)

  - Both modules have `packb` and `unpackb` funcs. Their API for extended types seem to be different. But we already convert everything to/from basic types (bool, int, float, str, list, dict) for saving/loading json. So it's probably fine to support both modules.

- Rename Jalali calendar to Persian calendar

- Organize/move config parameters into namespaces / classes

  - Rename `labelBox` (Year & Month Bar) main win item/module to `yearMonthBar`
  - Changes in `Font` objects:
    - Replace bold (bool) property with weight (int)
      - `Pango.Weight` ranges from 100 to 1000 (400=NORMAL), let's divide that by 10
    - Save/load as dict (currently it's list)

- Script to migrate from `~/.starcal3` to `~/.starcal4`

## AyanDict v3.0 (2025 or 2026)

- Migrate to [miqt](https://github.com/mappu/miqt) and Qt6 (ready)
  - Need Github action for building for Mac OS (ARM)
  - Need Github action for building for Windows (AMD64 and ARM)

## `starcal-server`

- Migrate to GraphQL
- Try switching from MongoDB to [FerretDB](https://github.com/FerretDB/FerretDB)
