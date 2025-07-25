# beingtomgreen.network_mounts

A simple Ansible role to install and configure NFS & SMB mounts on Debian/Ubuntu based systems.

## Installation & usage

Given that Galaxy seems to have abandoned roles, I suggest referencing this repository directly in your projects `requirements.yml`:

```yaml
---

roles:
  - name: beingtomgreen.network_mounts
    src: https://github.com/BeingTomGreen/ansible-role-network-mounts.git

collections: []
```

You can then install it alongside your other requirements as normal:

```bash
ansible-galaxy install -r requirements.yml
```

Now you're free to use it within your project:

```yaml
---

- hosts: my-little-server
  become: true
  vars:
    # Do we want to install smb/nfs clients?
    network_mounts_install_smb_utils: true
    network_mounts_install_nfs_utils: true

    # The mount points will be owned by
    network_mounts_user: media
    network_mounts_group: media

    # Our mounts
    network_mounts:
      - src: '192.168.6.9:/mnt/share'
        path: '/mnt/nfs-server/share'
        fstype: 'nfs'
      - src: '//smb-server/share'
        path: '/mnt/smb-server/share'
        fstype: 'cifs'
        opts: 'username=foo,password=bar,uid=1000,gid=1000'
        state: 'absent'

  roles:
     - role: beingtomgreen.network_mounts
```

## Role Variables

See [`defaults/main.yml`](defaults/main.yml) for more details.

## Requirements

None.

## Dependencies

None.

## License

[MIT](LICENSE)

## Author Information

[Tom Green](https://github.com/BeingTomGreen)
