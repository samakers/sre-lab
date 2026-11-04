## Saint John: runaway log writer

- **Problem:** Something was constantly writing to `/var/log/bad.log`.
- **What I checked:** Watched the log with `tail -f`, then used `lsof` to see which process had it open.
- **What I found:** `badlog.py` (PID 589, user `admin`) had the file open for writing (`3w`).
- **Root cause:** A running process was writing to the log every 0.3 seconds or so.
- **Fix:** Stopped it with `kill 589`, then confirmed it was gone with `ps -p 589`.
- **What I learned:** `lsof` connects a file to the process using it. In production, I'd check what started the process and why before killing it, in case it restarts or matters.

