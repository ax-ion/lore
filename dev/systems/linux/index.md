# Linux — Systems

---

## XDG Base Directory Standard

Where applications store their files. Follow this and you don't litter the home directory.

| Purpose | Variable | Default |
|---------|----------|---------|
| Config | `$XDG_CONFIG_HOME` | `~/.config` |
| Data | `$XDG_DATA_HOME` | `~/.local/share` |
| Cache | `$XDG_CACHE_HOME` | `~/.cache` |
| Runtime (sockets, pipes) | `$XDG_RUNTIME_DIR` | `/run/user/$UID` |
| State (logs, history) | `$XDG_STATE_HOME` | `~/.local/state` |

Always respect the env var, fall back to the default:
```bash
config_dir="${XDG_CONFIG_HOME:-$HOME/.config}/yourapp"
```

---

## Filesystem Hierarchy Standard (FHS)

Where things belong on the system:

| Path | Purpose |
|------|---------|
| `/etc` | System-wide config |
| `/usr/bin` | System binaries |
| `/usr/local/bin` | Locally installed binaries |
| `~/.local/bin` | Per-user binaries |
| `/var/log` | System logs |
| `/var/lib` | Persistent application data (system-wide) |
| `/tmp` | Temporary files, cleared on reboot |
| `/run` | Runtime data, cleared on reboot |

Don't put user-installed tools in `/usr/bin`. Use `/usr/local/bin` or `~/.local/bin`.

---

## File Permissions — What the Numbers Actually Mean

`rwxrwxrwx` = owner / group / other

| Octal | Meaning |
|-------|---------|
| 644 | Owner reads+writes, everyone else reads — config files |
| 755 | Owner reads+writes+executes, everyone else reads+executes — scripts, dirs |
| 600 | Owner reads+writes only — private keys, secrets |
| 700 | Owner only, all permissions — private directories |
| 777 | Everyone everything — almost never correct |

SSH private keys must be 600 or SSH will refuse to use them.

---

## systemd Service Essentials

Minimal service unit:

```ini
[Unit]
Description=My Service
After=network.target

[Service]
Type=simple
User=myuser
WorkingDirectory=/home/myuser/myapp
ExecStart=/usr/bin/python3 /home/myuser/myapp/main.py
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Key decisions:
- `Type=simple` — process runs in foreground (most common)
- `Type=forking` — process daemonizes itself (legacy, avoid)
- `Type=notify` — process signals systemd when ready (use for servers that need time to start)
- `Restart=on-failure` — restarts only on crash, not on clean exit
- `Restart=always` — restarts on everything including clean exit

Commands:
```bash
systemctl enable myservice     # start on boot
systemctl start myservice      # start now
systemctl status myservice     # check status
journalctl -u myservice -f     # tail logs
```

---

## What Gets Overlooked

- **ulimits** — default open file limits (1024) will bite you running databases or high-connection servers. Set `LimitNOFILE=65536` in your systemd unit.
- **Environment files** — never hardcode secrets in systemd units. Use `EnvironmentFile=/etc/myapp/env` and restrict permissions on that file (640, owned by root:myuser).
- **Sticky bit on /tmp** — `/tmp` has the sticky bit set (1777). Files in /tmp can only be deleted by their owner even though the directory is world-writable. Don't rely on /tmp for sensitive intermediate files.
- **`/proc` and `/sys`** — virtual filesystems, not real files. Reading them is how you inspect kernel state. Writing to them (with care) changes kernel parameters at runtime.
- **inotify limits** — tools that watch many files (webpack, VSCode, etc.) hit `inotify` limits. Fix with `echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf`.
