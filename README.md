# nv

<div align="center">

[![Lua](https://img.shields.io/badge/Made%20with%20Lua-blueviolet.svg?style=for-the-badge&logo=lua)]()

</div>

<div align="center">

[![Neovim Minimum Version](https://img.shields.io/badge/Neovim-0.5+-blueviolet.svg?style=flat-square&logo=Neovim&logoColor=white)](https://github.com/neovim/neovim)
[![Last Commit](https://img.shields.io/github/last-commit/shift-d/nv.svg?style=flat-square&label=Last%20Commit&color=58eb34)](https://github.com/shift-d/nv/pulse)

</div>

nv is a lua neovim config which tries to be simple, cute and well-documented

## Installation

### Pre-requisites

#### For installation
- [neovim v0.5.0+](https://neovim.io) (required for lua support)
- git

#### Requirements for default config to work
- [Nerd patched font](https://www.nerdfonts.com/) - used by nvim-web-devicons
- [glow](https://github.com/charmbracelet/glow) - used by [glow.nvim](#ellisonleaoglownvim)
- [sumneko-lua](https://github.com/sumneko/lua-language-server) - used by [lua-dev](#folkelua-devnvim)
- [ripgrep](https://github.com/BurntSushi/ripgrep) - default [telescope](#nvim-telescopetelescopenvim) grep searcher


### Manual

1. Backup your previous neovim config if it exists
2. Clone repository into config folder
    - Windows
        - cmd
            - default: `git clone https://github.com/shift-d/nv --depth 1 %LOCALAPPDATA%\nvim\`
            - XDG_CONFIG_HOME is set: `git clone https://github.com/shift-d/nv --depth 1 %XDG_CONFIG_HOME%\nvim\`
        - powershell
            - default: `git clone https://github.com/shift-d/nv --depth 1 $env:LOCALAPPDATA\nvim\`
            - XDG_CONFIG_HOME is set: `git clone https://github.com/shift-d/nv --depth 1 $env:XDG_CONFIG_HOME\nvim\`
    - Unix:
        - default: `git clone https://github.com/shift-d/nv --depth 1 ~/.config/nvim/`
        - XDG_CONFIG_HOME is set: `git clone https://github.com/shift-d/nv -- depth 1 $XDG_CONFIG_HOME/nvim/`
3. Open neovim inside config directory
4. Type `:PackerInstall`
5. Reopen neovim - and... done!

### Script

#### Windows
1. Open powershell
2. Run `Invoke-WebRequest https://raw.githubusercontent.com/shift-d/nv/main/scripts/install.ps1 | select -ExpandProperty Content | Invoke-Expression`
3. Follow steps 3-5 from [manual installation](#manual)

#### Unix
1. Open shell
2. Run `curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/shift-d/nv/main/scripts/install.sh | bash`
3. Follow steps 3-5 from [manual installation](#manual)

### Post-installation
- Add [LspInstall](https://github.com/williamboman/nvim-lsp-installer) plugin
    - NOTE: I'd recommend this plugin because it is crossplatform, unlike other LspInstall plugins
    - NOTE: I did not include this plugin because I wanted users to decide whether they want to install lsp servers manually or not

## Configuration

Feel free to configurate everything!
Unlike [NvChad](https://github.com/NvChad/NvChad) and [kyoto.nvim](https://github.com/samrath2007/kyoto.nvim) nv provdes only glue for your config.
Make it yourself!

Please, review every config file. If you don't know what exactly this option does - run `:h $option` or if it's in plugin config - visit it's README.md.

## Directory overview

`init.lua` - file that imports every module
`lua/` - folder that should be used for containing `*.lua` files
`lua/config/` - folder for plugin configuration files
`lua/options.lua` - `vim.opt`, `vim.o` and `vim.g` options
`lua/mappings.lua` - keybindings handled by [nest.nvim](https://github.com/LionC/nest.nvim)
`lua/plugins.lua` - plugin specification file; more info in [Plugins](#Plugins) section
`lua/lsp.lua` - LSP settings
`lua/utils.lua` - global functions for lua
`viml/` - folder that should be used for containing  `*.vim` files
`viml/commands.vim` - definitions of user commands and autocommands

## Comparison to other configs

State|nv|NvChad|kyoto.nvim|Lunarvim|
-----|--|------|----------|--------|
Number of plugins | 17 | 33 | 30 | 26|
Why | simplicity and well-documented | fast and pretty | fast and customizable | sane defaults|
Installation | crossplatform | crossplatform | linux/macos only | [not yet](https://github.com/LunarVim/LunarVim/pull/1261)
Required | nerd font, glow, sumneko-lua, rg | rg, nodejs, nerd font | nerd font, ctags, python, nodejs, rg | rust, python, nodejs |

## Plugins

Plugins in nv are managed with [packer.nvim](https://github.com/wbthomason/packer.nvim)
List below contains every plugin provided by default with notes about it's configuration

### Colors

#### [Pocco81/Catppuccino.nvim](https://github.com/Pocco81/Catppuccino.nvim)
Pack of treesitter-compatible colorschemes with multiple other plugin integrations available
- loads after reading `init.lua` (`VimEnter` event)
- config is located in `lua/config/colorscheme.lua`

#### [nvim-treesitter/nvim-treesitter](https://github.com/nvim-treesitter/nvim-treesitter)
Built-in language parser's configurator
- loads when starting to edit a new buffer (`BufRead` event)
- config is located in `lua/config/treesitter.lua`

#### [hoob3rt/lualine.nvim](https://github.com/hoob3rt/lualine.nvim)
Lua-powered statusline
- requires
    - [kyazdani42/nvim-web-devicons](https://github.com/kyazdani42/nvim-web-devicons)
- config is located in `lua/config/statusline.lua`

### Text

#### [mhartington/formatter.nvim](https://github.com/mhartington/formatter.nvim)
Plugin for formatting current buffer
- loads on `:Format` command
- config is located in `lua/config/formatter.lua`

#### [ellisonleao/glow.nvim](https://github.com/ellisonleao/glow.nvim)
Markdown preview, uses [glow](https://github.com/charmbracelet/glow) under hood
- loads if current buffer has `markdown` filetype

### Tpope section

#### [tpope/vim-surround](https://github.com/tpope/vim-surround)
Amazing vimscript plugin that allows you edit surrounding symbols
- loads after reading `init.lua` (`VimEnter` event)

### Utils

#### [nvim-lua/plenary.nvim](https://github.com/nvim-lua/plenary.nvim)
Bunch of great lua functions;

#### [LionC/nest.nvim](https://github.com/LionC/nest.nvim)
Small lua wrapper around keymap api. Allows creating nested keymaps

#### [nvim-telescope/telescope.nvim](https://github.com/nvim-telescope/telescope.nvim)
Superpowered lua fuzzy finder
- loads on `:Telecope` command
- config is located in `lua/config/telescope.nvim`

#### [glepnir/dashboard-nvim](https://github.com/glepnir/dashboard-nvim)
Lua dashboard that you see after open neovim.

#### [kyazdani42/nvim-tree.lua](https://github.com/kyazdani42/nvim-tree.lua)
A file explorer tree written in lua
- loads on `:NvimTreeToggle` command
- requires
    - [kyazdani42/nvim-web-devicons](https://github.com/kyazdani42/nvim-web-devicons)
- config is located in `lua/config/nvimtree.lua`

#### [projekt0n/circles.nvim](https://github.com/projekt0n/circles.nvim)
Replaces `nvim-web-devicons` and lsp's icons with minimalistic colored circles
- config is located in `lua/config/circles.lua`

### Git

#### [lewis6991/gitsigns.nvim](https://github.com/lewis6991/gitsigns.nvim)
Super fast git decorations implemented purely in lua/teal
- loads if cwd contains `.git` directory
- requires
    - [nvim-lua/plenary.nvim](https://github.com/nvim-lua/plenary.nvim)
- config is located in `lua/config/gitsigns.lua`

### Completion

#### [hrsh7th/nvim-cmp](https://github.com/hrsh7th/nvim-cmp)
Completion engine based on "sources" concept
- loads when starting to edit a new buffer (`BufRead` event)
- requires
    - [hrsh7th/cmp-buffer](https://github.com/hrsh7th/cmp-buffer)
        - loads after `nvim-cmp` plugin
    - [hrsh7th/cmp-nvim-lua](https://github.com/hrsh7th/cmp-nvim-lua)
        - loads after `nvim-cmp` plugin
    - [hrsh7th/cmp-nvim-lsp](https://github.com/hrsh7th/cmp-nvim-lsp)
        - loads after `nvim-cmp` plugin
    - [saadparwaiz1/cmp_luasnip](https://github.com/saadparwaiz1/cmp_luasnip)
        - loads after `LuaSnip` plugin
- config is located in `lua/config/cmp.lua`

#### [L3MON4D3/LuaSnip](https://github.com/L3MON4D3/LuaSnip)
Neovim snippet engine built in lua
- loads after `nvim-cmp` plugin

### LSP

#### [neovim/nvim-lspconfig](https://github.com/neovim/nvim-lspconfig)
Native neovim lsp configurator
- loads after `cmp-nvim-lsp` plugin
- config is located in `lua/lsp.lua`

#### [simrat39/rust-tools.nvim](https://github.com/simrat39/rust-tools.nvim)
Rust lsp configurator that makes use of nvim-lspconfig. Here is only for an example of lsp usage.
- requires
    - [neovim/nvim-lspconfig](https://github.com/neovim/nvim-lspconfig)
    - [nvim-lua/plenary.nvim](https://github.com/nvim-lua/plenary.nvim)
    - [nvim-lua/popup.nvim](https://github.com/nvim-lua/popup.nvim)
    - [nvim-telescope/telescope.nvim](https://github.com/nvim-telescope)

#### [folke/lua-dev.nvim](https://github.com/folke/lua-dev.nvim)
Dev setup for init.lua and plugin development with full signature help, docs and completion for nvim lua API.
- loads if current buffer has `lua` type


# FAQ

## Why use vimscript and not write entire config in lua?

Sometimes you are not able to write code in lua, so you have to call vimscript from lua.
In my opinion, making stacks of `vim.cmd(...` is a bad idea, so I'd like to separate vimscript only categories from lua code.
In case of this config, defining commands and autocommands is not supported in neovim lua api _yet_, so that's why I moved their definition to .vim file.

NOTE: related PR's for adding commands and autocommands support for lua API:
[neovim/neovim#11613](https://github.com/neovim/neovim/pull/11613)
[neovim/neovim#14661](https://github.com/neovim/neovim/pull/14661)
