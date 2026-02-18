# lazygit Configuration

Config path: `~/.config/lazygit/config.yml`

## Complete Config (Monokai Theme)

```yaml
gui:
  theme:
    activeBorderColor:
      - "#a6e22e"  # Monokai green
      - bold
    inactiveBorderColor:
      - "#75715e"  # Monokai comment gray
    optionsTextColor:
      - "#66d9ef"  # Monokai cyan
    selectedLineBgColor:
      - "#49483e"  # Monokai selection
    cherryPickedCommitFgColor:
      - "#66d9ef"
    cherryPickedCommitBgColor:
      - "#49483e"
    markedBaseCommitFgColor:
      - "#a6e22e"
    markedBaseCommitBgColor:
      - "#49483e"
    unstagedChangesColor:
      - "#f92672"  # Monokai pink
    defaultFgColor:
      - "#f8f8f2"  # Monokai foreground
  nerdFontsVersion: "3"
  showBottomLine: false
  border: rounded
git:
  paging:
    colorArg: always
    pager: "delta --dark --paging=never"
os:
  editPreset: nvim
```

## Essential Keybinds

| Key | Action |
|-----|--------|
| `?` | Show all keybinds |
| `Space` | Stage/unstage file |
| `c` | Commit |
| `p` | Push |
| `P` | Pull |
| `e` | Open in editor (nvim) |
| `[` / `]` | Switch panels |
| `Enter` | Expand/view |

## Theme Variants

To match lazygit theme to Ghostty theme, adjust the hex colors:

**TokyoNight Storm:**
```yaml
activeBorderColor: ["#7aa2f7", bold]
inactiveBorderColor: ["#565f89"]
optionsTextColor: ["#7dcfff"]
selectedLineBgColor: ["#283457"]
unstagedChangesColor: ["#f7768e"]
defaultFgColor: ["#c0caf5"]
```

**Rose Pine:**
```yaml
activeBorderColor: ["#31748f", bold]
inactiveBorderColor: ["#6e6a86"]
optionsTextColor: ["#9ccfd8"]
selectedLineBgColor: ["#26233a"]
unstagedChangesColor: ["#eb6f92"]
defaultFgColor: ["#e0def4"]
```
