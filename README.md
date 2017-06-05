Ansible Dovecot Role
====================

This role installs Dovecot and (very) basic configuration. PRs wecomed.

Semantic versionning is used (upgrading minor or patch *should* be safe).

Variables
---------

- `dovecot_auth_master_user_separator`: Triggers "master logins as user" when set (usually to '*'); (default: False)
- `dovecot_passdbs`: passdb definitions, see below (default: [])
- `dovecot_userdbs`: userdb definitions, see below (default: [])
- `dovecot_mail_location`: where to store mail (default: "mbox:~/mail:INBOX=/var/mail/%u")
- `dovecot_mail_access_groups`: Mail access group (default: False)
- `dovecot_first_valid_uid`: First valid UID (default: False)
- `dovecot_first_valid_gid`: First valid GID (default: False)
- `dovecot_default_login_user`: Default login user, see below (default: False)
- `dovecot_master_users_file`: Where to store master users (default: /etc/dovecot/passwd.master)
- `dovecot_master_users`: Master users, see below (default: {})
- `dovecot_users`:

`dovecot_passdbs and dovecot_userdbs` can be set with the following structure:

```
dovecot_passdbs:
  - driver: passwd-file
    args: "scheme=SHA1 /etc/dovecot/passwd.master"
    master: "yes"
    pass: "yes"
  - driver: passwd-file
    args: "scheme=SHA1 /etc/dovecot/passwd"

dovecot_userdbs:
  - driver:  static
    args: "uid=2222 gid=2222 home=/var/vmail/%d/%n allow_all_users=yes"
```

`dovecot_default_login_user` can be set like so:

```
dovecot_default_login_user:
  user: foo
  group: foo
  uid: 2222
  gid: 2222 
```

The following structure:

```
dovecot_master_users:
  foo: foopass
  bar: barpass
```
will create 2 master users (foo and bar).

Tests
-----

Test can then be run using vagrant:

```
vagrant up
vagrant ssh -c specs
```

Licence
-------

MIT
