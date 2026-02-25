---
name: configuring-ghostty-vibe-stack
description: "Configures a complete terminal-based AI coding environment centered on Ghostty terminal with Fish shell, yazi, lazygit, Neovim (LazyVim), fzf, zoxide, atuin, and supporting tools. Includes CJK font optimization for Chinese/Japanese/Korean users on macOS with Apple Silicon. This skill should be used when setting up or modifying a Ghostty-based development environment, configuring terminal tools for vibe coding workflows, or troubleshooting Ghostty/Fish/yazi/lazygit issues."
---

## Language
**Match user's language**: Respond in the same language the user uses.

# Ghostty Vibe Coding Stack

A complete terminal-based AI coding environment for macOS (Apple Silicon). Replaces heavy IDEs with lightweight, composable tools for Claude Code / AI-assisted development.

## How It Works

Follow these steps in order. Skip steps where the tool is already installed.

Copy this checklist and track progress:

```
Setup Progress:
- [ ] Step 1: Pre-flight checks
- [ ] Step 2: Install Ghostty
- [ ] Step 3: Install CLI tools
- [ ] Step 4: Install fonts
- [ ] Step 5: Configure Ghostty
- [ ] Step 6: Configure Fish shell
- [ ] Step 7: Install Fish plugins
- [ ] Step 8: Configure lazygit
- [ ] Step 9: Configure yazi
- [ ] Step 10: Install Neovim + LazyVim
- [ ] Step 11: Set Ghostty as default terminal
- [ ] Step 12: Validate and verify
```

### Step 1: Pre-flight Checks

Verify prerequisites before starting:

```bash
# Check macOS and architecture
uname -m  # expect: arm64
sw_vers --productVersion  # expect: 13.0+

# Check Homebrew
brew --version || echo "Homebrew not installed — install from https://brew.sh"
```

If Homebrew is missing, install it:
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Check what is already installed to skip redundant steps:
```bash
for cmd in ghostty fish yazi lazygit nvim fzf zoxide atuin fd rg bat delta; do
  printf "%-10s: " "$cmd"
  which $cmd 2>/dev/null || echo "not installed"
done
```

Use this table to resolve any missing items:

| Check | Fix |
|-------|-----|
| Homebrew not installed | Run the install script above |
| `ghostty` not found | Step 2: `brew install --cask ghostty` |
| Any CLI tool not found | Step 3: `brew install <tool>` (all tools installed together) |
| Architecture not arm64 | This skill targets Apple Silicon; Intel Macs may have compatibility issues with some tools |

### Step 2: Install Ghostty

Check if Ghostty is already installed:
```bash
ls /Applications/Ghostty.app 2>/dev/null && echo "Ghostty installed" || echo "Not installed"
```

If not installed:
```bash
brew install --cask ghostty
```

### Step 3: Install CLI Tools

Install all tools in one command (already-installed tools are skipped automatically):

```bash
brew install fish yazi lazygit neovim fzf zoxide atuin fd ripgrep bat git-delta
```

### Step 4: Install Fonts

Ask the user which font setup they prefer before installing:

**Option A: CJK-optimized (recommended for Chinese/Japanese/Korean users)**
```bash
brew install --cask font-maple-mono-nf-cn font-sarasa-gothic font-jetbrains-mono-nerd-font
```

**Option B: Latin-only (English-primary users)**
```bash
brew install --cask font-jetbrains-mono-nerd-font
```

### Step 5: Configure Ghostty

Read the complete config template from [references/ghostty-config.md](references/ghostty-config.md).

Before writing, ask the user about preferences:
- **Theme**: Run `ghostty +list-themes` to show options. Popular: Monokai Vivid, Rose Pine, TokyoNight Storm, Catppuccin Mocha
- **Transparency**: Whether to enable background opacity (some users prefer fully opaque)
- **Font size**: Default 15, adjust for their display

Check if config already exists before writing:
```bash
mkdir -p ~/.config/ghostty
ls ~/.config/ghostty/config 2>/dev/null && echo "Config exists" || echo "No config"
```

If config exists: show current content, ask the user:
- **(A) Back up and replace**: `cp ~/.config/ghostty/config ~/.config/ghostty/config.backup.$(date +%s)` then write new config
- **(B) Skip**: keep existing config
- **(C) Show diff and merge**: show differences, let user decide per-section

After writing, ALWAYS validate:
```bash
ghostty +validate-config
```

If validation shows theme errors, the theme name likely needs exact casing. Check with `ghostty +list-themes | grep -i <name>`.

### Step 6: Configure Fish Shell

Read the complete config template from [references/fish-config.md](references/fish-config.md).

Ask the user if they want to register Fish as a login shell. Explain this means:
- Fish will be available in `chsh` as a login shell option
- It requires `sudo` to modify `/etc/shells`
- Their current shell remains the default unless they explicitly run `chsh -s $(which fish)` later

If the user agrees, register Fish:
```bash
grep -q "$(which fish)" /etc/shells || echo "$(which fish)" | sudo tee -a /etc/shells
```

**Do NOT run `chsh` automatically.** Only mention it as an optional next step if the user asks to make Fish their default shell.

Check if config already exists before writing:
```bash
mkdir -p ~/.config/fish/{completions,conf.d,functions}
ls ~/.config/fish/config.fish 2>/dev/null && echo "Config exists" || echo "No config"
```

If config exists: show current content, ask the user:
- **(A) Back up and replace**: `cp ~/.config/fish/config.fish ~/.config/fish/config.fish.backup.$(date +%s)` then write new config
- **(B) Skip**: keep existing config
- **(C) Show diff and merge**: show differences, merge section by section. **Idempotency check**: before adding init lines (`fzf --fish | source`, `zoxide init fish | source`, `atuin init fish | source`) or aliases, grep for them in the existing file to avoid duplicates.

After writing the config, validate Fish can parse it:
```bash
fish -n ~/.config/fish/config.fish && echo "Fish config syntax OK" || echo "Fish config has syntax errors"
```

If syntax errors are found, show the error output and fix the config before proceeding.

Import existing shell history into atuin:
```bash
fish -c "atuin import auto"
```

### Step 7: Install Fish Plugins

Check if Fisher (plugin manager) is installed:
```bash
fish -c "type fisher" 2>/dev/null || fish -c "curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher"
```

Install Tide prompt:
```bash
fish -c "fisher install IlanCosman/tide@v6"
```

### Step 8: Configure lazygit

Read the complete config template from [references/lazygit-config.md](references/lazygit-config.md).

The reference includes color themes for Monokai, TokyoNight, and Rose Pine. Match the lazygit theme to whichever Ghostty theme the user chose in Step 5.

Check if config already exists before writing:
```bash
mkdir -p ~/.config/lazygit
ls ~/.config/lazygit/config.yml 2>/dev/null && echo "Config exists" || echo "No config"
```

If config exists: show current content, ask the user:
- **(A) Back up and replace**: `cp ~/.config/lazygit/config.yml ~/.config/lazygit/config.yml.backup.$(date +%s)` then write new config
- **(B) Skip**: keep existing config
- **(C) Show diff and merge**: show differences, let user decide per-section

After writing, validate the YAML is parseable by lazygit:
```bash
lazygit -c ~/.config/lazygit/config.yml --version && echo "lazygit config OK" || echo "lazygit config may have issues"
```

If lazygit is not yet available, validate YAML syntax with:
```bash
python3 -c "import yaml; yaml.safe_load(open('$HOME/.config/lazygit/config.yml'))" && echo "YAML syntax OK" || echo "YAML syntax error"
```

### Step 9: Configure yazi

Read the complete config template from [references/yazi-config.md](references/yazi-config.md).

Check if config already exists before writing:
```bash
mkdir -p ~/.config/yazi
ls ~/.config/yazi/yazi.toml 2>/dev/null && echo "Config exists" || echo "No config"
```

If config exists: show current content, ask the user:
- **(A) Back up and replace**: `cp ~/.config/yazi/yazi.toml ~/.config/yazi/yazi.toml.backup.$(date +%s)` then write new config
- **(B) Skip**: keep existing config
- **(C) Show diff and merge**: show differences, let user decide per-section

After writing, validate the TOML is parseable:
```bash
python3 -c "import tomllib; tomllib.load(open('$HOME/.config/yazi/yazi.toml', 'rb'))" && echo "yazi config OK" || echo "TOML syntax error"
```

### Step 10: Install Neovim + LazyVim

Check if nvim config already exists:
```bash
ls ~/.config/nvim/init.lua 2>/dev/null && echo "Nvim config exists" || echo "No config"
```

If config exists, ask the user:
- **(A) Back up and replace**: `cp -r ~/.config/nvim ~/.config/nvim.backup.$(date +%s)` then clone fresh
- **(B) Skip**: keep existing Neovim config

If no existing config (or user chose A), clone to a temp directory first so a failed clone does not destroy the existing config:
```bash
NVIM_TMP=$(mktemp -d)
git clone https://github.com/LazyVim/starter "$NVIM_TMP/nvim" && rm -rf "$NVIM_TMP/nvim/.git"
```

Only replace the config after a successful clone:
```bash
rm -rf ~/.config/nvim
mv "$NVIM_TMP/nvim" ~/.config/nvim
rm -rf "$NVIM_TMP"
```

If the clone fails, inform the user that their existing config (or backup) is untouched and suggest retrying when network is available.

Tell the user: first time opening `nvim`, LazyVim auto-installs all plugins — wait about 30 seconds.

### Step 11: Set Ghostty as Default Terminal (Optional)

Ask the user if they want Ghostty to replace their current default terminal in Finder's "Open in Terminal".

If yes, read the Swift helper from [references/set-default-terminal.md](references/set-default-terminal.md) and run it.

### Step 12: Validate and Verify

Run final verification:
```bash
echo "=== Tool Versions ==="
for cmd in fish yazi lazygit nvim fzf zoxide atuin fd rg bat delta; do
  printf "%-10s: " "$cmd"
  $cmd --version 2>&1 | head -1
done

echo ""
echo "=== Ghostty Config ==="
ghostty +validate-config 2>&1 || echo "Config OK (no output = no errors)"

echo ""
echo "=== Fish Shell ==="
fish -c "echo Fish is working"
```

Present the user with a summary of what was installed and configured, plus the quick reference below.

## Quick Reference

| Alias | Command |
|-------|---------|
| `y` | yazi (file manager) |
| `yy` | yazi with cd-on-exit |
| `lg` | lazygit |
| `v` | nvim |
| `cc` | claude |
| `z <keyword>` | zoxide smart cd |

| Ghostty Shortcut | Action |
|------------------|--------|
| `Cmd+D` | Vertical split |
| `Cmd+Shift+D` | Horizontal split |
| `Cmd+Alt+Arrow` | Navigate splits |
| `` Ctrl+` `` | Quick Terminal (global) |

| Fish Key | Action |
|----------|--------|
| `Tab` | Accept autosuggestion |
| `Alt+Tab` | Accept one word |
| `→` | Completion menu |
| `Ctrl+R` | History search (atuin) |

## Recovery / Rollback

If new config breaks something, open **Terminal.app** (macOS built-in, always available) and run the appropriate fix:

| Broken | Fix |
|--------|-----|
| Ghostty won't launch or renders wrong | `mv ~/.config/ghostty/config ~/.config/ghostty/config.broken` — Ghostty uses defaults on next launch |
| Fish shell broken on startup | `mv ~/.config/fish/config.fish ~/.config/fish/config.fish.broken` — Fish loads without custom config |
| Want to revert Fish as login shell | `chsh -s /bin/zsh` |
| Want to remove Fish from /etc/shells | `sudo sed -i '' '\|/fish$|d' /etc/shells` |
| lazygit or yazi broken | Delete the config file (`~/.config/lazygit/config.yml` or `~/.config/yazi/yazi.toml`) — tool reverts to defaults |
| Neovim/LazyVim broken | `rm -rf ~/.config/nvim` — if you have a backup: `cp -r ~/.config/nvim.backup.<timestamp> ~/.config/nvim` |
| Any config with `.backup.<timestamp>` | `cp <file>.backup.<timestamp> <file>` to restore the backed-up version |

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

**List available themes**: `ghostty +list-themes`
