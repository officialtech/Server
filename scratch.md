

## Install Python 3.13 + venv tooling
```bash
apt install -y software-properties-common
add-apt-repository ppa:deadsnakes/ppa
apt update
apt install -y python3.13 python3.13-venv python3.13-dev
```

- Install build deps (often needed for wheels):
```bash
apt install -y build-essential pkg-config libpq-dev libssl-dev libffi-dev zlib1g-dev
```

## If pip isn't available
- Install pip for Python 3.13
- Ubuntu sometimes doesn’t ship python3.13-pip in a convenient way; a reliable approach:
```bash
curl -sS https://bootstrap.pypa.io/get-pip.py -o /tmp/get-pip.py
python3.13 /tmp/get-pip.py
python3.13 -m pip --version
```

## Install and configure Nginx
```bash
sudo apt install -y nginx
sudo systemctl enable --now nginx
```

