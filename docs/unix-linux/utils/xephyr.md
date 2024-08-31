---
tags:
    - linux
    - unix
    - utils
    - xephyr
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Xephyr

Xephyr is a nested X server that runs as an X application.

## Instalation

<Tabs>
  <TabItem value="arch" label="archlinux" default>
        ```bash
        $ sudo pacman -S xorg-server-xephyr
        ```
  </TabItem>
</Tabs>

## Usage

To run a nested X window, you will need to specify a new display:
```bash
$ Xephyr -br -ac -noreset -screen 800x600 :1
```
This will launch a new Xephyr window with a DISPLAY of ":1". In order to launch an application in that window, you would need to specify that display:
```bash
$ DISPLAY=:1 xterm
```

### Launching window managers

If you want to launch a specific WM, [awesomewm](https://awesomewm.org) for example, you would type:
```bash
$ DISPLAY=:1 awesome
```

### Grabbing and un-grabbing user input

Pressing `Ctrl+Shift` should lock/unlock your mouse pointer and your keystrokes inside Xephyr window exclusively if possible.

## Other examples for situations where Xephyr can be useful

- A testing environment for an X application, or feature, in which the tester would like to keep working in their usual X environment,
  yet defending the other applications from failures of the application under test. Example script for running tested app(for examples
  window manager) inside Xephyr:
  ```bash title="xephyr.sh"
  #!/bin/bash

  Xephyr -br -ac -reset -screen 1920x1080 :5 &
  sleep 1s
  export DISPLAY=:5
  $1 &
  ```
  To run [awesomewm](https://awesomewm.org) inside Xephyr you can run:
  ```bash
  $ ./xephyr.sh awesome
  ```

