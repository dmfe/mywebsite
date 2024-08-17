---
tags:
    - linux
    - unix
    - utils
    - apt
---

# apt

apt is a command-line tool for working with debian package manager. It stands
for Advanced Packaging Tool(APT).

## Working with APT examples

```bash title="Install new package"
$ apt install nvim
```

```bash title="Remove package"
$ apt remove nvim
```
Adding the `--purge` option to `apt remove` will also removes the package configuration
files.


```bash title="Update the local package index"
$ apt update
```

```bash title="Upgrade all packages in system"
$ apt update
$ apt upgrade
```

```bash title="Check apt cache size"
$ du -sh /var/cache/apt/archives/partial
```

```bash title="Clean apt cache except blocking file"
$ apt-get clean
```

```bash title="Clean apt cache, but it will remove only those packages, which can't be loaded from repositories."
$ apt-get autoclean
```

