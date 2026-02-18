# ghostty-vibe-coding-stack

[中文文档](README.zh.md)

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that configures a complete terminal-based AI coding environment. Replaces heavy IDEs with lightweight, composable TUI tools on macOS with Apple Silicon — with CJK font optimization for Chinese/Japanese/Korean users.

| Tool | Purpose | Why |
|------|---------|-----|
| **Ghostty** | GPU-accelerated terminal | Native splits, Quick Terminal, fast rendering |
| **Fish** | Shell | Best-in-class autosuggestions, zero config |
| **Tide** | Prompt theme | Powerlevel10k equivalent for Fish |
| **yazi** | File manager (TUI) | Image preview, Kitty protocol, fast navigation |
| **lazygit** | Git client (TUI) | Visual staging, diff, branch management |
| **Neovim** | Editor (LazyVim) | LSP, treesitter, when you need a quick edit |
| **fzf** | Fuzzy finder | File search, history, pipe filtering |
| **zoxide** | Smart cd | Jump to directories by keyword |
| **atuin** | Shell history | Searchable, filterable, cross-terminal sync |
| **fd / rg / bat / delta** | CLI replacements | Faster find, grep, cat, diff |

## Installation

### Via `npx skills` (recommended)

```bash
npx skills add psylch/ghostty-vibe-coding-stack
```

Or install to Claude Code specifically:

```bash
npx skills add psylch/ghostty-vibe-coding-stack -a claude-code
```

### Via Plugin Marketplace

In Claude Code:

```
/plugin marketplace add psylch/ghostty-vibe-coding-stack
/plugin install configuring-ghostty-vibe-stack@psylch-ghostty-vibe-coding-stack
```

### Manual Install

```bash
git clone https://github.com/psylch/ghostty-vibe-coding-stack.git ~/.claude/skills/ghostty-vibe-coding-stack
```

Restart Claude Code after installation.

## Prerequisites

- **macOS** with Apple Silicon (M1+)
- **Homebrew** installed
- **Ghostty** terminal installed ([ghostty.org](https://ghostty.org))
- **Claude Code** for AI-assisted development

## Usage

In Claude Code, use any of these trigger phrases:

```
configure my terminal environment
setup ghostty vibe coding stack
配置 Ghostty
终端配置
开发环境搭建
```

The skill will guide Claude through installing and configuring the entire stack.

## What Gets Configured

### Ghostty
- CJK font fallback chain (Maple Mono NF CN → Sarasa Term SC → JetBrains Mono NF → PingFang SC)
- Liquid Glass style (transparency, blur, display-p3 color)
- Native splits (`Cmd+D` / `Cmd+Shift+D`) and tab navigation
- Quick Terminal (global `` Ctrl+` `` dropdown)
- Theme with dark/light auto-switching

### Fish Shell
- Tide prompt theme
- Custom key bindings (Tab/→ swap for intuitive completion)
- fzf, zoxide, atuin integrations
- Aliases: `y`=yazi, `lg`=lazygit, `v`=nvim, `cc`=claude, `z`=zoxide

### lazygit
- Monokai / TokyoNight / Rose Pine color themes
- delta as diff pager (syntax-highlighted diffs)
- Nerd Font v3 icons, rounded borders

### yazi
- Hidden files shown, natural sort
- nvim as default editor

## Typical Layout

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

## Known Issues

- **Ghostty does not support `Cmd+V` image paste** for Claude Code ([Discussion #10117](https://github.com/ghostty-org/ghostty/discussions/10117)). Use `Ctrl+V` instead.
- **Ghostty theme names require exact casing** with spaces (e.g., `Rose Pine` not `rose-pine`). Validate with `ghostty +validate-config`.
- **Fish `bind` syntax differs from Zsh** — use `bind right complete`, not `bind -k right complete`.

## File Structure

```
ghostty-vibe-coding-stack/
├── .claude-plugin/
│   ├── marketplace.json              # Plugin registry
│   └── plugin.json                   # Plugin manifest
├── skills/
│   └── configuring-ghostty-vibe-stack/
│       ├── SKILL.md                  # Main skill definition
│       └── references/
│           ├── ghostty-config.md     # Full Ghostty config + themes
│           ├── fish-config.md        # Full Fish config + keybinds
│           ├── lazygit-config.md     # lazygit themes (Monokai/Tokyo/Rose Pine)
│           └── yazi-config.md        # yazi config + keybinds
├── README.md
├── README.zh.md
└── LICENSE
```

## License

MIT
