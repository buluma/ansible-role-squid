# [Ansible role squid](#ansible-role-squid)

Install and configure squid on your system.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/buluma/ansible-role-squid/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-squid/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-squid/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-squid)|[![downloads](https://img.shields.io/ansible/role/d/buluma/squid)](https://galaxy.ansible.com/buluma/squid)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-squid.svg)](https://github.com/buluma/ansible-role-squid/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-squid/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
- become: true
  gather_facts: true
  hosts: all
  name: Converge
  roles:
  - role: buluma.squid
    squid_acls:
    - classifier: src
      name: localnet
      value: 0.0.0.1-0.255.255.255
    squid_cache_dir: aufs /var/spool/squid 16000 16 256 max-size=8589934592
    squid_cache_replacement_policy: heap LFUDA
    squid_maximum_object_size_mb: 256
    squid_rules:
    - acl: to_localhost
      decision: deny
    - acl: localnet
      decision: allow
    - acl: localhost
      decision: allow
    - acl: all
      decision: deny
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-squid/blob/master/molecule/default/prepare.yml):

```yaml
- become: true
  gather_facts: false
  hosts: all
  name: Prepare
  roles:
  - role: buluma.bootstrap
  - role: buluma.core_dependencies
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-squid/blob/master/defaults/main.yml):

```yaml
squid_cache_dir: ufs /var/spool/squid 100 16 256
squid_port: 3128
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-squid/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-core_dependencies)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-squid/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Alpine](https://hub.docker.com/r/buluma/alpine)|all|
|[Amazon](https://hub.docker.com/r/buluma/amazonlinux)|all|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|all|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[opensuse](https://hub.docker.com/r/buluma/opensuse)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-squid/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-squid/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

