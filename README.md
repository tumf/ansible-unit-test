ansible-role-test-init
======================

A unit testing framework for Ansible.

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
|ansible_unit_test_group|string||(testing group)

> **Note**
> `prefix_dir` is obsolate.

## How to start your Ansible role project.


### 1. Generate ansible role template files.

```
ansible-galaxy init ansible-role-docker-machine
cd ansible-role-docker-machine
curl -sL https://raw.githubusercontent.com/tumf/ansible-unit-test/master/ansible-role-test-init |bash
```

Generated files are as below:

    ansible-role-docker-machine
    ├── README.md
    ├── defaults
    │   └── main.yml
    ├── files
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── tasks
    │   └── main.yml
    ├── templates
    ├── tests
    │   ├── cases
    │   ├── run
    │   └── test.yml
    └── vars
        └── main.yml


### 2. Run all tests.

Run as follows:

```
./tests/run
```

### 3. Creaet first test case

Create your first test case named 'install' as belows:


```tests/task.yml
---
- hosts: 127.0.0.1
  connection: local
  tags:
    - install
  roles:
    - role: ../..
```

Run the `install` task as belows:

```
./tests/run install
```

### 4. Add set up tasks.

The tasks tagged to 'install-setup' are set up tasks for a test case named `install`.

```tests/task.yml
---
- hosts: 127.0.0.1
  connection: local
  tags:
    - install-setup
  tasks:
    -debug: msg=my-setup-tasks

- hosts: 127.0.0.1
  connection: local
  tags:
    - install
  roles:
    - role: ../..
```



### 5. Update set up task.

Update your test case by role.

```
run -w install
```

### 6. Skip Task

Skip some tasks in unit testing:


```
- name: Configuring service
  service:
    name: newrelic-sysmond
    state: "{{ newrelic_service_state }}"
    enabled: "{{ newrelic_service_enabled }}"
  when: not ansible_unit_test
```


### 7. Output Path

You must prepend `ansible_unit_test_prefix_dir` to the output path.


```
- name: Create Install Directory
  file: path="{{ ansible_unit_test_prefix_dir }}/usr/local/bin" state=directory recurse=yes
```
