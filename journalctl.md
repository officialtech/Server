
## Journalctl Gunicorn Log Retrieval Commands

| Command Type | Syntax | Description | Example |
|-------------|--------|-------------|---------|
| **From Specific Timestamp** | `journalctl -u gunicorn.service --since "YYYY-MM-DD HH:MM:SS"` | Fetch logs from a specific date and time | <b>journalctl -u gunicorn.service --since "2025-01-15 14:30:00"</b> |
| **Last N Hours** | `journalctl -u gunicorn.service --since "-Nh"` | Retrieve logs from the last N hours | <b>journalctl -u gunicorn.service --since "-2h"</b> |
| **Last N Lines** | `journalctl -u gunicorn.service -n 100` | Show last 100 log entries | <b>journalctl -u gunicorn.service -n 100</b> |
| **Follow Live Logs** | `journalctl -u gunicorn.service -f` | Continuously display new log entries | <b>journalctl -u gunicorn.service -f</b> |

<hr>

## Advanced Filtering Options

### Additional Useful Flags
- `-r` or `--reverse`: Display logs in reverse chronological order
- `--no-pager`: Output logs directly to terminal
- `-p warning`: Filter logs by priority level

### Complex Filtering Example
```bash
journalctl -u gunicorn.service --since "2025-01-01" --until "2025-01-31" -p err
```
<b>This command retrieves error-level logs for the Gunicorn service throughout January 2025</b>

<hr>



