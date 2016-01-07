ansible-role-test-init
======================

UnitTesting Framwork for Ansible.

## Install

### Option 1 - Download

Change script install directory.

```bash
cd ~/bin
```

Download

```bash
curl https://raw.githubusercontent.com/tumf/ansible-unit-test/master/ansible-role-test-init > ansible-role-test-init
chmod +x ansible-role-test-init
```

Run

```bash
~/bin/ansible-role-test-init
```

### Option 2 - Direct run

in role directory.

```
curl -s https://raw.githubusercontent.com/tumf/ansible-unit-test/master/ansible-role-test-init |bash
```

## Variables

|name|type|default|in test
|----|----|-------|-------
|ansible_unit_test_prefix_dir|string|""|./tests/outputs/{case}
|ansible_unit_test|boolean|false|true
|ansible_unit_test_user|string||(testing user)
|ansible_unit_test_group|string|(testing group)

> **Note**
> `prefix_dir` is obsolate.

```
