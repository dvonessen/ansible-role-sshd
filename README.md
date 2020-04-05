# Ansible sshd role

This role installs and configures `sshd` in a secure way.
It configures, that Ciphers, Key Exchange and MACs to ensure secure communication.

All configuration options inside this role are well documented in **man(5) sshd_config**.

## Description



## Role Variables

| Name                              | Default                                                                                                                   | Description                                                                                         |
| :-------------------------------- | :------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------------- |
| `sshd_config_port`                | 22                                                                                                                        | TCP Port on which `sshd` is listening.                                                              |
| `sshd_config_host_key_config`     | []                                                                                                                        | List of sshd host keys to persist on host. For format see: [Format](defautls/main.yml)              |
| `sshd_config_ciphers`             | aes128-ctr,aes192-ctr,aes256-ctr                                                                                          | Ciphers which are allowed.                                                                          |
| `sshd_config_host_key_algorithms` | ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss                                               | Host key algorithms which are allowed.                                                              |
| `sshd_config_macs`                | hmac-sha2-256,hmac-sha2-512,hmac-sha1                                                                                     | Message authentication codes (MACs) which are used.                                                 |
| `sshd_config_kex_algorithms`      | ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha256 | Key exchange algorithms used by sshd and ssh client.                                                |
| `sshd_config_syslog_facility`     | AUTHPRIV                                                                                                                  | SSHd's syslog facility.                                                                             |
| `sshd_config_log_level`           | VERBOSE                                                                                                                   | SSHd's log level.                                                                                   |
| `sshd_config_deny_users`          | []                                                                                                                        | DenyUsers entries, disallows users to login via ssh. For format see: [Format](defautls/main.yml)    |
| `sshd_config_deny_groups`         | []                                                                                                                        | DenyGroups entry, disallows all members of given group. For format see: [Format](defautls/main.yml) |

## Role Tags

| Name           | Description                                                                                                                            |
| :------------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| sshd_all       | Tag to distinct running of sshd role.                                                                                                  |
| sshd_install   | Imports task (install.yml)[tasks/install.yml]. It will ensure, that openssh-server is installed.                                       |
| sshd_configure | Imports task (configure.yml)[tasks/configure.yml]. It will configure opessh-server and will create persistent host keys if configured. |

## Dependencies

**None**

## Example Playbook


```yaml
- name: All
  hosts: all
  debugger: on_failed
  roles:
    - role: ansible-role-sshd
  vars:
    sshd_config_port: 2222
    sshd_config_deny_groups: nginx
```

## Molecule

This role ist tested with molecule.
To run tests with molecule you have to install molecule and vagrant python packages.

```bash
pip install -u molecule molecule-vagrant
```

As you can see above, we are currently using vagrant for testing roles.
Therefor, you have to install vagrant.

## License

MIT License

## Contributors

Daniel von Essen
