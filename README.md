# [squid](#squid)

Install and configure squid on your system.

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-squid/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-squid/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-squid/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-squid)|[![quality](https://img.shields.io/ansible/quality/61208)](https://galaxy.ansible.com/buluma/squid)|[![downloads](https://img.shields.io/ansible/role/d/61208)](https://galaxy.ansible.com/buluma/squid)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-squid.svg)](https://github.com/buluma/ansible-role-squid/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-squid.svg)](https://github.com/buluma/ansible-role-squid/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-squid.svg)](https://github.com/buluma/ansible-role-squid/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: buluma.squid
      squid_cache_dir: "aufs /var/spool/squid 16000 16 256 max-size=8589934592"
      squid_cache_replacement_policy: heap LFUDA
      squid_maximum_object_size_mb: 256
      squid_acls:
        - name: localnet
          classifier: src
          value: "0.0.0.1-0.255.255.255"
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

The machine needs to be prepared. In CI this is done using `molecule/default/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: buluma.bootstrap
    - role: buluma.core_dependencies
```


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for squid

# The port squid is listening on.
squid_port: 3128

# The directory where (and how) to cache.
squid_cache_dir: ufs /var/spool/squid 100 16 256
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-squid/blob/main/requirements.txt).

## [Status of used roles](#status-of-requirements)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab ](https://gitlab.com/buluma/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-bootstrap)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|[![Build Status GitLab ](https://gitlab.com/buluma/ansible-role-core_dependencies/badges/main/pipeline.svg)](https://gitlab.com/buluma/ansible-role-core_dependencies)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-squid/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|alpine|all|
|amazon|Candidate|
|el|8|
|debian|all|
|fedora|all|
|opensuse|all|
|ubuntu|all|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.


If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-squid/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-squid/blob/master/CHANGELOG.md)

## [License](#license)

Apache-2.0

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

### [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
