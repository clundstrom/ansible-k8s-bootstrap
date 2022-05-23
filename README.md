# Ansible K8s bootstrapping for 2 node Raspberry Pi 3 & 4 cluster

These plays are defined for a clean Ubuntu server 20.04 LTS vanilla installation.

## SSH setup

Run the following commands to configure public key authentication for the nodes.

```bash
ssh-keygen -t ed25519 -C "admin"
ssh-copy-id -i ~/.ssh/admin.pub <host_address>
````

## Test connection

`ansible all -m ping`


## Run the base config

Optional: Dry run with `--check --diff` to see what will change.

`ansible-playbook base_config.yaml --diff -u ubuntu --ask-vault-pass -e @secrets.yaml`

## Vault management

1. Create a file secrets.yaml
```yaml
---
k8s_admin_password: "<your password>"
```

2. (Optional): Create a vault.pass file to store the vault password.
3. Encrypt with `ansible-vault encrypt secrets.yaml`


### Viewing secrets

`ansible-vault view secrets.yaml`


## Bootstrap cluster

Use k8s user with sudo for bootstrapping.

`ansible-playbook bootstrap.yaml --check --diff -u k8s -K`