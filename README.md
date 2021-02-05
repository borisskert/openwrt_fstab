# openwrt_fstab

Ansible role to setup fstab config in OpenWRT.

## Supported operating systems:

* OpenWRT
  * 19.07.x

## System requirements

* package `python3` (at least temporary) installed on target machine

## Role parameters

| Variable      | Type | Default | Description           |
|---------------|------|------------|---------|-----------------------|
| fstab_anon_swap | boolean | true | [See official docs](https://openwrt.org/docs/guide-user/storage/fstab) |
| fstab_anon_mount | boolean | true | [See official docs](https://openwrt.org/docs/guide-user/storage/fstab) |
| fstab_auto_swap  | boolean | false | [See official docs](https://openwrt.org/docs/guide-user/storage/fstab) |
| fstab_auto_mount | boolean | false | [See official docs](https://openwrt.org/docs/guide-user/storage/fstab) |
| fstab_delay_root | boolean | `0`   | [See official docs](https://openwrt.org/docs/guide-user/storage/fstab) |
| fstab_check_fs   | boolean | true  | [See official docs](https://openwrt.org/docs/guide-user/storage/fstab) |

## Usage

### requirements.yml

```yaml
- name: setup_fstab
  src: https://github.com/borisskert/openwrt_fstab.git
  scm: git
```

### Playbook

#### Minimal Playbook

```yaml
- hosts: test_machine
  become: yes

  roles:
    - role: setup_fstab
```

#### Playbook with all parameters

```yaml
- hosts: test_machine
  become: yes

  roles:
    - role: setup_fstab
      fstab_anon_swap: false
      fstab_anon_mount: false
      fstab_auto_swap: true
      fstab_auto_mount: true
      fstab_delay_root: 0
      fstab_check_fs: false
```


## Testing

Requirements:

* [Vagrant](https://www.vagrantup.com/)
* [Ansible](https://docs.ansible.com/)
* [Molecule](https://molecule.readthedocs.io/en/latest/index.html)
* [yamllint](https://yamllint.readthedocs.io/en/stable/#)
* [ansible-lint](https://docs.ansible.com/ansible-lint/)
* [Docker](https://docs.docker.com/)

### Run within docker

```shell script
molecule test
molecule test --scenario-name with-parameters
```

I recommend to use [pyenv](https://github.com/pyenv/pyenv) for local testing.
Within the Github Actions pipeline I use [my own molecule Docker image](https://github.com/borisskert/docker-molecule).

## License

MIT

## Author Information

* [borisskert](https://github.com/borisskert)
