---
tags:
    - linux
    - unix
    - utils
    - transmission
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Transmission

[Transmission](https://transmissionbt.com/) is a light-weight and cross-platform BitTorrent client.

## Installation

<Tabs>
  <TabItem value="arch" label="archlinux" default>
        ```bash
        $ sudo pacman -S transmission-cli
        ```
  </TabItem>
</Tabs>

## transmission-remote

**transmission-remote** is a remote control utility for transimission-daemon.
By default connects to the transmission session at `localhost:9091`.

### Command examples

```bash title="Print command-line option descriptions"
$ transmission-remote -h
$ transmission-remote --help
```

```bash title="Add torrents to transmission"
$ transmission-remote -a filenames-or-URLs
$ transmission-remote --add filenames-or-URLs
```

```bash title="List all torrents"
$ transmission-remote -l
$ transmission-remote --list
```

```bash title="List all active torrents"
$ transmission-remote -tactive -l
```

```bash title="List all torrents with label 'abc'"
$ transmission-remote -F l:abc -l
```

```bash title="List all torrents with name containig 'def'"
$ transmission-remote -F n:def -l
```

```bash title="Start all torrents"
transmission-remote -tall --start
```

```bash title="Get a list of files for torrent with id = 1"
transmission-remote -t1 -f
```
