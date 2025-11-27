# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a modular Neovim configuration optimized for Kotlin development, using lazy.nvim as the plugin manager.

## Architecture

**Load order:** `init.lua` loads `config.options` first (before lazy.nvim bootstrap), then lazy.nvim imports all files from `lua/plugins/`, and finally `config.keymaps` loads after plugins.

**Plugin pattern:** Each file in `lua/plugins/` returns a table of lazy.nvim plugin specs. Lazy.nvim auto-discovers and merges all specs via `{ import = "plugins" }`.

**LSP setup:** Mason auto-installs `kotlin_language_server`. The `on_attach` function in `lua/plugins/lsp.lua` defines all LSP keybindings. To add a new language server, add it to `ensure_installed` and create a new `lspconfig.<server>.setup()` call with `capabilities` and `on_attach`.

**Formatting/Linting:** conform.nvim handles formatting, nvim-lint handles linting. Both configured in `lua/plugins/formatting.lua` with ktlint for Kotlin.

## Adding a New Plugin

Create a new file in `lua/plugins/` returning a lazy.nvim spec:
```lua
return {
  {
    "author/plugin-name",
    event = "VeryLazy",  -- or other lazy-loading trigger
    opts = {},
  },
}
```

## Adding a New Language Server

1. Add server name to `ensure_installed` in `lua/plugins/lsp.lua`
2. Add `lspconfig.<server>.setup({ capabilities = capabilities, on_attach = on_attach })` in the config function
3. Optionally add formatter/linter to `lua/plugins/formatting.lua`

## Key Configuration Files

- `lua/config/options.lua` - Leader key must be set here before lazy.nvim loads
- `lua/plugins/lsp.lua` - Central LSP keybindings in `on_attach` function
- `lua/plugins/formatting.lua` - Format-on-save and linter configuration
