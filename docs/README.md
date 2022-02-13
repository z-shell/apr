<h2 align="center">
  <a href="https://github.com/z-shell/zi">
    <img src="https://github.com/z-shell/zi/raw/main/docs/images/logo.svg" alt="Logo" width="80" height="80">
  </a>
❮ ZI ❯ Package - Apr
</h2>

<h3 align="center">
  
| **Package source:** |        Source Tarball        | Binary |        Git         | Node | Gem |
| :-----------------: | :--------------------------: | :----: | :----------------: | :--: | :-: |
|     **Status:**     | :heavy_check_mark: (default) |  :x:   | :heavy_check_mark: | :x:  | :x: |

</h3>

- [Available `pack''` invocations](#available-pack-invocations)
- [Default Profile](#default-profile)

> This repository compatible with [ZI](https://github.com/z-shell-zi)

The [apache/apr](https://github.com/apache/apr) zsh package that can use the NPM package registry to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
  - there can be multiple lists of ices,
  - the ice lists are stored in _profiles_; there's at least one profile, _default_,
  - the ices can be selectively overridden.

### Available `pack''` invocations

```zsh
# Download, build and install the latest Apache Portable Runtime source tarball
zi pack for apr
```

### Default Profile

Provides the Apache Portable Runtime library by compiling and installing it to the `$ZPFX` directory (`~/.zi/polaris` by default). It uses the
[z-shell/z-a-readurl](https://github.com/z-shell/z-a-readurl) annex to download the latest Apache Portable Runtime tarball.

The ZI command executed will be equivalent to:

```zsh
zi as"null|monitor" dlink"https://.*/apr-%VERSION%.tar.bz2" \
    atclone'ziextract --move --auto; print -P \\n%F{75}Building Apache Portable Runtime...\\n%f; ./configure \
        --prefix="$ZPFX" >/dev/null && make >/dev/null && print -P \
        \\n%F{75}Installing Apache Portable Runtime to $ZPFX...\\n%f && make install >/dev/null && print -P \
        \\n%F{34}Installation of Apache Portable Runtime succeeded.%f || \
        print -P \\n%F{160}Installation of Apache Portable Runtime failed.%f' \
    atpull'%atclone' for \
        https://apr.apache.org/download.cgi
```