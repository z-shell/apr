| **Package source:** |  Source Tarball  | Binary | Git | Node | Gem |
| :-----------------: | :--------------: | :----: | :-: | :--: | :-: |
|     **Status:**     | + <br> (default) |   -    |  +  |  –   |  –  |

- [Introduction](#introduction)
- [Install](#install)
  - [Available `pack''` invocations](#available-pack-invocations)
  - [Default Profile](#default-profile)

# Introduction

> **[?]**
> This repository not compatible with previous versions (zplugin, zinit).
>
> Please upgrade to [ZI](https://github.com/z-shell-zi)

The [apache/apr](https://github.com/apache/apr) zsh package than can use the NPM package registry to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
  - there can be multiple lists of ices,
  - the ice lists are stored in _profiles_; there's at least one profile, _default_,
  - the ices can be selectively overridden.

# Install

## Available `pack''` invocations

[apache/apr](https://github.com/apache/apr) either from the release archive
or from Git repository:

```zsh
# Download, build and install the latest Apache Portable Runtime source tarball
zi pack for apr
```

## Default Profile

Provides the Apache Portable Runtime library by compiling and installing it to
the `$ZPFX` directory (`~/.zi/polaris` by default). It uses the
[z-shell/z-a-as-monitor](https://github.com/z-shell/z-a-as-monitor) annex to
download the latest Apache Portable Runtime tarball.

The ZI command executed will be equivalent to:

```zsh
zi as"null|monitor" dlink"https://.*/apr-%VERSION%.tar.bz2" \
    atclone'zpextract --move --auto; print -P \\n%F{75}Building Apache Portable Runtime...\\n%f; ./configure \
        --prefix="$ZPFX" >/dev/null && make >/dev/null && print -P \
        \\n%F{75}Installing Apache Portable Runtime to $ZPFX...\\n%f && make install >/dev/null && print -P \
        \\n%F{34}Installation of Apache Portable Runtime succeeded.%f || \
        print -P \\n%F{160}Installation of Apache Portable Runtime failed.%f' \
    atpull'%atclone' for \
        https://apr.apache.org/download.cgi
``
```
