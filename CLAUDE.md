# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a modular Neovim configuration for multi-language development (Kotlin, Java, Python, JavaScript, TypeScript), using lazy.nvim as the plugin manager.

## Architecture

**Load order:** `init.lua` loads `config.options` first (before lazy.nvim bootstrap), then lazy.nvim imports all files from `lua/plugins/`, and finally `config.keymaps` loads after plugins.

**Plugin pattern:** Each file in `lua/plugins/` returns a table of lazy.nvim plugin specs. Lazy.nvim auto-discovers and merges all specs via `{ import = "plugins" }`.

**LSP setup:** Mason auto-installs language servers (kotlin_language_server, jdtls, pyright, ts_ls). The `on_attach` function in `lua/plugins/lsp.lua` defines all LSP keybindings. To add a new language server, add it to `ensure_installed` and create a handler in the `handlers` table.

**Formatting/Linting:** conform.nvim handles formatting, nvim-lint handles linting. Both configured in `lua/plugins/formatting.lua` with language-specific tools (ktlint, google-java-format, black, prettier, ruff, eslint_d).

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
