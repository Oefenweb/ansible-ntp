## ntp

[![CI](https://github.com/Oefenweb/ansible-ntp/workflows/CI/badge.svg)](https://github.com/Oefenweb/ansible-ntp/actions?query=workflow%3ACI)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-ntp-blue.svg)](https://galaxy.ansible.com/Oefenweb/ntp)

Set up a ntp server in Debian-like systems.

#### Requirements

None

#### Variables

 * `ntp_driftfile` [default: `/var/lib/ntp/ntp.drift`]]: This command specifies the name of the file use to record the frequency offset of the local clock oscillator
 * `ntp_statsdir` [default: `false`]]: Set this (to `/var/log/ntpstats`) if you want statistics to be logged (**Must not end with a slash**)
 * `ntp_statistics` [default: `[loopstats, peerstats, clockstats]`]]:
 * `ntp_filegens` [default: `['loopstats file loopstats type day enable', 'peerstats file peerstats type day enable', 'clockstats file clockstats type day enable']`]]:
 * `ntp_servers` [default: `[0.ubuntu.pool.ntp.org, 1.ubuntu.pool.ntp.org, 2.ubuntu.pool.ntp.org, 3.ubuntu.pool.ntp.org, ntp.ubuntu.com]`]]: The servers to sync time with
 * `ntp_restricts` [default: `['-4 default nomodify nopeer noquery notrap', '-6 default nomodify nopeer noquery notrap', '127.0.0.1', '::1']`]]:
 * `ntp_enables` [default: `[]`]]: Provides a way to enable various server options
 * `ntp_disables` [default: `[monitor]`]]: Provides a way disable various server options
 * `ntp_broadcast` [default: `false`]]: In broadcast mode the local server sends periodic broadcast messages to a client population at the address specified
 * `ntp_broadcastclient` [default: `false`]]: This command enables reception of broadcast server messages to any local interface

#### Dependencies

None

## Recommended

* `ansible-logrotated` ([see](https://github.com/Oefenweb/ansible-logrotated), when `ntp_statsdir != false`)

#### Example (simple)

```yaml
---
- hosts: all
  roles:
    - oefenweb.ntp
```

#### Example (with statistics to be logged (and rotated))

```yaml
---
- hosts: all
  roles:
    - oefenweb.ntp
    - oefenweb.logrotated
  vars:
    ntp_statsdir: /var/log/ntpstats
    logrotated_logrotate_d_files:
      ntpstats:
        - logs:
            - '/var/log/ntpstats/*'
          weekly: true
          missingok: true
          rotate: 8
          compress: true
          delaycompress: true
          notifempty: true
          copytruncate: true
```

#### License

BSD

#### Author Information

Mischa ter Smitten (based on work of [Benno Joy](https://github.com/bennojoy))

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-ntp/issues)!
