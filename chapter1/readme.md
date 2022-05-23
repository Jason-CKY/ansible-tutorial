# Chapter 1

## Inventory file

config file in `.ini` format that groups remote machines to run ansible plays on. You can input either hostname, ip-addresses or url to ssh into the remote machine. Since I have set-up the ssh keys, I only have to put the Host in my ssh config file to ssh into these servers.

**Example values:**

* raspi/192.168.1.140 (provided you have the ssh-keys configured)
* user@192.168.1.140
* user@192.168.1.140:222 (if its not using standard port 22 for ssh)

**note:**

You can run `ansible <command> -m ping --ask-pass` if you use password-authentication for ssh access

## Ansible.cfg

For general ansible default configs, also in `.ini` format. Can set location of inventory file so you don't have to pass it as cmd-line arguments when running ansible.

## Ping test

Run `ansible -i inventory example -m ping`

`-i` flag is to point to inventory file. The command runs an example play that pings all servers.

Run `ansible example -m ping` if you have set `ansible.cfg` the location of `inventory` file.

## Ad-hoc commands

Run ad-hoc linux commands to your remote hosts with `-a` flag.

For example, run `ansible example -a "free -h"` to find out how much free memory space you have on each remote machine.

## Ansible commands

### Pattern

When you execute Ansible through an ad hoc command or by running a playbook, you must choose which managed nodes or groups you want to execute against. Patterns let you run commands and playbooks against specific hosts and/or groups in your inventory. An Ansible pattern can refer to a single host, an IP address, an inventory group, a set of groups, or all hosts in your inventory. Patterns are highly flexible - you can exclude or require subsets of hosts, use wildcards or regular expressions, and more. Ansible executes on all inventory hosts included in the pattern

The `inventory` file groups remote machines under `example` header, thus all the commands run uses `ansible example <module> <args>`, which means the run the modules against the list of remote machines under `example` pattern.

### Modules

Default module is `command`, which runs the command directly onto the server. We previously run `ansible example -m ping` which runs the `ping` module to ping all the remote machines.

### Arguments

Gives arguments to the module if needed. This is done via the `-a` flag. For example, `ansible example -a "free -h"` runs the default `command` against `example` pattern, with the arguments `free -h`.
