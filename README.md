<div align="center">
  <h1 align="center">· CodeCompanion Copilot Enterprise adapter ·</h1>

  <p align="center">
    A CodeCompanion adapter for GitHub Copilot Business/Enterprise.
    <br/>
    <br/>
    <a href="https://github.com/olimorris/codecompanion.nvim/releases/tag/v17.18.0">
        <img src="https://img.shields.io/badge/CodeCompanion-v17.18.0-C678DD?style=for-the-badge">
    </a>
    <a href="https://neovim.io">
        <img src="https://img.shields.io/badge/Neovim-57A143?style=for-the-badge&logo=neovim&logoColor=white">
    </a>
    <a href="https://www.lua.org">
        <img src="https://img.shields.io/badge/Lua-2C2D72?style=for-the-badge&logo=lua&logoColor=white">
    </a>
    <a href="https://opensource.org/licenses/MIT">
        <img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge">
    </a>
  </p>
</div>

Adds a custom CodeCompanion adapter for GitHub Copilot Business/Enterprise plans.

## 📋 Requirements

- A GitHub Copilot Business/Enterprise plan for your organization,
- [codecompanion.nvim](https://codecompanion.olimorris.dev/), and
- one of the following plugins, setup for an enterprise account:
    - [copilot.vim](https://github.com/github/copilot.vim), look for the [`g:copilot_enterprise_uri`](https://github.com/github/copilot.vim/blob/v1.53.0/doc/copilot.txt#L76-L82) global option;
    - [copilot.lua](https://github.com/zbirenbaum/copilot.lua), look for the config option [`auth_provider_url`](https://github.com/zbirenbaum/copilot.lua/blob/master/doc/copilot.txt#L80-L84).

## 📦 Installation

### Install the plugin

Use your favourite package manager.

<details>
<summary>lazy.nvim</summary>

Install as a dependency of `olimorris/codecompanion.nvim`.

```lua
{
    "olimorris/codecompanion.nvim",
    dependencies = {
        "dyamon/codecompanion-copilot-enterprise.nvim"
        -- other plugins...
    }
}
```

</details>

### Add the adapter to CodeCompanion

If your organization is available at `https://acme.ghe.com`

```lua
require("codecompanion").setup({
  adapters = {
    http = {
      copilot_enterprise = function()
        local adapter = require 'codecompanion.adapters.copilot_enterprise'
        adapter.opts.provider_url = "acme.ghe.com" -- 'https://' can be removed but doesn't hurt.
        return adapter
      end,
    },
  },
  strategies = {
    chat = {
      -- Setup the custom adapter for each strategy. You can change default models as usual.
      -- See https://codecompanion.olimorris.dev/configuration/adapters.html#changing-the-default-adapter
      -- and https://codecompanion.olimorris.dev/configuration/adapters.html#changing-a-model
      adapter = {
        name = "copilot_enterprise",
        model = "claude-sonnet-4",
      },
    },
    inline = {
      adapter = "copilot_enterprise",
    },
    cmd = {
      adapter = "copilot_enterprise",
    },
  },
})
```

## 🔮 Future Roadmap

- [ ] **Copilot statistics**: it seems like the same API endpoint used for individual GitHub accounts to get statistics about Copilot usage is available for enterprise accounts as well, but returns a whooping 404;
      I can replicate this behaviour in VS Code as well. If the feature becomes available in the future, the plugin supports it already.

## 🙏 Acknowledgements

- [Oli Morris](https://github.com/olimorris) for creating [CodeCompanion.nvim](https://codecompanion.olimorris.dev).

## 📄 License

MIT
