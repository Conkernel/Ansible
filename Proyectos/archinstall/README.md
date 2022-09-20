# Arch-Ansible: an Ansible playbook to install Arch Linux

- El nombre del host quedará como "Archy". Se puede cambir en los ficheros de configuraciones.

- Para un funcionamiento adecuado, es necesario ajustar en el servidor dns el nombre archy

- Comandos de ayuda en mi lab: 
  
  ssh-keygen -f "/home/oloco/.ssh/known_hosts" -R "archy"

  ssh-copy-id root@archy

  cd /mnt/repos/Ansible/Proyectos/archinstall/ansible
  

* Run: ansible-playbook -i hosts.yaml --tags bootstrap,mainconfig site.yaml



Este proyecto no es obra mía.


Desaconsejo totalmente utilizar este repositorio, ni siquiera para prácticas. El enlace al proyecto original es el siguiente. Todos los méritos a su dueñ@:


https://binary-manu.github.io/arch-ansible/


<------- Comienzo del README.md original ------->


[![Stars](https://img.shields.io/github/stars/binary-manu/arch-ansible.svg?style=social&label=Star)](https://github.com/binary-manu/arch-ansible/stargazers)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/binary-manu/arch-ansible/blob/master/LICENSE.txt)
[![Link to the docs](https://img.shields.io/badge/Read%20the%20full%20docs!-%F0%9F%8E%93-brightgreen)][docs]
[![Changelog](https://img.shields.io/badge/Changelog-%F0%9F%97%9E-purple)](CHANGELOG.md)

Arch-Ansible is a playbook designed to install Arch Linux on a target
machine. It was conceived to ease the preparation of virtual machines,
but it can also be used to install on bare metal.

*If you are a new user, please keep reading, otherwise have a look at
the [changelog](CHANGELOG.md) for the latest changes.*

The simplest way to get started is to provision a VM with Arch Linux to
try the playbook out. Both VirtualBox and QEMU (possibly via libvirt)
are supported, but the examples below use VirtualBox because
it has been supported since the start, so the playbook is well-tested
against it.

First, change some default settings by writing the
following YAML snippet to `ansible/group_vars/all/50-user-settings.yaml`
and customize it to suit your regional settings:

```yaml
# Set your timezone, locale and keymap
locale_timezone: Europe/Rome
locale_locale: it_IT.UTF-8
locale_keymap: it
users_root_info:
    # Choose a root password
    password: "abcd$1234_root"
users_info:
  # Change "manu" to your username
  manu:
    # Choose a password for your user.
    # You'll be able to use sudo.
    password: "abcd$1234_manu"
    is_admin: true
```

Now, if you want Packer to build a brand new VM image, type:

```sh
cd packer
packer build -only=virtualbox-iso packer-template.json
```

or, if you prefer to spin up a turn-key Vagrant machine, go with:

```sh
cd vagrant
# A reload is required after provisioning
vagrant up --provider=virtualbox && vagrant reload
```

After login, type `startx` to run the GUI.

There's a good deal of things that can be customized: DE themes,
preinstalled utilities, screensaver behaviour and more. Have a look at
the [documentation][docs] for more information. The [side
projects][side-projects] section links to specific documentation about
integration with Vagrant and Packer.

If you find this project helpful, why not showing some ♥ by giving it a
star on GitHub?

[docs]: https://binary-manu.github.io/arch-ansible
[side-projects]: https://binary-manu.github.io/arch-ansible#side-projects

<!-- vi: set tw=72 et sw=2 fo=tcroqan autoindent: -->
