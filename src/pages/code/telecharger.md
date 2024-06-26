---
slug: "/telecharger-youtube-dl-tui"
title: "Telecharger :: youtube-dl TUI"
descriptionion: "Telecharger is a Youtube-DL TUI. It provides the ability to build lists of videos you wish to download, rename the files, saving as audio only and a host of other functionality."
pubDate: "2023-02-01"
hero: "/images/code/telecharger-dashboard.jpg"
tags: ["cli", "go", "tool"]
layout: "../../layouts/BlogPostLayout.astro"
---

> Telecharger is a [Youtube-DL](https://github.com/ytdl-org/youtube-dl) TUI

![Form](/images/code/telecharger.gif)
### [Telecharger Repo](https://github.com/jim-at-jibba/dtc)

Telecharger is a [Youtube-DL](https://github.com/ytdl-org/youtube-dl) TUI. It provides the ability to build lists of videos you wish to download, rename the files, saving as audio only and a host of other functionality.

Not all the flags that youtube-dl allows are supported yet but you can provide them as a string on the form and telecharger will sort the rest out for you.

<details>
  <summary>Example</summary>

Adding the following extra commands

`--add-metadata --write-all-thumbnails --embed-thumbnail --write-info-json --embed-subs --all-subs`

![Extra commnds](/images/code/telecharger-extra-commands.gif)

</details>

The SQLite database is created in a **telecharger** directory in your home directory. In the future config will likely live here too.

## Requirements

- [Youtube-DL](https://github.com/ytdl-org/youtube-dl)
- [FFMPEG](https://ffmpeg.org/)

**Warning**

I have not tested this on windows and doubt it will work there. Sorry.

## Install

```sh
go install github.com/jim-at-jibba/telecharger@latest
```

## Usage

```sh
telecharger
```
