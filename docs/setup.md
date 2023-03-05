# Setup

## Install Ansible

You have to install Ansible to make use of this configuration. The following
instructions are intended with systems running Mac OSX with [Homebrew]
already installed.

[Homebrew]: https://brew.sh/

Install Ansible:

```bash
brew install ansible
```

## SSH Configuration

It is assumed that your SSH config is specifying a username and private
key that corresponds to the root user, or user with sudo privileges on the
server.

```ssh-config
Host derek
  Hostname 192.168.1.50
  User jason
  IdentityFile ~/.ssh/id_ed25519
```

## Ansible Galaxy

Install the [Ansible Galaxy](https://galaxy.ansible.com/) dependencies using
the following command:

```bash
ansible-galaxy install -r requirements.yml
```

## Ansible Vault

The most sensitive settings are stored in `settings.yml`, which is encrypted
using Ansible Vault. A single password is used to unencrypt this file,
stored in `~/.vault_pass`. Run the following command to create a random password
in this file:

```bash
openssl rand -base64 48 > ~/.vault_pass && chmod 600 ~/.vault_pass
```

Run the following command to initialize your `settings.yml` Vault file using
the contents of `settings-example.yml` as a template.

```bash
ansible-vault encrypt secrets-example.yml --output secrets.yml
```

Ansible-Vault uses the default editor you have configured. Add the following
to your `~/.bash_profile` configuration to easily edit the `secrets.yml`
file.

```bash
export EDITOR="codium --wait"
```

To view or edit the Vault file, run the following commands:

```bash
# edit vault file
ansible-vault edit secrets.yml

# view contents of vault file
ansible-vault view secrets.yml
```

By default this file is not included in the repository. You can comment this
out in `.gitignore` to ensure it is included in your repository.

For more details, see [Ansible Vault]

[Ansible Vault]: https://docs.ansible.com/ansible/latest/user_guide/vault.html
