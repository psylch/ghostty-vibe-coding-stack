# yazi Configuration

Config path: `~/.config/yazi/`

## yazi.toml

```toml
[manager]
show_hidden = true
sort_by = "natural"
sort_dir_first = true

[opener]
edit = [
  { run = 'nvim "$@"', block = true, for = "unix" },
]

[preview]
max_width = 1000
max_height = 1000
```

## Essential Keybinds

| Key | Action |
|-----|--------|
| `q` | Quit |
| `/` | Search files |
| `Space` | Select (multi-select) |
| `y` | Yank (copy) |
| `x` | Cut |
| `p` | Paste |
| `d` | Delete |
| `r` | Rename |
| `.` | Toggle hidden files |
| `~` | Jump to home directory |
| `Enter` | Open file/enter directory |

## Usage Tips

- Use `y` alias to open yazi, `q` to quit (returns to original directory)
- Use `yy` alias to open yazi and cd to browsed directory on quit
- yazi supports image preview in Ghostty (Kitty graphics protocol)
