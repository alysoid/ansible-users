# [Catena](https://github.com/alysoid/catena) Ansible Role: users

Manage system [users and groups](https://wiki.archlinux.org/title/users_and_groups).

## Role variables

### `system_users`

It uses [ansible.builtin.user](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/user_module.html) and [ansible.posix.authorized_key](https://docs.ansible.com/ansible/latest/collections/ansible/posix/authorized_key_module.html) modules in combination.

```yaml
# Default
system_users: []

# Example
system_users:
  - username: satoshi
    password: "{{ password }}"
    # Description (aka Gecos) of user account
    # https://www.redhat.com/sysadmin/linux-gecos-demystified
    comment: Satoshi Nakamoto
    # Comma separated groups user will be added to
    # When empty '', the user is removed from all groups
    groups: adm,sys
    shell: /bin/bash
    authorized_keys:
      - key: "{{ lookup('file', '~/.ssh/id_ed25519.pub') }}"
        state: present
    # Remove the user account when state is 'absent'
    remove: no
    state: present
```

### `system_groups`

It uses [ansible.builtin.group](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/group_module.html) module.

```yaml
# Default
system_groups: []

# Example
system_groups:
  - name: backup
    state: absent
  - name: bitcoin
    state: present
    gid: 2009
```
