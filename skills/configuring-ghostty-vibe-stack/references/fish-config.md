# Fish Shell Configuration

Config path: `~/.config/fish/config.fish`

## Complete Config

```fish
if status is-interactive
    # Homebrew
    eval (/opt/homebrew/bin/brew shellenv)

    # Editor
    set -gx EDITOR nvim
    set -gx VISUAL nvim

    # PATH
    fish_add_path $HOME/.local/bin
    fish_add_path $HOME/bin
    fish_add_path $HOME/.bun/bin
    fish_add_path $HOME/.pyenv/bin
    fish_add_path $HOME/go/bin

    # pyenv (optional)
    if command -q pyenv
        pyenv init - | source
        pyenv init --path | source
    end

    # Custom key bindings: swap Tab and →
    # Tab = accept autosuggestion, → = completion menu
    bind tab accept-autosuggestion
    bind alt-tab forward-word
    bind right complete
    bind \e\[C complete

    # fzf
    fzf --fish | source

    # zoxide (smart cd)
    zoxide init fish | source

    # atuin (enhanced shell history)
    atuin init fish | source

    # Aliases
    alias lg "lazygit"
    alias y "yazi"
    alias v "nvim"
    alias g "git"
    alias gs "git status"
    alias gd "git diff"
    alias gl "git log --oneline -20"
    alias cc "claude"

    # yazi: cd to directory on exit
    function yy
        set tmp (mktemp -t "yazi-cwd.XXXXXX")
        yazi $argv --cwd-file="$tmp"
        if set cwd (command cat -- $tmp); and [ -n "$cwd" ]; and [ "$cwd" != "$PWD" ]
            builtin cd -- $cwd
        end
        command rm -f -- $tmp
    end
end
```

## Key Bindings

Default key bindings are swapped for a more intuitive experience:

| Key | Action |
|-----|--------|
| `Tab` | Accept full autosuggestion (gray text) |
| `Alt+Tab` | Accept one word of suggestion |
| `→` | Open completion menu |
| `Ctrl+R` | History search (atuin) |

## Emacs Mode Shortcuts (built-in)

| Key | Action |
|-----|--------|
| `Ctrl+A` | Jump to line start |
| `Ctrl+E` | Jump to line end |
| `Ctrl+W` | Delete previous word |
| `Ctrl+U` | Delete entire line |
| `Ctrl+K` | Delete to end of line |
| `Alt+F` | Forward one word |
| `Alt+B` | Back one word |
| `Ctrl+L` | Clear screen |
| `Alt+E` | Edit command in $EDITOR |
| `Alt+S` | Prepend sudo |

## Fish Plugins

Installed via Fisher (`fish -c "fisher install <plugin>"`):

- **Tide v6** — prompt theme (like Powerlevel10k for Fish)

## Notes

- Fish bind syntax: use `bind right` not `bind -k right` (`-k` is zsh syntax)
- Override both symbolic and escape sequence: `bind right complete` AND `bind \e\[C complete`
- `..` works as `cd ..` natively in Fish
