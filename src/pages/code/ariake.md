---
slug: "/ariake-nvim"
title: "Ariake.nvim :: Neovim Theme"
descriptionion: "Ariake is a beautiful dark theme for Neovim"
pubDate: "2023-04-24"
hero: "/images/code/typescriptreact-ariake.png"
tags: ["lua", "neovim", "tool"]
layout: "../../layouts/BlogPostLayout.astro"
---

> Beautiful, dark colour schema for Neovim

<div align="center">
    <h1>Ariake</h1>
</div>


## Install

To install ariake.nvim you need a plugin manager.

- [Lazy.nvim](https://github.com/folke/lazy.nvim)

Example with Lazy.nvim

```lua
return {
    {
        'jim-at-jibba/ariake.nvim',
        config = function ()

         vim.cmd.colorscheme 'ariake'
        end
    }
}
```

## Extra

In the extras folder there are Ariake theme files for:

- [Kitty](https://sw.kovidgoyal.net/kitty/)
- [Spacebar](https://github.com/cmacrae/spacebar)

## Examples


<img alt="Example" src="/images/code/go-ariake.png" />
<img alt="Example" src="/images/code/python-ariake.png" />
<img alt="Example" src="/images/code/lua-ariake.png" />

