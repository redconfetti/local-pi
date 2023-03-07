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
ansible-playbook playbook.yml --tags "docker"
```

## Docker Context

After installing the Docker Desktop on your local machine, the 'default'
context used by the Docker client is for the Docker Engine running natively
on your machine.

If you want to connect to your Raspberry Pi running Docker, you'll need
to configure an alternative context.

The Docker Engine is not exposed on a public port of the Raspberry Pi node by
default. It's recommended that you use SSH to connect to a Docker Engine node.

```bash
# list current contexts
$ docker context list
NAME             TYPE   DESCRIPTION           DOCKER ENDPOINT                               ORCHESTRATOR
default *        moby   Current DOCKER_HOST   unix:///var/run/docker.sock                   swarm
desktop-linux    moby                         unix:///Users/jason/.docker/run/docker.sock
rpi              moby                         ssh://jason@192.168.1.51                      swarm

# test ssh into server and accept ECDSA key
ssh -l jason -- 192.168.1.51

# create new context using local docker node
$ docker context create rpi \
  --default-stack-orchestrator=swarm \
  --docker host=ssh://jason@192.168.1.51
Successfully created context "rpi"

# switch to the new context
$ docker context use rpi
rpi
Current context is now "rpi"

# list docker services
$ docker ps
"CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES"
```

[docker context]: https://docs.docker.com/engine/context/working-with-contexts/
