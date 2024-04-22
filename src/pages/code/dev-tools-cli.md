---
slug: "/dev-tools-cli"
title: "DTC :: CLI package"
descriptionion: "A collection of tools that you would normally reach to a browser for."
pubDate: "2022-11-23"
hero: "/images/code/dtc.jpg"
tags: ["cli", "go", "tool"]
layout: "../../layouts/BlogPostLayout.astro"
---

### [DTC Repo](https://github.com/jim-at-jibba/dtc)
Written in Go and leaning heavily on Cobra and the suite of tools from [Charm](https://charm.sh/):

- [Bubbletea](https://github.com/charmbracelet/bubbletea)
- [Lipgloss](https://github.com/charmbracelet/bubbletea)
- [Bubbles](https://github.com/charmbracelet/bubbles)

## Install

```sh
go install github.com/jim-at-jibba/dtc@latest
```

## UUID

**Generate UUID v4**

_The output of this command is automatically copied to the clipboard 📋_

<details>
  <summary>Example</summary>

```bash
dtc uuid generate
```

**Takes count flag to generate mulitple UUIDs at a time**

```bash
dtc uuid generate --count=100
```

![UUID Generate](/images/code/uuid.gif)
![UUID Generate](/images/code/uuid-count.gif)

</details>

## Base64

_The output of this command is automatically copied to the clipboard 📋_

### Encode

**Encode and Decode base64 strings in both standard and URL compatible formats**

<details>
  <summary>Example</summary>

**Standard**

```bash
dtc base64 encode
```

**URL Compatible**

```bash
dtc base64 encode -u
```

![BASE64 ENCODE](/images/code/base64-encode.gif)

</details>

### Decode

**Encode and Decode base64 strings in both standard and URL compatible formats**

<details>
  <summary>Example</summary>

**Standard**

```bash
dtc base64 decode
```

**URL Compatible**

```bash
dtc base64 decode -u
```

![BASE64 DECODE](/images/code/base64-decode.gif)

</details>

## File Share

_The output of this command is automatically copied to the clipboard 📋_

**Ephemeral file sharing, the link provided will expire, after a given time or when the file is downloaded. Makes use of [https://file.io](file.io)**

Note that there's a limit of 100mb on files

<details>
  <summary>Example</summary>

**Defaults to 14 days expiry**

```bash
dtc file-share
```

**Pass in an expiry time frame**

```bash
dtc file-share

# current dir, expires in 3 days
dtc file-share --expiry=3d

# expires in 4 weeks
dtc file-share --expiry=4w
```

![FILE SHARE](/images/code/file-share.gif)

</details>

### JWT Debugger

> Debug JWT - Validity is not tested!

The output of this command is automatically copied to the clipboard 📋

<details>
  <summary>Example</summary>

```bash
dtc jwt-debugger
```

![JWT DEBUGGER](/images/code/jwt-debugger.gif)

</details>
