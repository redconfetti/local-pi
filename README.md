# local-pi

Ansible config for my personal Raspberry Pi running Docker

Tested with a fresh installation of Raspberry Pi OS Lite (64-bit),
a port of Debian Bullseye with no desktop environment.
Applied to SD card via [Raspberry Pi Imager][2] with Advanced options
pre-configuring hostname, user, SSH, wifi, and locale settings.

Local SSH config in `~/.ssh/config`:

```ini
Host derek
  HostName 192.168.1.51
  User jason
  Port 22

Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```

- [Setup](docs/setup.md)
- [Usage](docs/usage.md)

## External Roles

- Ansible Timezone - [Galaxy][1] [Source][0]

[0]: https://github.com/yatesr/ansible-timezone
[1]: https://galaxy.ansible.com/yatesr/timezone
[2]: https://www.raspberrypi.com/software/
