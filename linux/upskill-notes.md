# Linux Upskill Challenge notes

## Day 1: Server health

**Server:** Hetzner cpx02, 1 vCPU, about 1 GB RAM, no swap, 19 GB disk, Ubuntu 26.04.1 LTS.

**Setup and hardening**
- Logged in as root with an SSH key, then ran `apt update && apt upgrade -y`.
- Created user `sam`, added it to `sudo`, and copied my SSH key across.
- Disabled root login and password logins in `/etc/ssh/sshd_config.d/99-hardening.conf`, checked with `sshd -t`, then restarted SSH.
- Tested a new login in a second terminal before closing the root session.
- Cloud firewall allows inbound SSH (TCP 22) and ping (ICMP) only.

**Health checks**
- `free -h`: watch `available`, not `free`. Linux uses spare RAM as cache and frees it when programs need it.
- No swap means the OOM killer stops a process if RAM runs out.
- `df -h`: check `/`. Start investigating above about 80-90%. `tmpfs` lives in RAM and is cleared on reboot.
- `uptime`: load averages are for 1, 5 and 15 minutes. Compare them with the CPU count, and check whether they're rising or falling.
- `uname -a`: kernel version and architecture (`x86_64`).
- `ls -la`: permissions are owner, group and others. `.ssh` should be `drwx------`.

**What I learned**
- Always test a new login before locking anything down, so you don't lock yourself out.
- One number on its own means little. Compare it with capacity and look at the trend.

