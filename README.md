itiut.pip-packages
=========

[![Build Status](https://travis-ci.org/itiut/ansible-role-pip-packages.svg?branch=master)](https://travis-ci.org/itiut/ansible-role-pip-packages)
[![Ansible Role](https://img.shields.io/ansible/role/5234.svg)](https://galaxy.ansible.com/list#/roles/5234)

Ansible role for configuring pip packages.

Requirements
------------

- pip
- Ansible 1.8 or higher

Role Variables
--------------

Role variables are in [defaults/main.yml](defaults/main.yml).

#### `pip_packages_default_install_state` (default: `present`)

A default state of installing (or installed) packages: `present` or `latest`.

#### `pip_packages_install` (default: `[]`)

An array of packages to install.  
A package is specified by 2 ways:
- A string of the package name
- A hash with following keys:
  - `name` (required): name of the package
  - `version` (optional): version of the package
  - `state` (optional): state of the package (`present` or `latest`)

##### Example

```yaml
- vars:
    pip_packages_install:
      - virtualenv
      - { name: bottle, version: 0.12.1 }
      - { name: pep8, state: latest }
```

#### `pip_packages_remove` (default: `[]`)

An array of package names to remove.

#### `pip_packages_executable` (default: `''`)

An executable name or path for pip.  
If this variable evaluate to false (e.g. empty string `''`), it is ignored.

Example Playbooks
----------------

Ensure that `virtualenv`, `bottle` (v0.12.1) and `pep8` (latest) are installed.

```yaml
- hosts: localhost
  roles:
    - role: itiut.pip-packages
      pip_packages_install:
        - virtualenv
        - { name: bottle, version: 0.12.1 }
        - { name: pep8, state: latest }
```

Ensure that `pep8` (latest) are installed by `pip3`.

```yaml
- hosts: localhost
  roles:
    - role: itiut.pip-packages
      pip_packages_install:
        - pep8
      pip_packages_default_install_state: latest
      pip_packages_executable: pip3
```

TODO
-------

- Support other options of pip module (e.g. requirements, virtualenv)

License
-------

MIT
