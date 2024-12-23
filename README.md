# FINAL PROJECT OS SERVER - 23.83.0962

# Webserver Project

This project is a webserver setup using Ubuntu Server, configured with the following specifications and installed services:

## Server Specifications
- **Operating System:** Ubuntu Server
- **RAM:** 12 GB
- **Processor:** 8 Cores
- **Storage:** 50 GB

## Installed Services
1. **Apache2:** Used as a reverse proxy server.
2. **Flask:** Python-based web framework for application development.
3. **Gunicorn:** WSGI server to serve the Flask application.
4. **SSH:** Secure Shell for remote server access.

## Hosting
The webserver is hosted using **Cloudflare Tunnel** for secure and reliable access.

---

## Setup Guide

### 1. Update and Upgrade the System
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Install Apache2
```bash
sudo apt install apache2 -y
```
Enable and start the Apache2 service:
```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

### 3. Install Python and Required Modules
```bash
sudo apt install python3 python3-pip -y
```
Install Flask and Gunicorn:
```bash
pip3 install flask gunicorn
```

### 4. Configure Flask Application
Create your Flask application, e.g., `app.py`:
```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def home():
    return "Hello, World!"

if __name__ == "__main__":
    app.run()
```

### 5. Run the Flask Application with Gunicorn
Start the Gunicorn server:
```bash
gunicorn --bind 0.0.0.0:8000 app:app
```

### 6. Configure Apache2 as a Reverse Proxy
Enable required Apache modules:
```bash
sudo a2enmod proxy proxy_http
```
Edit the Apache configuration file (e.g., `/etc/apache2/sites-available/000-default.conf`):
```apache
<VirtualHost *:80>
    ServerName yourdomain.com

    ProxyPass / http://127.0.0.1:8000/
    ProxyPassReverse / http://127.0.0.1:8000/
</VirtualHost>
```
Restart Apache2:
```bash
sudo systemctl restart apache2
```

### 7. Install and Configure Cloudflare Tunnel
Follow the official Cloudflare Tunnel setup guide:
- Install Cloudflare Tunnel binary (`cloudflared`).
- Authenticate and configure your tunnel.
- Ensure your domain points to the tunnel.

---

## Usage
- Access the webserver via the configured Cloudflare Tunnel URL.
- Manage and modify the Flask application as needed in the `app.py` file.

---

## Notes
- Ensure proper security configurations for production environments.
- Regularly update your server and services to maintain security and stability.

## License
This project is open-source and available under the MIT License.

