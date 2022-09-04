<!-- Badges -->
<!--

If pre-commit ci is enabled, uncomment the badge below
and replace with the repository name

[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/owner/<repo>/main.svg)](https://results.pre-commit.ci/latest/github/owner/<repo>/main)
-->

<!-- Actions status -->
<!--
If there are Github Actions, uncomment the line below to add the
status badge
[![main](https://github.com/owner/<repo>/actions/workflows/main.yml/badge.svg)](https://github.com/owner/<repo>/actions/workflows/main.yml)
-->
[![semantic-release: angular](https://img.shields.io/badge/semantic--release-conventional-e10079?logo=semantic-release)](https://github.com/semantic-release/semantic-release)

# Ansible role Vault Agent

An Ansible role to provision Vault Agent to nodes.
Most of the configuration assumes a static deployment, aside an existing Vault cluster.
Auto auth is only implemented for approle initially.

## Requirements

- Vault server
- If using auto_auth with approle: client token capable of looking up the role id on the approle

## Role Variables

See `defaults/main.yml`

## Dependencies

## Example Playbook

```yaml

---
- name: Preflight
  hosts: localhost
  tasks:
    - name: Check Vault token
      ansible.builtin.assert:
        that: lookup('env', 'VAULT_TOKEN') != ''
        fail_msg: No Vault token set 📪
        success_msg: Vault token present 🔐
        quiet: False
- name: Deploy vault agent
  hosts: pis,!vault_servers
  become: true
  roles:
    - ansible-role-vault-agent

```

## License

MIT

## Author Information

Bruce Becker <brucellino@hey.com> @brucellino <https://www.brucellino.com>
