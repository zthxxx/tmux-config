<div align="center">

# zthxxx/tmux-config

A modern, ergonomic tmux configuration built for daily use —
with sane defaults, Vi-style pane splits, F-key window management, and plugin support.

</div>

---

## What's Different from Default tmux

| Feature | Default tmux | This config |
|---|---|---|
| Prefix key | `Ctrl-B` | `Ctrl-S` |
| Mode keys | `vi` | `emacs` |
| Pane/window base index | `0` | `1` |
| Mouse | off | on (toggleable via F10) |
| Escape time | 500ms | 0ms |
| Scroll history | 2000 lines | 65535 lines |
| Window names | manual | auto (directory basename) |
| Window renumbering | off | on (gaps closed automatically) |
| Status bar background | solid color | transparent |
| Copy-mode drag | exits copy mode | stays in copy mode |
| Terminal passthrough | off | on (supports yazi image preview, kitty, ghostty) |
| Extended key support | off | on (xterm-256color, kitty, ghostty) |

---

## Installation

```bash
mkdir -p ~/.config/tmux
curl -L https://github.com/zthxxx/tmux-config/raw/main/tmux.conf -o ~/.config/tmux/tmux.conf
```

### Install Plugins (optional but recommended)

```bash
# Install Tmux Plugin Manager
git clone --depth=1 https://github.com/tmux-plugins/tpm ~/.config/tmux/plugins/tpm
```

Then inside tmux, press **`prefix + I`** to fetch and load all plugins.

#### treemux Requirements

The [treemux](https://github.com/kiyoon/treemux) plugin requires `Neovim` and `pynvim`:

```bash
uv tool install --upgrade pynvim
# or: pip install pynvim
```


### Development (symlink)

```bash
git clone --depth=1 git@github.com:zthxxx/tmux-config.git tmux-config
cd tmux-config
mkdir -p ~/.config/tmux
ln -fs "$(pwd)/tmux.conf" ~/.config/tmux/tmux.conf
```

and also need install TPM as above.

---

## Keybindings

### Prefix

The prefix is **`Ctrl-S`** (instead of the default `Ctrl-B`).

Press `prefix + Ctrl-S` to send the prefix through to a nested tmux session.

---

### Window Management (no prefix needed)

| Key | Action |
|---|---|
| `Alt+1` … `Alt+0` | Jump to window 1–10 |
| `Alt+Shift+1` … `Alt+Shift+9` | Move current pane to window 1–9 |
| `F2` / `Ctrl-F2` | Previous window |
| `F3` / `Ctrl-F3` | Next window |
| `F5` / `Ctrl-F5` | New window (opens in current directory) |
| `F6` / `Ctrl-F6` | Detach from session |
| `F7` | Kill current pane |
| `F8` | Rename current window (pre-filled with current name) |
| `Ctrl-F8` | Rename current session (pre-filled with current name) |
| `F10` | Toggle mouse on/off |
| `F12` | Enter nested-tmux pass-through mode |

> **Ctrl-F\* alternatives** are provided for VSCode's integrated terminal where bare F-keys may be intercepted.

---

### Pane Splits (prefix required)

Splits open in the current pane's directory with vim style. Layout mnemonic:

```
     K
  H  J  L
```

| Key | Action |
|---|---|
| `prefix + k` | Split above (new pane on top) |
| `prefix + j` | Split below (new pane on bottom) |
| `prefix + h` | Split left |
| `prefix + l` | Split right |

---

### Window Reordering (prefix required)

| Key | Action |
|---|---|
| `prefix + <` | Move window one position left (repeatable) |
| `prefix + >` | Move window one position right (repeatable) |

---

### Search (prefix required)

| Key | Action |
|---|---|
| `prefix + /` | Enter copy mode and open incremental forward search |
| `/` *(in copy mode)* | Open incremental forward search |
| `Ctrl-r` *(in copy mode)* | Search backward (default emacs binding) |
| `n` / `N` *(in copy mode)* | Next / previous match |

---

### Mouse & Copy Mode

Mouse is enabled by default. Drag to select text — the selection is copied **without** exiting copy mode (preserves scroll position). Double-click selects and copies a word.

---

### Config Reload (prefix required)

| Key | Action |
|---|---|
| `prefix + Ctrl-R` | Reload `~/.config/tmux/tmux.conf` |

---

### Nested tmux Mode

Press **`F12`** to toggle nested-tmux pass-through mode. In this mode:
- The prefix is suspended so all keystrokes pass to the inner tmux session.
- The status bar turns teal to indicate pass-through is active.
- Press **`F12`** again to return to normal mode.

---

## Plugins

| Plugin | Purpose | Key Bindings |
|---|---|---|
| [TPM](https://github.com/tmux-plugins/tpm) | Plugin manager | `prefix+I` install, `prefix+U` update, `prefix+Alt+u` clean |
| [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect) | Save/restore sessions across reboots | `prefix+Alt+Shift+S` save, `prefix+Alt+Shift+R` restore |
| [treemux](https://github.com/kiyoon/treemux) | Neovim-powered sidebar file tree | `prefix+Tab` toggle, `prefix+Backspace` toggle & focus |

---

## Status Bar

```
tmux: <session> | ... windows ...              <hostname> | YYYY-MM-DD HH:MM:SS
```

- Left: session name
- Center: window list — current window is **bold + reversed**; windows with activity are underlined
- Right: hostname and live clock (updates every second)
- Background is transparent (inherits terminal background)
- The top border of the status bar is rendered via pane border, giving a clean overline effect
