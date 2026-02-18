# Ghostty Configuration

Config path: `~/.config/ghostty/config`

## Complete Config

```ini
# Shell
command = /opt/homebrew/bin/fish

# Font - CJK optimized fallback chain
font-family = Maple Mono NF CN
font-family = Sarasa Term SC
font-family = JetBrainsMono Nerd Font
font-family = PingFang SC
font-size = 15
font-thicken = true

# Theme
# Popular dark themes: Monokai Vivid, Rose Pine, TokyoNight Storm, Catppuccin Mocha
# Auto dark/light: theme = dark:Rose Pine,light:Rose Pine Dawn
theme = Monokai Vivid

# Window - Liquid Glass style
background-opacity = 0.88
background-blur-radius = 20
window-padding-x = 16
window-padding-y = 16
window-decoration = true
macos-titlebar-style = tabs
window-colorspace = display-p3

# Typography
adjust-cell-height = 20%

# Splits
keybind = super+d=new_split:right
keybind = super+shift+d=new_split:down

# Navigate splits
keybind = super+alt+left=goto_split:left
keybind = super+alt+right=goto_split:right
keybind = super+alt+up=goto_split:up
keybind = super+alt+down=goto_split:down

# Tabs
keybind = super+t=new_tab

# Clipboard
clipboard-paste-protection = false
copy-on-select = clipboard

# Cursor
cursor-style = bar
cursor-style-blink = false

# Scrollback
scrollback-limit = 10000

# Quick Terminal (global dropdown terminal)
keybind = global:ctrl+grave_accent=toggle_quick_terminal
quick-terminal-position = top
quick-terminal-screen = main
quick-terminal-animation-duration = 0.15

# Shell integration
shell-integration = detect
```

## Theme Selection

Use exact names (with spaces). Verify with `ghostty +list-themes`.

Popular choices:
- **Monokai Vivid** — vibrant, classic
- **Rose Pine** / **Rose Pine Dawn** — elegant, low-contrast
- **TokyoNight Storm** — deep blue, eye-friendly
- **Catppuccin Mocha** — pastel dark

Auto dark/light switching:
```ini
theme = dark:Rose Pine,light:Rose Pine Dawn
theme = dark:TokyoNight Storm,light:TokyoNight Day
```

## Keybinds Reference

| Shortcut | Action |
|----------|--------|
| `Cmd+D` | Vertical split |
| `Cmd+Shift+D` | Horizontal split |
| `Cmd+Alt+Arrow` | Navigate splits |
| `Cmd+T` | New tab |
| `` Ctrl+` `` | Toggle Quick Terminal (global) |

## Validation

Always validate after editing config:
```bash
ghostty +validate-config
```
