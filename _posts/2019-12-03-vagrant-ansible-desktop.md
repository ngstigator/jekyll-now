---
published: false
---
## Disposable Development Desktops using Vagrant and Ansible

If you're like me, you live in morbid fear of messing up your development environment. Having to uninstall tools, reinstall them again, or worse, having to redo your entire OS because you've arrived at an unrecoverable state is the bane of an IT worker's existence.

But what if you can simply throw away your broken configuration, and start fresh with a few simple steps? Now I've tried this with [VirtualBox](https://www.virtualbox.org/) and using the snapshot feature. This required that I start from clean desktop and painstakingly install and configure my development environment properly. I found this to be clunky and I didn't trust my past self to have saved a snapshot from where I could get to where I wanted to go to get something done. If something was broken, I'd have to go back snapshots until I had one that I can safely start from and I'm almost back to square one.

A better way might be to treat desktops like we do servers, and create, destroy, and recreate them as needed. With this in mind, I put together an [Ansible playbook](https://bitbucket.org/ngstigator/ansible-vagrant-desktop/src/master/) from which I can run against a Vagrant Ubuntu instance, and voila, I can have as many desktops as I want, with individual configurations that are stored in version control.

I learned some things about Vagrant and Ansible along the way. I may create an actual Vagrant box for this but for now it does what I need. Now back to work...
