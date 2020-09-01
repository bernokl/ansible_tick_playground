# ansible_tick_playground
The intent of this repo is to allow you to install tickstack on a remote ubuntu AWS host that you have ssh access to.

This repo cantains a few basic roles, a couple of playbooks and an inventory to spin up, telegraf, influxdb, chronograf and kapacitor on a single host.
The bootstap playbook will also add some basic packages like docker, and a few others.

This is just POC to have ansible bring the stack up and is not intended for production use.

Telegraf is a direct debian install, the other 3 will be set up as docker containers on the same host
 
From the host where the repo was cloned (a laptop was used for testing) you can run the ansible-playbook commands below, before you start:
- Make sure that you replace the ip address in the inventory file to your intended AWS target.
- In `/etc/ansible/ansible.cfg` add a line to point the roles_path to your roles something like:
`roles_path    = /home/user/projects/tickServerAnsible/roles/`

Next from the root of the repo run.
`ansible-playbook playbooks/bootstrap/bootstrap.yml -i inventories/latest --user=ubuntu --ask-vault-pass`

Once that finishes run:
`ansible-playbook playbooks/bootstrap/tickstack.yml -i inventories/latest --user=ubuntu --ask-vault-pass`

Although not strictly needed the vault was encrypted to simulate a real world use case. The vault password is set to `Go3!egeheim`
