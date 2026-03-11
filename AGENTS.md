# talon-community — Shared Talon Commands

Fork of [talonhub/community](https://github.com/talonhub/community). Provides standard voice commands for general computing. Unless absolutely necessary **do not edit files here directly** — override in `jeans-talon/` if at all possible.

## Directory Structure

| Directory        | Purpose                                                                               |
| ---------------- | ------------------------------------------------------------------------------------- |
| `core/`          | Core functionality: keys, edit, text, formatters, numbers, modes, help, app switching |
| `apps/`          | App-specific commands (77+ apps: Chrome, VSCode, Terminal, etc.)                      |
| `tags/`          | Tag-activated command groups: browser, terminal, debugger, find, messaging, emoji     |
| `lang/`          | Language-specific rules (27+ languages): keywords, types, functions                   |
| `plugin/`        | Optional features: mouse control, command history, macros, media, draft window        |
| `settings/`      | CSV data files: `abbreviations.csv`, `file_extensions.csv`, `words_to_replace.csv`    |
| `settings.talon` | Global settings (imgui scale, feature toggles, user defaults)                         |

## Finding Things

**Action definitions** — search `.py` files for `def action_name`:

- `core/` for general actions (edit, format, navigate)
- `apps/` for app-specific overrides
- `tags/` for tag-scoped actions

**List definitions** — two places:

- `.talon-list` files (e.g., `core/keys/letter.talon-list` for phonetic alphabet)
- Python: `mod.list()` declaration + `ctx.lists["user.name"] = {...}` population

**Tag definitions** — `core/tags.py` bulk-defines common tags; others in feature `.py` files via `mod.tag()`

**Captures** — `core/numbers/numbers.py`, `core/keys/keys.py`, etc. — `@mod.capture(rule=...)` decorators

**Settings** — `settings.talon` at root for values; declarations via `mod.setting()` in `.py` files

## Customization (Without Editing Community)

1. **Override actions** — Create a context in `jeans-talon/` with more-specific matchers; Talon picks the most-specific match
2. **Override lists** — Create a `.talon-list` file with the same `list: user.name` header in `jeans-talon/`
3. **Add commands** — Create new `.talon` files in `jeans-talon/` with the same context matchers
4. **Override settings** — Set values in your own `settings.talon` (more-specific context wins)

## Key Files

- `settings.talon` — Global settings and tag activation
- `core/keys/letter.talon-list` — Phonetic alphabet (air=a, bat=b, cap=c, ...)
- `core/edit/edit.talon` — Universal edit commands
- `core/formatters/` — Text formatters (snake_case, CamelCase, etc.)
- `core/help/` — Help system (`help active`, `help search`, `help alphabet`)
- `core/modes/modes.py` — Sleep/wake/dictation mode logic
- `core/user_settings.py` — CSV settings loader with `resource.watch()`
