# ghostty-vibe-coding-stack

[English](README.md)

一个 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 技能插件，用于配置完整的终端 AI 编程环境。用轻量级、可组合的 TUI 工具替代臃肿的 IDE——适用于 macOS Apple Silicon，包含针对中文/日文/韩文用户的 CJK 字体优化。

| 工具 | 用途 | 别名 |
|------|------|------|
| **Ghostty** | GPU 加速终端 | - |
| **Fish** | Shell（自动建议最强） | - |
| **Tide** | Fish 提示符主题 | - |
| **yazi** | TUI 文件管理器 | `y`, `yy` |
| **lazygit** | TUI Git 客户端 | `lg` |
| **Neovim** | 编辑器 (LazyVim) | `v` |
| **fzf** | 模糊搜索 | `Ctrl+R` |
| **zoxide** | 智能 cd | `z` |
| **atuin** | 增强历史命令 | `Ctrl+R` |
| **fd / rg / bat / delta** | CLI 增强工具 | - |

## 安装

### 通过 `npx skills`（推荐）

```bash
npx skills add psylch/ghostty-vibe-coding-stack
```

### 通过 Plugin Marketplace

在 Claude Code 中输入：

```
/plugin marketplace add psylch/ghostty-vibe-coding-stack
/plugin install configuring-ghostty-vibe-stack@psylch-ghostty-vibe-coding-stack
```

### 手动安装

```bash
git clone https://github.com/psylch/ghostty-vibe-coding-stack.git ~/.claude/skills/ghostty-vibe-coding-stack
```

安装后重启 Claude Code。

## 前置条件

- **macOS** Apple Silicon (M1+)
- **Homebrew**
- **Ghostty** 终端（[ghostty.org](https://ghostty.org)）
- **Claude Code**

## 使用方式

在 Claude Code 中输入：

```
配置 Ghostty
终端配置
开发环境搭建
configure my terminal
setup ghostty vibe coding stack
```

## 配置效果

### Ghostty
- 中文字体 fallback 链：Maple Mono NF CN → Sarasa Term SC → JetBrains Mono NF → 苹方
- 毛玻璃效果（透明度 + 模糊 + display-p3 色域）
- 原生分屏（`Cmd+D` 垂直 / `Cmd+Shift+D` 水平）
- Quick Terminal（全局 `` Ctrl+` `` 下拉终端）

### Fish Shell
- Tide 提示符主题
- Tab/→ 键互换（Tab 接受建议，→ 打开补全菜单）
- 集成 fzf、zoxide、atuin
- 快捷别名：`y`=yazi, `lg`=lazygit, `v`=nvim, `cc`=claude

### lazygit
- Monokai / TokyoNight / Rose Pine 配色
- delta 差异查看器
- Nerd Font 图标

## 典型布局

```
┌──────────────┬──────────────────────┐
│  yazi (y)    │  Claude Code (cc)    │
│  文件浏览     │  或 Neovim (v)       │
│  + 预览      │                      │
│              ├──────────────────────┤
│              │  lazygit (lg)        │
│              │  或 dev server       │
└──────────────┴──────────────────────┘
```

## 已知问题

- Ghostty 不支持 `Cmd+V` 粘贴图片给 Claude Code，用 `Ctrl+V` 代替
- Ghostty 主题名需要精确大小写和空格（如 `Rose Pine` 而非 `rose-pine`）
- Fish 绑键语法和 Zsh 不同——用 `bind right complete`，不用 `bind -k right`

## 许可证

MIT
