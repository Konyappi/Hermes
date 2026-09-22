# Hermes
Dokumentasi/Tutorial
# Dokumentasi: Cara Install Hermes Agent

**Apa itu:** AI coding agent yang jalan di server (VPS), dikontrol lewat chat Telegram — jadi bisa coding kapan saja tanpa perlu laptop menyala.

---

## Prasyarat

- VPS dengan Ubuntu (20GB disk, 2GB RAM sudah cukup)
- Akses terminal ke VPS (SSH)
- Bot Telegram (dibuat lewat **@BotFather**, dapat bot token)
- API key model AI (misal Google Gemini via https://aistudio.google.com/apikey)

---

## Langkah Instalasi

### 1. Install dependency yang dibutuhkan
```bash
sudo apt update
sudo apt install -y libatomic1
```
*(Ini mencegah error `libatomic.so.1` saat Node.js dijalankan nanti)*

### 2. Install Hermes
```bash
curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash
source ~/.bashrc
```

### 3. Kalau command `hermes` belum dikenali
```bash
echo 'export PATH="/home/$USER/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### 4. Jalankan wizard setup
```bash
hermes setup
```
Pilih **Full setup** (bukan Quick Setup/Nous Portal) supaya bisa pasang API key sendiri.

### 5. Set model AI
Saat wizard tanya provider, pilih **Google AI Studio (Native Gemini API)**, lalu masukkan API key.
Kalau ingin ganti model/key belakangan:
```bash
hermes model
```

### 6. Hubungkan ke Telegram
```bash
hermes gateway setup
```
- Masukkan bot token dari BotFather
- Masukkan User ID Telegram sendiri (cek lewat **@userinfobot**) sebagai allowlist, supaya cuma kamu yang bisa akses bot

### 7. Jadikan permanen (jalan 24/7)
```bash
hermes gateway install
hermes gateway start
```

### 8. Tes
Buka Telegram, chat ke bot yang sudah dibuat. Kalau dia balas, instalasi berhasil.

---

## Command yang Sering Dipakai

| Command | Fungsi |
|---|---|
| `hermes` | Mulai chat langsung di terminal |
| `hermes model` | Ganti/cek model AI |
| `hermes config` | Lihat/edit konfigurasi |
| `hermes gateway restart` | Restart service setelah ubah config |
| `hermes gateway status` | Cek status service |

---

## Troubleshooting Umum

| Gejala | Solusi |
|---|---|
| `libatomic.so.1` error | `sudo apt install -y libatomic1`, install ulang |
| `hermes: command not found` | Tambahkan PATH manual (lihat langkah 3) |
| Model AI error 401 (Unauthenticated) | Cek ulang API key, pastikan formatnya benar dan tidak salah copy |
| Model AI error 429 (kuota habis) | Tunggu reset kuota harian, atau aktifkan billing di provider AI |
| Gateway "already running" | Pakai `hermes gateway restart`, jangan jalankan `hermes gateway` manual |
