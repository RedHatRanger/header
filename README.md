# `header` – File Header Management Script - by RedHatRanger

`header` is a Bash utility that automatically adds or updates a standardized metadata header at the top of files (YAML, Bash, Python, configs, etc.).
It’s designed to help teams maintain consistent file documentation and versioning, while preserving shebangs (`#!/usr/bin/env bash`) and file permissions.

---

## ✨ Features

* Adds a new header to files without one, or updates existing headers
* Preserves shebang (`#!`) line if present
* Preserves original file permissions
* Header fields managed automatically:

  * **File** – filename
  * **Author** – preserved if exists; otherwise set to provided or current user
  * **Created On** – preserved once set; otherwise added at creation
  * **Last Modified** – always updated
  * **Modified By** – always updated
  * **Description** – preserved unless explicitly updated
  * **Version** – starts at `v1.0`, increments by `0.1` on each modification

---

## 📦 Installation

Save the script and make it executable:

```bash
sudo cp header /usr/local/bin/header
sudo chmod 755 /usr/local/bin/header
```

### Optional Vim Integration

To automatically insert or update headers when editing YAML files, add the following to your `~/.vimrc` (or globally in `/etc/vim/vimrc`):

```vim
autocmd BufRead,BufNewFile *.yml,*.yaml !header %
autocmd FileType yaml setlocal et ai ts=2 sw=2 sts=2
```

---

## 🚀 Usage

```bash
header [OPTIONS] FILE [FILE2 ...]
```

### Options

| Option                   | Description                                      |
| ------------------------ | ------------------------------------------------ |
| `-a, --author NAME`      | Set author (default: current user)               |
| `-m, --modified-by NAME` | Set Modified By field (default: current user)    |
| `-d, --desc TEXT`        | Set Description. Use `"-"` to preserve existing  |
| `-f, --force-author`     | Overwrite existing Author with the provided name |
| `-h, --help`             | Show usage                                       |

---

## 📝 Examples

### Add a new header

```bash
header --author "Alice" --desc "Production Configuration Template" sample.yaml
```

### Update an existing header

```bash
header -m "Bob" -d "Alice's code, modified by Bob" sample_with_header.yaml
```

### Replace the Author (force mode)

```bash
header --author "Bob" --force-author app.yaml
```

### Multiple files

```bash
header --author devops --desc "Infra configs" config1.yaml config2.yaml
```

---

## 🔍 Notes

* Preserves **Author** and **Created On** by default
* `--force-author` is required to overwrite Author
* `--desc "-"` preserves existing description
* Version auto-increments (`v1.0`, `v1.1`, `v1.2`, …)
