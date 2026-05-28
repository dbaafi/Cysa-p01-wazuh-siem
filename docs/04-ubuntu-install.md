# Phase 1 — Installing the Ubuntu Server

## What this phase did
Set up the base operating system (Ubuntu Server 22.04 LTS) on a virtual
machine. This is the foundation that the Wazuh SIEM software will run on
in the next phase.

## Final result
A working Ubuntu server, reachable from my Mac, ready for Wazuh.

| Item        | Value                                      |
|-------------|--------------------------------------------|
| OS          | Ubuntu Server 22.04.5 LTS (ARM64)          |
| Hostname    | wazuh-server                               |
| IP address  | 192.168.64.2                               |
| Disk        | 56 GB (root)                               |
| Login user  | dbaafi (has admin/sudo rights)             |
| Remote access | SSH enabled: `ssh dbaafi@192.168.64.2`   |

## Problems I hit and how I solved them

**1. The disk was only half-used.**
By default, Ubuntu's installer only assigned ~28 GB of my 60 GB disk to
the system, leaving the rest empty. Since Wazuh stores a lot of log data,
I manually expanded the main volume to use the full disk (~56 GB).

**2. The VM kept rebooting into the installer.**
After the install finished and the machine restarted, it loaded the
Ubuntu *installer* again instead of the system I just installed — an
endless loop. The cause: the installation ISO ("virtual DVD") was still
loaded in the drive. I fixed it by ejecting the ISO in UTM's settings,
after which the VM booted correctly from its own disk.

**3. Stayed on version 22.04 on purpose.**
The system offered an upgrade to Ubuntu 24.04, but I declined it. Wazuh's
installer is tested against 22.04, so changing versions could cause
problems. Sticking with the supported version is the safer choice.

## Maintenance done
- Updated all system packages (`sudo apt update && sudo apt upgrade`)
- Confirmed `curl` is installed (needed to download the Wazuh installer)

## A note on security
Login credentials are stored privately and are NOT included in this
public repository.

## Next step
Install Wazuh (the SIEM software) — manager, indexer, and dashboard.
