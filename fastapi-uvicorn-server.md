# Same like Gunicorn you can setup Gunicorn

---
### Ensure Dependencies Are Installed via `uv`
```bash
cd ~/fastapi-app
uv venv
uv pip install fastapi "uvicorn[standard]"
```
NOTE: (If you use a `pyproject.toml` file, run `uv add fastapi "uvicorn[standard]"` instead.)

---
- `/etc/systemd/system/fastapi.service`
- Notice the `.venv` path, the `--uds` flag (no `unix:` prefix), and `--proxy-headers` so FastAPI trusts traffic forwarded by `Nginx`
```bash
[Unit]
Description=FastAPI application managed by Uvicorn
After=network.target

[Service]
User=your_user
Group=www-data
WorkingDirectory=/home/your_user/fastapi-app
Environment="PATH=/home/your_user/fastapi-app/.venv/bin"

# Systemd automatically creates /run/fastapi owned by your_user:www-data
RuntimeDirectory=fastapi
RuntimeDirectoryMode=0755
UMask=0007

ExecStart=/home/your_user/fastapi-app/.venv/bin/uvicorn main:app \
    --workers 4 \
    --uds /run/fastapi/fastapi.sock \
    --proxy-headers \
    --forwarded-allow-ips="*"

Restart=always
RestartSec=5
KillSignal=SIGTERM
Type=simple
StandardOutput=journal
StandardError=journal
SyslogIdentifier=fastapi-app

[Install]
WantedBy=multi-user.target
```

> **Why `UMask=0007` and `KillSignal=SIGTERM` matter:**
> * `UMask=0007` ensures the created `.sock` file gives read/write permissions to the `www-data` group so Nginx doesn't return a `502 Bad Gateway (Permission Denied)` error.
> * Uvicorn uses `SIGTERM` (or `SIGINT`) for graceful shutdown, whereas `SIGQUIT` is specific to Gunicorn.
> 
> 

---

## Apply and Verify Socket Creation

Reload systemd, restart the service, and verify that `/run/fastapi/fastapi.sock` exists:

```bash
sudo systemctl daemon-reload
sudo systemctl restart fastapi
ls -l /run/fastapi/fastapi.sock

```
If the socket is created properly, you will see output similar to `srwxrwx--- 1 your_user www-data 0 ... /run/fastapi/fastapi.sock`.

---
## BONUS: `sudo journalctl -fu fastapi.service`
