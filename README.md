# ansible-role-ssh

[![Build Status](https://travis-ci.org/mjhenke/ansible-role-ssh.svg?branch=master)](https://travis-ci.org/mjhenke/ansible-role-ssh) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-ansible--role--ssh-blue.svg)](https://galaxy.ansible.com/mjhenke/ansible-role-ssh)

A light weight role for setting up OpenSSH server on Debian based systems.

#### Requirements
None

#### Variables
* `ssh_server_local_key`: [default: `~/.ssh/id_rsa`]: Specifies the local key to be used to ssh into the host machine.  If the local key is not found it will be generated.
* `ssh_server_remote_key`: [default: none]: Specifies a remote host key to be present.  If specified and not found, a key will be generated.
* `ssh_server_permit_root_login`: [default: `without-password` or `yes` depending on OS version, see `defaults/main.yml`]: Specifies whether root can log in using ssh.

* `ssh_server_x11_forwarding`: [default: `true`]: Specifies whether X11 forwarding is permitted.
* `ssh_server_x11_display_offset`: [default: `10`]: Specifies the first display number available for `sshd`'s X11 forwarding. This prevents `sshd` from interfering with real X11 servers.
* `ssh_server_x11_use_localhost`: [default: `false`]: Specifies `sshd` binding to loopback address of wildcard address.

* `ssh_server_allow_groups`: [default: `[sshlogin]`]: A list of group name patterns. If specified, login is allowed only for users whose primary group or supplementary group list matches one of the patterns. Groups will be created if not already.
* `ssh_server_allow_users`: [default: `[]`]: A list of user name patterns. If specified, login is allowed only for user names that match one of the patterns.
* `ssh_server_deny_groups`: [default: `[]`]: A list of group name patterns. If specified, login is disallowed for users whose primary group or supplementary group list matches one of the patterns.  Groups will be created if not already.
* `ssh_server_deny_users`: [default: `[]`]: A list of user name patterns. If specified, login is disallowed for user names that match one of the patterns.

## Dependencies
None

#### Example
```yaml
---
- hosts: all
  roles:
    - ansible-role-ssh
```

```yaml
---
- hosts: all
  tasks:
  - include_role: 
      name: ansible-role-ssh
    vars:
      ssh_server_local_key: '~/.ssh/user_id_rsa'
```

#### License
MIT

#### Author Information
Michael Henke

#### Feedback, bug-reports, requests, ...
Are [welcome](https://github.com/mjhenke/ansible-role-ssh/issues)!
