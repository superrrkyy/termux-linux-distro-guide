# Termux Linux Distro Guide

Panduan lengkap menggunakan **Termux** di Android untuk menginstal dan menjalankan berbagai distribusi Linux (Ubuntu, Fedora, Debian, Arch, Kali, Alpine, dan lainnya) dengan **proot-distro**. Semua dijelaskan langkah demi langkah agar mudah diikuti bahkan oleh pemula.

---

## 📋 Daftar Isi

- [Apa itu Termux?](#-apa-itu-termux)
- [Apa itu Proot-Distro?](#-apa-itu-proot-distro)
- [Prasyarat](#-prasyarat)
- [Instalasi Termux](#-instalasi-termux)
- [Update & Upgrade Paket Termux](#-update--upgrade-paket-termux)
- [Instalasi Proot-Distro](#-instalasi-proot-distro)
- [Daftar Distro yang Didukung](#-daftar-distro-yang-didukung)
- [Cara Instal Distro](#-cara-instal-distro)
  - [Ubuntu](#ubuntu)
  - [Fedora](#fedora)
  - [Debian](#debian)
  - [Arch Linux](#arch-linux)
  - [Kali Linux](#kali-linux)
  - [Alpine](#alpine)
- [Cara Login ke Distro](#-cara-login-ke-distro)
- [Perintah Dasar di Dalam Distro](#-perintah-dasar-di-dalam-distro)
- [Manajemen Distro](#-manajemen-distro)
  - [Backup](#backup)
  - [Restore](#restore)
  - [Menghapus Distro](#menghapus-distro)
- [Troubleshooting](#-troubleshooting)
- [Tips & Trik](#-tips--trik)
- [Lisensi](#-lisensi)

---

## 🧠 Apa itu Termux?

**Termux** adalah aplikasi terminal emulator untuk Android yang menyediakan lingkungan Linux yang cukup lengkap. Dengan Termux, kamu bisa menjalankan perintah Linux, menginstal paket, menulis skrip, bahkan menjalankan distribusi Linux penuh tanpa perlu me-root perangkat Android.

> **Catatan Penting:**  
> Selalu unduh Termux dari **F-Droid**, bukan dari Google Play Store. Versi Play Store sudah usang dan banyak paket yang tidak kompatibel.

---

## 🧩 Apa itu Proot-Distro?

**Proot-Distro** adalah skrip yang memanfaatkan `proot` untuk menginstal dan menjalankan distribusi Linux di dalam Termux. Dengan proot-distro, kamu bisa memiliki lingkungan Linux yang terisolasi (rootfs) tanpa memerlukan akses root pada Android.

---

## 📌 Prasyarat

Sebelum memulai, pastikan:

- Perangkat Android dengan versi **7.0 (Nougat)** ke atas (disarankan Android 9+).
- Koneksi internet stabil.
- Termux terinstal dari **F-Droid** (bukan Play Store).
- Penyimpanan cukup (minimal 2 GB, tergantung distro yang diinstal).

---

## 📲 Instalasi Termux

1. Unduh dan instal aplikasi **F-Droid** dari [f-droid.org](https://f-droid.org).
2. Buka F-Droid, cari **Termux**, lalu ketuk **Install**.
3. Setelah selesai, buka Termux. Berikan izin penyimpanan bila diminta dengan perintah:
   ```bash
   termux-setup-storage
```

---

🔄 Update & Upgrade Paket Termux

Sebelum menginstal apa pun, perbarui dulu daftar paket dan paket yang ada:

```bash
pkg update && pkg upgrade -y
```

Kemudian instal paket-paket dasar yang diperlukan:

```bash
pkg install git wget curl proot -y
```

---

⚙️ Instalasi Proot-Distro

Instal proot-distro dengan perintah:

```bash
pkg install proot-distro -y
```

Verifikasi instalasi:

```bash
proot-distro --version
```

---

📃 Daftar Distro yang Didukung

Untuk melihat daftar distro yang tersedia, jalankan:

```bash
proot-distro list
```

Contoh output:

```
alpine
archlinux
debian
fedora
kali
nethunter
ubuntu
void
```

---

🚀 Cara Instal Distro

Format perintah instalasi:

```bash
proot-distro install <nama-distro>
```

Ubuntu

```bash
proot-distro install ubuntu
```

Fedora

```bash
proot-distro install fedora
```

Debian

```bash
proot-distro install debian
```

Arch Linux

```bash
proot-distro install archlinux
```

Kali Linux

```bash
proot-distro install kali
```

Alpine

```bash
proot-distro install alpine
```

Proses instalasi akan mengunduh rootfs dari internet. Waktu yang dibutuhkan tergantung kecepatan internet dan ukuran distro.

---

🔑 Cara Login ke Distro

Setelah distro terinstal, kamu bisa masuk (login) ke dalamnya dengan perintah:

```bash
proot-distro login <nama-distro>
```

Contoh:

```bash
proot-distro login ubuntu
```

Setelah itu, prompt akan berubah menjadi prompt distro tersebut (misalnya root@localhost:~# untuk Ubuntu). Kamu sekarang berada di dalam lingkungan Linux virtual dan bisa menjalankan perintah Linux seperti biasa.

Catatan:
Secara default, kamu login sebagai root. Tidak perlu sudo kecuali kamu membuat user baru.

---

🛠️ Perintah Dasar di Dalam Distro

Setelah login, kamu bisa mengelola sistem seperti di Linux biasa.

Update & Upgrade Paket

Ubuntu / Debian

```bash
apt update && apt upgrade -y
```

Fedora

```bash
dnf update -y
```

Arch Linux

```bash
pacman -Syu
```

Alpine

```bash
apk update && apk upgrade
```

Instal Paket Baru

Ubuntu / Debian

```bash
apt install nama-paket
```

Fedora

```bash
dnf install nama-paket
```

Arch Linux

```bash
pacman -S nama-paket
```

Alpine

```bash
apk add nama-paket
```

---

🧰 Manajemen Distro

Backup

Untuk mencadangkan distro beserta semua isinya:

```bash
proot-distro backup <nama-distro> --output <nama-file>.tar.gz
```

Contoh:

```bash
proot-distro backup ubuntu --output ubuntu-backup.tar.gz
```

File backup akan tersimpan di direktori aktif Termux.

Restore

Untuk mengembalikan dari file backup:

```bash
proot-distro restore <nama-file>.tar.gz
```

Contoh:

```bash
proot-distro restore ubuntu-backup.tar.gz
```

Menghapus Distro

Untuk menghapus distro dan semua datanya:

```bash
proot-distro remove <nama-distro>
```

Contoh:

```bash
proot-distro remove fedora
```

---

🔧 Troubleshooting

1. Termux tidak bisa mengakses penyimpanan

Jalankan:

```bash
termux-setup-storage
```

2. Repository Termux tidak ditemukan atau paket gagal diunduh

Pastikan Termux terinstal dari F-Droid, bukan dari Play Store. Jika masih bermasalah, jalankan:

```bash
pkg update
```

3. Proot-distro gagal mengunduh rootfs

Kemungkinan masalah koneksi atau server. Coba lagi, atau gunakan mirror alternatif:

```bash
proot-distro install <nama-distro> --override-alias <nama-distro>-oldstable
```

4. Perintah sudo tidak ditemukan di dalam distro

Secara default kamu sudah menjadi root, jadi tidak perlu sudo. Namun jika ingin menginstalnya:

```bash
apt install sudo
```

5. Distro terasa lambat

Matikan aplikasi lain yang berjalan di Android, atau gunakan perangkat dengan RAM lebih besar. Proot memang lebih lambat dibandingkan native.

---

💡 Tips & Trik

· Ganti mirror repository di dalam distro agar unduhan lebih cepat, terutama untuk Ubuntu/Debian.
· Buat user non-root jika ingin lebih aman, lalu gunakan sudo.
· Gunakan tmux di dalam distro untuk multitasking terminal.
· Instal desktop environment jika ingin GUI (misal XFCE) dan akses via VNC.

---

📄 Lisensi

Repository ini bebas digunakan untuk pembelajaran dan pengembangan. Silakan modifikasi dan bagikan.

---

🤝 Kontribusi

Jika menemukan kesalahan atau ingin menambahkan informasi, silakan buat pull request atau issue di repository ini.

```

---