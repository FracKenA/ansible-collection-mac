# Mac Collection for Ansible

<!-- [![MIT licensed][badge-license]][link-license] -->
<!-- [![Galaxy Collection][badge-collection]][link-galaxy] -->
<!-- [![CI][badge-gh-actions]][link-gh-actions] -->

This collection includes helpful Ansible roles and content to help with macOS automation. For a good example of the collection's usage, see my [Personal Mac Ansible Playbook](https://github.com/FracKenA/mac-ansible).

Roles included in this collection (click on the link to see the role's README and documentation):

- `frackena.macos.homebrew` ([documentation](https://github.com/FracKenA/ansible-collection-mac/blob/master/roles/homebrew/README.md))
- `frackena.macos.mas` ([documentation](https://github.com/FracKenA/ansible-collection-mac/blob/master/roles/mas/README.md))
- `frackena.macos.dock` ([documentation](https://github.com/FracKenA/ansible-collection-mac/blob/master/roles/dock/README.md))

## Installation

Install via Ansible Galaxy:

```shell
ansible-galaxy collection install frackena.macos
```

Or include this collection in your playbook's `requirements.yml` file:

```yaml
---
collections:
  - name: frackena.macos
```

For a real-world example, see my [My personal mac-ansible](https://github.com/FracKenA/mac-ansible/blob/main/requirements.yml).

### Role Requirements

Requires separate installation of the `elliotweiser.osx-command-line-tools` role. Because Ansible collections are not able to depend on roles, you will need to make sure that role is installed either by manually installing it with the `ansible-galaxy` command, or adding it under the `roles` section of your `requirements.yml` file:

```yaml
---
roles:
  - name: elliotweiser.osx-command-line-tools

collections:
  - name: frackena.macos
```

## Usage

Here's an example playbook which installs some Mac Apps (assuming you are signed into the App Store), CLI tools via Homebrew, and Cask Apps using Homebrew:

```yaml
- hosts: localhost
  connection: local
  gather_facts: false

  vars:
    mas_installed_app_ids:
      - 424389933 # Final Cut Pro
      - 497799835 # Xcode

    homebrew_installed_packages:
      - node
      - nvm
      - redis
      - ssh-copy-id
      - pv

    homebrew_cask_apps:
      - docker
      - firefox
      - google-chrome
      - vlc

  roles:
    - frackena.macos.homebrew
    - frackena.macos.mas
```

For a real-world usage example, see my [Personal Mac Ansible Playbook](https://github.com/FracKenA/mac-ansible).

See the full documentation for each role in the role's README, linked above.

## License

MIT

## Author

This collection was modified by [Ken Dobbins](https://github.com/FracKenA) as a fork of the repo [Ansible Collection Mac](https://github.com/geerlingguy/ansible-collection-mac) created by [Jeff Geerling](https://www.jeffgeerling.com), author of [Ansible for DevOps](https://www.ansiblefordevops.com).

<!-- [badge-gh-actions]: https://github.com/FracKenA/ansible-collection-mac/workflows/CI/badge.svg?event=push -->
<!-- [link-gh-actions]: https://github.com/FracKenA/ansible-collection-mac/actions?query=workflow%3ACI -->
<!-- [link-galaxy]: https://galaxy.ansible.com/frackena/mac -->
<!-- [link-license]: https://github.com/FracKenA/ansible-collection-mac/blob/master/LICENSE -->
