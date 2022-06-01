# Chapter 2

## Building infrastructure with Vagrant for testing

Vagrant is a software used to test ansible playbooks, by testing the commands against local VMs created so we do not affect any production servers.

## Vagrantfile

Run `vagrant init <box name>` to initialize a Vagrantfile. Refer to [vagrant cloud](https://app.vagrantup.com/boxes/search?provider=virtualbox) to search for publicly available vagrant boxes for templates.

## Inventory file

1. The first block puts both of our application servers into an ‘app’ group.
2. The second block puts the database server into a ‘db’ group.
3. The third block tells ansible to define a new group ‘multi’, with child groups,
and we add in both the ‘app’ and ‘db’ groups.
4. The fourth block adds variables to the multi group that will be applied to all
servers within multi and all its children.

## Ansible parallel feature

By default, Ansible will run your commands in parallel, using multiple process forks, so the command will complete more quickly. If you’re managing a few servers, this may not be much quicker than running the command serially, on one server after the other, but even managing 5-10 servers, you’ll notice a dramatic speedup if you use Ansible’s parallelism (which is enabled by default).

Run the same command again, but this time, add the argument `-f 1` to tell Ansible to use only one fork (basically, to perform the command on each server in sequence)

## Useful ad-hoc commands

* df -h
  * check for free device space
* free -m
  * check for available memory space
* date
  * check for date/timezone information

## Useful ansible modules

* `setup`
  * useful information regarding the machine

## Making changes using Ansible modules

We want to install the chrony daemon on the server to keep the time in sync. Instead
of running the command yum install -y chrony on each of the servers, we’ll use
ansible’s yum module to do the same (just like we did in the playbook example earlier,
but this time using an ad-hoc command).

`ansible multi -b -m yum -a "name=chrony state=present`

-b flag escalates to sudo priviledge
