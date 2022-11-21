---
slug: "/essential-terminal-packages-2020"
title: "Essential terminal packages in 2020"
description: "These are the CLI packages I cant live without."
pubDate: "2020-06-26"
hero: "../images/posts/favourite-cli/exa.png"
tags: ["productivity"]
layout: "../../layouts/BlogPostLayout.astro"
---

This is the start of a new series about maximising your terminal experience. I will write about what I think are essential packages for the CLI, a simple but super effective Vim setup and setting some sane Tmux defaults.

In this first article, I am going to list some of what I think are essential CLI packages. These are ones I use every day and could not live without. I am leaving Vim and Tmux off this list as they will get there own articles.

I spend all my time in a terminal. This is where I do all my development, hacking and note-taking. Spending so much time there I want it to work for me, providing a buttery smooth experience.

Here is a list of my top CLI packages.

## 1. ZSH and oh-my-zsh:

This is my chosen shell. It has way too many features to list here but here are a choice few:

- automatic cd: Just type the name of the directory
- recursive path expansion: For example “/u/lo/b” expands to “/usr/local/bin”. This is not one I use much because I lead on the tools mentioned below.
- spelling correction and approximate completion: If you make a small mistake typing a directory name, ZSH will fix it for you
- plugin and theme support: ZSH includes many different plugin frameworks. This is where [`oh-my-zsh`](https://ohmyz.sh/) comings in. Its a community drive framework for managing your ZSH configuration.

![ZSH](../images/posts/favourite-cli/zsh.png)

## 2. FZF

[FZF](https://github.com/junegunn/fzf) is a command-line fuzzy finder. It is super fast, light and works so well with all my other tools.

![fzf](../images/posts/favourite-cli/fzf.png)

## 3. RipGrep (rg)

[RipGrep](https://github.com/BurntSushi/ripgrep) is a stupid fast replacement for grep. It does away with lots of the hard to remember flags that grep requires. By default, it respects your `.gitignore`, and skips hidden files.

## 4. Autojump

[Autojump](https://github.com/wting/autojump) is a super-fast way to navigate your filesystem. It learns the directories you visit most and remembers them for next time.

## 5. HTTPie

[HTTPie](https://httpie.org/) is a user-friendly command line HTTP client. It has JSON support, syntax highlighting and lots more.

## 6. Bat

[Bat](https://github.com/sharkdp/bat) is a drop-in replacement for `cat` but with superpowers. It's highly configurable and supports syntax highlighting.

![Bat](../images/posts/favourite-cli/bat.png)

## 7. exa

[exa](https://the.exa.website/) is a modern replacement for `ls`. It is highly configurable, provides better defaults.

![HTTPie](../images/posts/favourite-cli/exa.png)

## 8. twf

[twf](https://github.com/wvanlint/twf) is a tree view explorer inspired by fzf.

![HTTPie](../images/posts/favourite-cli/twf.png)

You can find my dotfiles [here](https://github.com/jim-at-jibba/my-dots). This is how I use them, how will you?

# Thanks for reading 🙏

If there is anything I have missed, or if there is a better way to do something then please let me know.

Check out our software focused podcast - [Salted Bytes](https://open.spotify.com/show/7IdlgpiDfYcOdCn57mPLvH?si=X1ArfHvqQXSOAfc1h7Y_Eg)
