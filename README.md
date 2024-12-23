# FINAL PROJECT OS SERVER - 23.83.0962

# Proyek Webserver

Proyek ini adalah pengaturan webserver menggunakan Ubuntu Server, dikonfigurasi dengan spesifikasi berikut dan layanan yang diinstal:

## Spesifikasi Server
- **Sistem Operasi:** Ubuntu Server
- **RAM:** 12 GB
- **Prosesor:** 8 Core
- **Penyimpanan:** 50 GB

## Layanan yang Diinstal
1. **Apache2:** Digunakan sebagai reverse proxy server.
2. **Flask:** Framework web berbasis Python untuk pengembangan aplikasi.
3. **Gunicorn:** Server WSGI untuk melayani aplikasi Flask.
4. **SSH:** Secure Shell untuk akses server jarak jauh.
5. **Cloudflare Tunnel:** Untuk hosting yang aman dan andal.

---

## Panduan Pengaturan

### 1. Perbarui dan Tingkatkan Sistem
```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Instal Apache2
```bash
sudo apt install apache2 -y
```
Aktifkan dan mulai layanan Apache2:
```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

### 3. Instal Python dan Modul yang Diperlukan
```bash
sudo apt install python3 python3-pip -y
```
Instal Flask dan Gunicorn:
```bash
pip3 install flask gunicorn
```

### 4. Konfigurasi Aplikasi Flask
Buat aplikasi Flask Anda, misalnya `app.py`:
```python
from flask import Flask, render_template, url_for
import os

app = Flask(__name__)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/Harga')
@app.route('/Harga.html')
def harga():
    return render_template('Harga.html')

@app.route('/Internet-Rumah')  # Ubah spasi menjadi strip
@app.route('/Internet-Rumah.html')
def internet_rumah():
    return render_template('Internet-Rumah.html')

@app.route('/Kebijakan-Privasi')  # Ubah spasi menjadi strip
@app.route('/Kebijakan-Privasi.html')
def kebijakan_privasi():
    return render_template('Kebijakan-Privasi.html')

@app.route('/Layanan')
@app.route('/Layanan.html')
def layanan():
    return render_template('Layanan.html')

@app.route('/Lebih-Lanjut')  # Ubah spasi menjadi strip
@app.route('/Lebih-Lanjut.html')
def lebih_lanjut():
    return render_template('Lebih-Lanjut.html')

@app.route('/Paket-Dasar')  # Ubah spasi menjadi strip
@app.route('/Paket-Dasar.html')
def paket_dasar():
    return render_template('Paket-Dasar.html')

@app.route('/Paket-Premium')  # Ubah spasi menjadi strip
@app.route('/Paket-Premium.html') 
def paket_premium():
    return render_template('Paket-Premium.html')

@app.route('/Paket-Pro')  # Ubah spasi menjadi strip
@app.route('/Paket-Pro.html')
def paket_pro():
    return render_template('Paket-Pro.html')

@app.route('/Paket-Streaming')  # Ubah spasi menjadi strip
@app.route('/Paket-Streaming.html') 
def paket_streaming():
    return render_template('Paket-Streaming.html')

@app.route('/Solusi-Bisnis')  # Ubah spasi menjadi strip
@app.route('/Solusi-Bisnis.html')
def solusi_bisnis():
    return render_template('Solusi-Bisnis.html')

@app.route('/testimoni')
@app.route('/Testimoni.html')
def testimoni():
    return render_template('Testimoni.html')

# Tambahkan error handler
@app.errorhandler(404)
def page_not_found(e):
    return render_template('404.html'), 404

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)
```

### 5. Jalankan Aplikasi Flask dengan Gunicorn
Mulai server Gunicorn:
```bash
gunicorn --bind 127.0.0.1:8000 app:app
```

### 6. Konfigurasi Apache2 sebagai Reverse Proxy
Aktifkan modul Apache yang diperlukan:
```bash
sudo a2enmod proxy proxy_http
```
Edit file konfigurasi Apache (misalnya, `/etc/apache2/sites-available/000-default.conf`):
```apache
<VirtualHost *:80>
    ServerName rusdi.ambasigma.my.id

    ProxyPass / http://127.0.0.1:8000/
    ProxyPassReverse / http://127.0.0.1:8000/
</VirtualHost>
```
Restart Apache2:
```bash
sudo systemctl restart apache2
```

### 7. Instal dan Konfigurasi Cloudflare Tunnel
Ikuti panduan resmi untuk pengaturan Cloudflare Tunnel:
- Instal binary Cloudflare Tunnel (`cloudflared`).
- Autentikasi dan konfigurasi tunnel Anda.
- Pastikan domain Anda mengarah ke tunnel.

---

## Penggunaan
- Akses webserver melalui URL Tunnel Cloudflare yang telah dikonfigurasi.
- Kelola dan modifikasi aplikasi Flask sesuai kebutuhan di file `app.py`.

---

## Catatan
- Pastikan konfigurasi keamanan yang sesuai untuk lingkungan produksi.
- Perbarui server dan layanan Anda secara berkala untuk menjaga keamanan dan stabilitas.
