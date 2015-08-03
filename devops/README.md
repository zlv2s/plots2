# Getting a virtual machine deployment up and running

This is a required step if you do not have a remote target to deploy a system
onto. Remote targets can include Linode, Rackspace, Amazon EC2, etc. Usually
a local virtual machine is better than a remote target for testing and
development.

1. Install [vagrant](http://docs.vagrantup.com/v2/installation/index.html)
1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
1. Run a shell and switch to the project's code repository
1. `cd devops`
1. `vagrant up`

Vagrant will download a disk image with Linux installed that is ready for use
with Vagrant and turn it into a virtual machine. Vagrant will then run an 
Ansible deployment to prepare the virtual machine for running the project's
code.

# Deploying with Ansible

## onto a Vagrant virtual machine

If using Vagrant, Vagrant calls Ansible in a way that requires no
inventory or any additional work for the user.

If the virtual machine is not yet running, `vagrant up` will deploy the
virtual machine and deploy the software provisioned by Ansible.

If the virtual machine is already running and the software needs to be
provisioned again, `vagrant provision` will deploy the software provisioned by
Ansible to the running VM.

## onto some other system

This requires having access to Ansible on the local machine.

### Install Ansible software using virtual environments

The
[installation instructions](http://docs.ansible.com/intro_installation.html#running-from-source) 
are a bit overzealous. Here is a much simpler way to get Ansible installed:

1. checkout the Ansible git repository and switch to the devel branch.
  1. `git clone https://github.com/ansible/ansible.git`
  1. `cd ansible`
  1. `git checkout devel`
1. install virtualenv. on Debian-based systems, `sudo apt-get install virtualenv`
1. in some directory, create a Python virtual environment sandbox using `virtualenv ansible-venv`
1. run `source ansible-venv/bin/activate`
1. install prereqs with `pip install paramiko PyYAML Jinja2 httplib2`
1. switch to the ansible git repo directory and run `python setup.py install`

To run ansible from this install method, ensure the virtual environment is
activated with `source ansible-venv/bin/activate` before calling `ansible`.

### Updating Ansible software using virtual environments

Hop into the local Ansible git repo. Run `git pull origin devel` and
`git submodule update --recursive`. This brings the Ansible code up to date.

Load up the Ansible virtual environment with `source ansible-env/bin/activate`.
While active, go back to the ansible code repo and run
`python setup.py install`. This will install the new Ansible code over top
the previous installation, replacing it.

### Check your system inventory

The system inventory contains systems Ansible can push deployments to. See
[Ansible's instructions](http://docs.ansible.com/intro_inventory.html).

run updates against git
http://docs.ansible.com/git_module.html

vagrant
http://docs.ansible.com/guide_vagrant.html

rackspace
http://docs.ansible.com/guide_rax.html

http://docs.ansible.com/apt_module.html

http://docs.ansible.com/playbooks_best_practices.html
