# Neovim Configuration

A modern Neovim configuration optimized for Kotlin development.

## Features

- **LSP Support** - Full language server integration with kotlin-language-server
- **Autocompletion** - Intelligent code completion with nvim-cmp
- **Syntax Highlighting** - Treesitter-based highlighting
- **Fuzzy Finding** - Telescope for files, grep, and symbols
- **File Explorer** - Neo-tree sidebar
- **Git Integration** - Gitsigns for hunks, blame, and diffs
- **Linting & Formatting** - ktlint integration with format-on-save
- **Theme** - Tokyo Night colorscheme

## Requirements

- Neovim >= 0.9.0
- Git
- [ripgrep](https://github.com/BurntSushi/ripgrep) - for Telescope live grep
- [A Nerd Font](https://www.nerdfonts.com/) - for icons
- Java 11+ - for kotlin-language-server

### Install Dependencies (Ubuntu/Debian)

```bash
sudo apt install ripgrep
```

## Installation

1. Backup existing config (if any):
   ```bash
   mv ~/.config/nvim ~/.config/nvim.bak
   ```

2. Clone/copy this configuration to `~/.config/nvim`

3. Launch Neovim - plugins install automatically

4. Verify installation:
   ```vim
   :checkhealth
   :Mason
   ```

## Structure

```
~/.config/nvim/
├── init.lua                 # Entry point
├── lua/
│   ├── config/
│   │   ├── options.lua      # Vim options
│   │   └── keymaps.lua      # Global keybindings
│   └── plugins/
│       ├── colorscheme.lua  # Tokyo Night theme
│       ├── lsp.lua          # LSP + Mason setup
│       ├── completion.lua   # nvim-cmp + snippets
│       ├── treesitter.lua   # Syntax highlighting
│       ├── telescope.lua    # Fuzzy finder
│       ├── neo-tree.lua     # File explorer
│       ├── lualine.lua      # Statusline
│       ├── gitsigns.lua     # Git integration
│       └── formatting.lua   # Linting & formatting
```

## Keybindings

Leader key: `<Space>`

### LSP

| Key | Action |
|-----|--------|
| `gd` | Go to definition |
| `gD` | Go to declaration |
| `gr` | Go to references |
| `gi` | Go to implementation |
| `K` | Hover documentation |
| `<C-k>` | Signature help |
| `<leader>rn` | Rename symbol |
| `<leader>ca` | Code action |
| `<leader>D` | Type definition |
| `<leader>oi` | Organize imports |
| `[d` | Previous diagnostic |
| `]d` | Next diagnostic |
| `<leader>d` | Show diagnostic float |

### Navigation (Telescope)

| Key | Action |
|-----|--------|
| `<leader>ff` | Find files |
| `<leader>fg` | Live grep |
| `<leader>fb` | Buffers |
| `<leader>fh` | Help tags |
| `<leader>fr` | Recent files |
| `<leader>fc` | Find word under cursor |
| `<leader>fs` | Document symbols |
| `<leader>fS` | Workspace symbols |
| `<leader>fd` | Diagnostics |

### File Explorer

| Key | Action |
|-----|--------|
| `<leader>e` | Toggle Neo-tree |
| `<leader>o` | Focus Neo-tree |

### Git (Gitsigns)

| Key | Action |
|-----|--------|
| `]h` | Next hunk |
| `[h` | Previous hunk |
| `<leader>hs` | Stage hunk |
| `<leader>hr` | Reset hunk |
| `<leader>hS` | Stage buffer |
| `<leader>hu` | Undo stage hunk |
| `<leader>hp` | Preview hunk |
| `<leader>hb` | Blame line |
| `<leader>hd` | Diff this |
| `<leader>tb` | Toggle line blame |
| `<leader>td` | Toggle deleted |

### Formatting

| Key | Action |
|-----|--------|
| `<leader>f` | Format buffer |
| `<leader>l` | Trigger linting |

### Window Navigation

| Key | Action |
|-----|--------|
| `<C-h>` | Move to left window |
| `<C-j>` | Move to bottom window |
| `<C-k>` | Move to top window |
| `<C-l>` | Move to right window |
| `<S-h>` | Previous buffer |
| `<S-l>` | Next buffer |

### Completion (Insert Mode)

| Key | Action |
|-----|--------|
| `<Tab>` | Next item / expand snippet |
| `<S-Tab>` | Previous item |
| `<CR>` | Confirm selection |
| `<C-Space>` | Trigger completion |
| `<C-e>` | Abort completion |
| `<C-b>` | Scroll docs up |
| `<C-f>` | Scroll docs down |

## Plugins

| Plugin | Purpose |
|--------|---------|
| [lazy.nvim](https://github.com/folke/lazy.nvim) | Plugin manager |
| [tokyonight.nvim](https://github.com/folke/tokyonight.nvim) | Colorscheme |
| [mason.nvim](https://github.com/williamboman/mason.nvim) | LSP/tool installer |
| [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig) | LSP configurations |
| [nvim-cmp](https://github.com/hrsh7th/nvim-cmp) | Autocompletion |
| [LuaSnip](https://github.com/L3MON4D3/LuaSnip) | Snippet engine |
| [nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter) | Syntax highlighting |
| [telescope.nvim](https://github.com/nvim-telescope/telescope.nvim) | Fuzzy finder |
| [neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim) | File explorer |
| [lualine.nvim](https://github.com/nvim-lualine/lualine.nvim) | Statusline |
| [gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim) | Git integration |
| [conform.nvim](https://github.com/stevearc/conform.nvim) | Formatting |
| [nvim-lint](https://github.com/mfussenegger/nvim-lint) | Linting |

## Kotlin-Specific Features

- **kotlin-language-server** auto-installed via Mason
- **ktlint** for linting and formatting
- `<leader>oi` to organize imports
- Format on save enabled
- 4-space indentation (Kotlin standard)

## Commands

| Command | Action |
|---------|--------|
| `:Lazy` | Open plugin manager |
| `:Mason` | Open LSP/tool installer |
| `:LspInfo` | Show LSP status |
| `:ConformInfo` | Show formatter status |
| `:Telescope` | Open Telescope |
| `:Neotree` | Open file explorer |
