# ansible-role-btrfs

![GitHub](https://img.shields.io/github/license/cosandr/ansible-role-btrfs) ![GitHub last commit](https://img.shields.io/github/last-commit/cosandr/ansible-role-btrfs) ![GitHub issues](https://img.shields.io/github/issues-raw/cosandr/ansible-role-btrfs)

**Ansible role for setting up btrfs.**

## Supported Platforms

Should work on any Linux distribution with systemd and btrfs-progs.

## Requirements

Ansible 2.12 or higher.

## Variables

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `btrfs_scrub_email` | "" | Email address to send failure reports to, `mail` must be preconfigured. |
| `btrfs_scrub_from_email` | "" | Sets email from-address. |
| `btrfs_scrub_targets` | [] | List of scrub targets. |
| `btrfs_scrub_oncalendar` | *-*-01 03:00:00 | OnCalendar spec for scrub timer, defaults to 3am on the 1st of every month. |
| `btrfs_scrub_parallel` | false | Experimental, set to true to run scrubs in parallel. |

## Dependencies

None.

## Example Playbook

```yaml
---

- hosts: all
  become: true
  gather_facts: true
  roles:
    - role: btrfs
      vars:
        btrfs_scrub_targets:
          - "/"
          - "/srv/example"
          # For RAID56 it's recommended you scrub each disk instead of the filesystem
          - "/dev/disk/by-id/ata-whatever01"
          - "/dev/disk/by-id/ata-whatever02"
          - "/dev/disk/by-id/ata-whatever03"
```

## Author

[Andrei Costescu](https://github.com/cosandr/)
