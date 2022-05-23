# Chapter 1

## inventory

config file in `.ini` format that groups remote machines to run ansible plays on. You can input either hostname, ip-addresses or url to ssh into the remote machine. Since I have set-up the ssh keys, I only have to put the Host in my ssh config file to ssh into these servers.

**Example values:**

* raspi/192.168.1.140 (provided you have the ssh-keys configured)
* user@192.168.1.140
* user@192.168.1.140:222 (if its not using standard port 22 for ssh)

## Ansible.cfg

For general ansible default configs, also in `.ini` format. Can set location of inventory file so you don't have to pass it as cmd-line arguments when running ansible.

## Ping test

Run `ansible -i inventory example -m ping`

`-i` flag is to point to inventory file. The command runs an example play that pings all servers.
