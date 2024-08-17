---
sidebar_position: 3
tags:
    - linux
    - unix
    - utils
    - rsync
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# rsync

[rsync](https://rsync.samba.org/) is an open source utility that provides fast
incremental file transfer.

## Installation

<Tabs>
  <TabItem value="arch" label="archlinux" default>
        ```bash
        $ sudo pacman -S rsync
        ```
  </TabItem>
</Tabs>

## Usage

### As cp/mv alternative
`rsync` can be used as an advanced alternative for the `cp` or `mv` command,
especially for copying larger files:

```bash
$ rsync -P source destination
```

the `-P` option is the same as `--partial` `--progress`, which keeps partially 
transferred files and shows a progress bar. You may want to use the
`-r`/`--recursive` option to recurse into directories. 

### Copy between remote hosts

```bash title="Copy from local to remote host"
$ rsync source host:destination
```

```bash title="Copy from remote host to local"
$ rsync host:source destination
```

Network file transfers use the [SSH](https://wiki.archlinux.org/title/Secure_Shell)
protocol by default and `host` can be a real hostname hostname or a predefined
profile/alias from `.ssh/config`.

### Examples

```bash
$ rsync -uvrP --delete-after ~/website/ root@remote-host:/var/www/website/
```

`-u`/`--update` - skip files that are newer on the receiver  
`-v`/`--verbose` - increase verbosity  
`-r`/`--recursive` - recurse into directories  
`-P`/`--partial -- progress`- keeps partially transferred files and shows a progress bar  
`--delete-after` - receiver deletes after transfer, not during

