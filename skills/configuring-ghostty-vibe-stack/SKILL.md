---
name: configuring-ghostty-vibe-stack
description: "Configures a complete terminal-based AI coding environment centered on Ghostty terminal with Fish shell, yazi, lazygit, Neovim (LazyVim), fzf, zoxide, atuin, and supporting tools. Includes CJK font optimization for Chinese/Japanese/Korean users on macOS with Apple Silicon. This skill should be used when setting up or modifying a Ghostty-based development environment, configuring terminal tools for vibe coding workflows, or troubleshooting Ghostty/Fish/yazi/lazygit issues."
---

# Ghostty Vibe Coding Stack

A complete terminal-based AI coding environment for macOS (Apple Silicon). Replaces heavy IDEs with lightweight, composable tools optimized for Claude Code / AI-assisted development.

## Stack Overview

| Tool | Purpose | Alias |
|------|---------|-------|
| **Ghostty** | GPU-accelerated terminal | - |
| **Fish** | Shell with autosuggestions | - |
| **Tide** | Fish prompt theme | - |
| **yazi** | TUI file manager | `y`, `yy` |
| **lazygit** | TUI Git client | `lg` |
| **Neovim** | Editor (LazyVim distro) | `v` |
| **fzf** | Fuzzy finder | `Ctrl+R` |
| **zoxide** | Smart cd | `z` |
| **atuin** | Enhanced shell history | `Ctrl+R` |
| **fd** | Fast file finder | `fd` |
| **ripgrep** | Fast code search | `rg` |
| **bat** | Syntax-highlighted cat | `bat` |
| **delta** | Better git diff pager | - |

## Installation

Install all tools via Homebrew:

```bash
brew install fish yazi lazygit neovim fzf zoxide atuin fd ripgrep bat git-delta
```

Install fonts (CJK-optimized with Nerd Icons):

```bash
brew install --cask font-maple-mono-nf-cn font-sarasa-gothic font-jetbrains-mono-nerd-font
```

Install Fish plugins:

```bash
fish -c "fisher install IlanCosman/tide@v6"
```

Install LazyVim:

```bash
git clone https://github.com/LazyVim/starter ~/.config/nvim && rm -rf ~/.config/nvim/.git
```

Register Fish as allowed shell:

```bash
echo /opt/homebrew/bin/fish | sudo tee -a /etc/shells
```

Set Ghostty as default terminal (replaces Finder "Open in Terminal"):

```bash
cat << 'EOF' > /tmp/set_default_terminal.swift
import CoreServices
let result = LSSetDefaultRoleHandlerForContentType(
    "public.unix-executable" as CFString, .shell,
    "com.mitchellh.ghostty" as CFString)
print(result == 0 ? "Success" : "Failed: \(result)")
EOF
swiftc /tmp/set_default_terminal.swift -o /tmp/set_default_terminal && /tmp/set_default_terminal
```

## Configuration

For complete config files, see:

- **Ghostty**: [references/ghostty-config.md](references/ghostty-config.md)
- **Fish**: [references/fish-config.md](references/fish-config.md)
- **lazygit**: [references/lazygit-config.md](references/lazygit-config.md)
- **yazi**: [references/yazi-config.md](references/yazi-config.md)

## Typical Workflow Layout

Use Ghostty native splits (no tmux needed):

```
┌──────────────┬──────────────────────┐
│  yazi (y)    │  Claude Code (cc)    │
│  file tree   │  or Neovim (v)       │
│  + preview   │                      │
│              ├──────────────────────┤
│              │  lazygit (lg)        │
│              │  or dev server       │
└──────────────┴──────────────────────┘
```

- `Cmd+D` split right → left: `y`, right: `cc`
- `Cmd+Shift+D` split down on right pane → bottom: `lg`
- `Cmd+Alt+Arrow` to navigate between panes

## CJK Font Optimization

CJK users MUST configure font fallback chain to avoid rendering issues (oversized characters, misaligned spacing, sudden serif font fallback). Use fonts with built-in Nerd Icons and 1:2 halfwidth:fullwidth ratio.

Recommended font-family order:

1. **Maple Mono NF CN** — primary, CJK + Nerd Icons integrated
2. **Sarasa Term SC** — CJK fallback, perfect terminal metrics
3. **JetBrainsMono Nerd Font** — Latin fallback
4. **PingFang SC** — system fallback (macOS built-in)

Enable `font-thicken = true` to prevent thin/blurry CJK rendering. Set `font-size` to 15-16 (slightly larger than default 14 for CJK readability).

## Quick Terminal

Ghostty supports a global dropdown terminal (Quake-style):

```ini
keybind = global:ctrl+grave_accent=toggle_quick_terminal
quick-terminal-position = top
quick-terminal-screen = main
quick-terminal-animation-duration = 0.15
```

Press `` Ctrl+` `` from any app to toggle the terminal overlay.

## Troubleshooting

**Theme names require exact casing with spaces**:
- Wrong: `rose-pine`, `tokyo-night`
- Correct: `Rose Pine`, `TokyoNight Storm`
- List available: `ghostty +list-themes`
- Validate config: `ghostty +validate-config`

**Cmd+V does not paste images into Claude Code** (Ghostty bug, [Discussion #10117](https://github.com/ghostty-org/ghostty/discussions/10117)):
- Use `Ctrl+V` instead, or drag-and-drop image files

**Fish key binding syntax differs from Zsh**:
- Wrong: `bind -k right complete` (`-k` is zsh syntax)
- Correct: `bind right complete`
- Also override raw escape: `bind \e\[C complete`

**Chinese text too large or misaligned**:
- Add CJK font as first `font-family` entry
- Set `adjust-cell-height = 20%`

**List available fonts**: `ghostty +list-fonts`
