---
title: An Ansible Playbook for Docker Development
published: true
---
An easy way to run docker in a VM.

## Ansible Playbook

I threw together a quick [playbook to run docker inside a Vagrant VirtualBox VM](https://bitbucket.org/ngstigator/ansible-playbook-dockerhost/) (Ubuntu or CentOS). As we are running docker as the vagrant user, group inclusion is denoted in the playbook.

## Volume Gotchas

I ran into a small hiccup with volumes that weren't being populated in the specified host directory, which turned out to be folder permissions issue. Ensure that the host directories where docker volumes are stored are owned by "vagrant:docker", and it doesn't hurt to have them group-writable.
