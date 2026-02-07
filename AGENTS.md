# AGENTS.md

This file provides guidance to AI Agent (like [Claude Code](https://claude.ai/code)) when working with code in this repository.

## Repository Overview

A single-file tmux configuration (`tmux.conf`) intended as a shareable, drop-in config for others.
The only other meaningful file is `README.md`, which documents the config for end users.

## Key Rule

**Any config change that affects user-visible behavior — keybindings, settings, plugins — must also be reflected in `README.md`.**

This includes:
- Adding, removing, or rebinding keys
- Enabling/disabling features (mouse, passthrough, etc.)
- Adding or removing plugins and their bindings
- Changing the prefix key

## Structure

```
tmux.conf    ← the entire configuration (single source of truth)
README.md    ← user-facing docs: install guide, keybinding reference, feature comparison
```

## Config Sections (in order)

1. **Common settings** — escape time, repeat time, focus events, passthrough, extended keys
2. **Mouse & copy-mode** — mouse scroll behavior, copy-without-exit-copy-mode bindings
3. **Search bindings** — `/` and `Ctrl-R` in copy mode
4. **Window display** — base index, auto-rename, renumbering, titles
5. **Prefix key** — remapped from `Ctrl-B` to `Ctrl-S`
6. **Window navigation** — `Alt+N` to jump, `F2/F3` prev/next, `F5/F6/F7/F8` lifecycle
7. **Pane splits** — `h/j/k/l` directional splits
8. **Nested tmux** — `F12` pass-through toggle using `nest-tmux` key-table
9. **Window reordering** — `<` / `>` swap
10. **Theme** — transparent status bar, pane border overline effect
11. **Plugins** — TPM, tmux-resurrect, treemux

## Conventions

- All prefix bindings use `bind-key` (no `-n`); root-table bindings use `-n`
- Repeatable bindings use `-r`
- Comments above each binding group explain the intent and any non-obvious behavior
- Plugin config comes after all manual bindings, with `run '...tpm/tpm'` as the very last line
