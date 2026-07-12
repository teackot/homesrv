An atomic bootc image for my home server with Funkwhale!

Build a container image locally:

```bash
just pull # (optional)
just build
```

Build an interactive Anaconda installer ISO image:

```bash
just prepare_interactive
sudo podman pull ghcr.io/teackot/homesrv:44
sudo just registry=ghcr.io/teackot image=srv tag=44 disk
```

Build an unattended Anaconda installer ISO image:

```bash
just prepare_unattended user defaultpassword "ssh-ed25519 abcdef123456..."
sudo podman pull ghcr.io/teackot/homesrv:44
sudo just registry=ghcr.io/teackot image=srv tag=44 disk_type=anaconda-iso disk
```

### Known issues

#### `systemd-remount-fs.service` fails on boot

Happens because Anaconda adds an fstab entry for `/`. Tracked here: https://github.com/bootc-dev/bootc/issues/971

To fix simply remove the `/` entry from fstab
