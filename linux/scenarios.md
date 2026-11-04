## Saint John: runaway log writer

- **Problem:** Something was constantly writing to `/var/log/bad.log`.
- **What I checked:** Watched the log with `tail -f`, then used `lsof` to see which process had it open.
- **What I found:** `badlog.py` (PID 589, user `admin`) had the file open for writing (`3w`).
- **Root cause:** A running process was writing to the log every 0.3 seconds or so.
- **Fix:** Stopped it with `kill 589`, then confirmed it was gone with `ps -p 589`.
- **What I learned:** `lsof` connects a file to the process using it. In production, I'd check what started the process and why before killing it, in case it restarts or matters.

## Saskatoon: top IP in a log

- **Problem:** Find the IP with the most requests in `access.log`.
- **What I checked:** Used `head` to find the IP column, then counted requests per IP.
- **What I found:** `66.249.73.135` had the most, with 482 requests.
- **Fix:** Saved the top IP to `highestip.txt` using `awk`, `sort`, `uniq -c`, `sort -nr` and `head -1`.
- **What I learned:** Build a pipeline one step at a time. The output of `uniq -c` adds a column, so the IP moves from `$1` to `$2`.

