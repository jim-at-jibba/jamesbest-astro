---
slug: "/fix-coc-tsserver-issues-due-to-deno"
title: "Fixing coc-tsserver errors due to Deno"
desciption: "This is a quick post detailing how to fix issues with coc-tsserver"
pubDate: "2020-05-28"
hero: "/images/posts/coc-tsserver/coc-tsserver-header.jpg"
tags: ["typescript", "vim", "productivity"]
layout: "../../layouts/BlogPostLayout.astro"
---

This is a quick post detailing how to fix issues with [`coc-tsserver`](https://github.com/neoclide/coc-tsserver).

I am a long term Neovim user and feel that the only Intellisense engine to use is [CocVim](https://github.com/neoclide/coc.nvim). It is simply amazing. It breathes so much power into you Vim setup.

I write Typescript daily and so use the [`coc-tsserver`](https://github.com/neoclide/coc-tsserver) plugin. It gives all the power of VSCodes typescript engine in NeoVim. But recently it broke. It was reporting errors when there was nothing wrong. I made sure all my dependencies we up to date and still nothing. All I was seeing was this:

The error message is: `The error message is: [tsserver 2307] [E] Cannot find module <import-path>`

Something was wrong.

Thankfully someone was having the same issue and had created an issue in the CocVim git repo. It turns out that there is a bug in the `coc-deno` plugin that has some problems with non-deno projects.

Thankfully the fix is simple. Disable the deno plugin for non deno projects.

With in Vim: `:CocList extensions` and find the Deno plugin. Press tab and select `d` to disable it. Restart Vim and all your issues should have disappeared.

# Thanks for reading 🙏

If there is anything I have missed, or if there is a better way to do something then please let me know
