# Ansible K8s cluster bootstrap on Raspberry Pi 4

These plays are defined for a clean Ubuntu server 20.04 LTS vanilla installation



## SSH setup

Run the following commands to configure public key authentication for the nodes.

```bash
ssh-keygen -t ed25519 -C "admin"
ssh-copy-id -i ~/.ssh/admin.pub <host_address>
````

## Test connection

ansible all --key-file ~/.ssh/admin -i inventory -m ping



