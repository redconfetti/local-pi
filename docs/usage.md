# Usage

## Ansible Vault

```bash
# edit vault file
ansible-vault edit secrets.yml

# view contents of vault file
ansible-vault view secrets.yml
```

## Playbooks

There is a single playbook you can run against the Raspberry Pi host.
It is expected that your SSH client is configured to connect to the host
using a private SSH key without passphrase, and then use sudo on the remote
server to perform actions.

```bash
ansible-playbook playbook.yml
```

Alternatively you can run a specific role if you specify it by a tag

```bash
ansible-playbook playbook.yml --tags "common"
ansible-playbook playbook.yml --tags "motd"
```
