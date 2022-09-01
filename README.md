# pcanham.systemd_mount

An ansible role to set up mount points with Systemd (this role does not
consider `/etc/fstab` file).

## Requirements

None

## Dependencies

None

## Role Variables

Only one variable is required: `mounts`: a list of mount objects with the following properties:

* `description`: a description of the partition to mount,

* `source`: identify the partition to mount, as given to the `mount` command. Examples: `/dev/sdb1`, `/dev/disk/by-uuid/xxxx-xxx-xxx-xxx`,

* `dest`: path where to mount the partition,

* `type`: filesystem type, as given to the `mount` command with the `-t` argument (can be `auto` or `none`),

* `options`: mount options, as given to the `mount` command with the `-o` argument,

* `after`, `wants`, `wantedby`: options for the Systemd unit file. If not
  defined, `after` and `wants` are omitted. On the other hand, `wantedby` has a
default value: `multi-user.target`.

## Example Playbook

```yaml
- hosts: servers
  vars:
    - mounts:
        - description: External Harddrive
          source: /dev/disk/by-uuid/xxxxxx-xxx-xxx-xxxxxx
          dest: /mnt/harddrive
          type: ext4
          options: default
  roles:
    - role: pcanham.systemd_mount
```
