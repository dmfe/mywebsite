---
sidebar_position: 2
tags:
    - linux
    - unix
    - utils
    - systemd
---

# systemd

_systemd_ is a suit of basic building blocks for a linux system.
It provides a system and service manager that runs as PID 1 and starts the rest of the system.

## Basic systemctl usage

The main command used to introspect and control _systemd_ is `systemctl`.
Some of its uses are examinig the system state and managing the system and services.

### Using units

Units commonly include, but are not limited to, services (.service), mount points (.mount),
devices (.device) and sockets (.socket). When using `systemctl`, you generally have to
specify the complete name of the unit file, including suffix, for example `sshd.socket`.
There are a few short forms when specifying the unit int the following `systemctl` commands:
- If you do not specify the suffix, systemctl will assume _.service_
- Mount points will automatically be translated into the appropriate _.mount_ unit.
  For example `/home` is equivalent to `home.mount`
- Similar to mount points, devices are automatically translated into the appropriate _.device_ unit.
  Therefore specifying `/dev/sda2` is equivalent to `dev-sda2.device`

|                                   Action                                       |                  Command              |                    Note                |
|--------------------------------------------------------------------------------|---------------------------------------|----------------------------------------|
| **Show system status**                                                         | `systemctl status`                    |                                        |
| **List running** units                                                         | `systemctl` or `systemctl list-units` |                                        |
| **List failing** units                                                         | `systemctl --failed`                  |                                        |
| **List installed** unit files                                                  | `systemctl list-unit-files`           |                                        |
| **Show process status** for a PID                                              | `systemctl status pid`                | cgroup slice, memory and parent        |
| **Show a manual page** associated with a unit                                  | `systemctl help unit`                 | as supported by the unit               |
| **Status** of a unit                                                           | `systemctl status unit`               | including whether it is running or not |
| **Check** whether a unit is enabled                                            | `systemctl is-enabled unit`           |                                        |
| **Start** a unit immediately                                                   | `systemctl start unit`                |                                        |
| **Stop** a unit immediately                                                    | `systemctl stop unit`                 |                                        |
| **Restart** a unit                                                             | `systemctl restart unit`              |                                        |
| **Reload** a unit and its configuration                                        | `systemctl reload unit`               |                                        |
| **Enable** a unit to start auatomatically at boot                              | `systemctl enable unit`               |                                        |
| **Enable** a unit to start auatomatically at boot and **start** it immediately | `systemctl enable --now unit`         |                                        |
| **Disable** a unit to no longer to start at boot                               | `systemctl disable unit`              |                                        |
| **Reenable** a unit                                                            | `systemctl reenable unit`             | i.e. disable and enable anew           |


