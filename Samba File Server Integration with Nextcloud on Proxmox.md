# 📁 Samba File Server Integration with Nextcloud on Proxmox

> Implementasi File Server Samba yang terintegrasi dengan Nextcloud menggunakan Proxmox VE, MariaDB, Apache2, dan Cloudflare Tunnel.

![Platform](https://img.shields.io/badge/Platform-Proxmox-orange)
![OS](https://img.shields.io/badge/OS-Debian%2013-red)
![Nextcloud](https://img.shields.io/badge/Nextcloud-v34.0.1-blue)
![MariaDB](https://img.shields.io/badge/MariaDB-11.8.6-green)
![Apache](https://img.shields.io/badge/Apache2-Web%20Server-purple)
![License](https://img.shields.io/badge/License-MIT-success)

---

# 📖 Overview

Project ini bertujuan membangun sistem penyimpanan file berbasis **Samba Server** yang terintegrasi dengan **Nextcloud** sehingga pengguna dapat mengakses file baik melalui jaringan lokal menggunakan SMB maupun melalui internet menggunakan Nextcloud.

Seluruh layanan dijalankan pada **Proxmox VE** menggunakan **LXC Container** sehingga mudah dikelola dan memiliki resource yang terpisah.

---

# 🏗️ Arsitektur Sistem

```
                Internet
                    │
                    │ HTTPS
                    ▼
           Cloudflare Tunnel
                    │
                    ▼
         ┌────────────────────┐
         │ Nextcloud CT100    │
         │ Apache + PHP       │
         │ MariaDB            │
         └─────────┬──────────┘
                   │ SMB/CIFS
                   ▼
         ┌────────────────────┐
         │ Samba Server CT101 │
         │ /srv/samba         │
         └─────────┬──────────┘
                   │
                   ▼
              File Storage
```

---

# 💻 Environment

| Komponen | Keterangan |
|----------|------------|
| Hypervisor | Proxmox VE 9.2.2 |
| Samba Server | CT101 |
| Nextcloud | CT100 |
| OS | Debian GNU/Linux 13 (Trixie) |
| PHP | 8.4.23 |
| MariaDB | 11.8.6 |
| Apache | Apache2 |
| Nextcloud | 34.0.1 |
| Tunnel | Cloudflare Tunnel |

---

# 🌐 Network

| Device | IP Address |
|---------|------------|
| Samba Server | 192.168.5.141 |
| Nextcloud | 192.168.5.142 |

---

# 📂 Folder Structure

```text
/srv/samba
│
├── Common
│   ├── Dokumen/
│   ├── Shared/
│   ├── Info-Perusahaan.txt
│   └── README.txt
│
├── Management
│   ├── Laporan/
│   ├── Rapat/
│   └── Struktur-Organisasi.txt
│
├── Personal
│   ├── arrival/
│   ├── budi/
│   ├── rini/
│   ├── siti/
│   └── wati/
│
└── Projects
    ├── ProjectA/
    └── ProjectB/
```

---

# 👥 User

| Username | Folder Personal |
|----------|-----------------|
| arrival | ✅ |
| budi | ✅ |
| rini | ✅ |
| siti | ✅ |
| wati | ✅ |

---

# 🔐 Permission

| Folder | User |
|---------|------|
| Personal | Semua User |
| Common | Semua User |
| Management | arrival |
| ProjectA | budi |
| ProjectB | rini |

---

# 🗄️ Database

Database digunakan oleh Nextcloud.

```
Database : nextcloud
Username : nextclouduser
Host     : localhost
```

---

# ☁️ Cloudflare Tunnel

```
Tunnel Name :
nextcloud-tunnel
```

Cloudflare Tunnel digunakan agar layanan Nextcloud dapat diakses melalui internet tanpa membuka port publik secara langsung.

---

# 🔄 Integrasi Nextcloud

Nextcloud menggunakan fitur **External Storage SMB/CIFS**.

Storage yang dihubungkan:

- Common
- Personal
- Management
- ProjectA
- ProjectB

---

# 📊 Activity Diagram

```
Start
   │
   ▼
User membuka Nextcloud
   │
   ▼
Cloudflare Tunnel
   │
   ▼
Nextcloud Login
   │
   ▼
Login Valid?
 ├── Tidak → Login Gagal
 │
 └── Ya
      │
      ▼
 Dashboard
      │
 Pilih Folder
      │
 Request ke Samba
      │
 Hak Akses?
 ├── Tidak → Access Denied
 │
 └── Ya
      │
 Ambil File
      │
 Tampilkan File
      │
     End
```

---

# ✅ Pengujian

Pengujian yang dilakukan:

- Verifikasi User Nextcloud
- Verifikasi External Storage
- Pengujian Hak Akses
- Pengujian Sinkronisasi File
- Pengujian Login User
- Pengujian Cloudflare Tunnel

---

# 📸 Dokumentasi

Tambahkan screenshot berikut pada folder **docs/images**

```
docs/
│
├── proxmox.png
├── samba.png
├── nextcloud-dashboard.png
├── external-storage.png
├── login.png
├── folder-common.png
├── folder-personal.png
├── permission.png
├── cloudflare.png
└── activity-diagram.png
```

---

# 🚀 Hasil Implementasi

✔ Samba Server berhasil dibuat

✔ Nextcloud berhasil diinstal

✔ MariaDB berhasil dikonfigurasi

✔ Apache berjalan normal

✔ Cloudflare Tunnel aktif

✔ External Storage SMB berhasil ditambahkan

✔ Hak akses sesuai konfigurasi

✔ Sinkronisasi file berhasil

---

# 📚 Referensi

- https://www.samba.org/
- https://nextcloud.com/
- https://pve.proxmox.com/
- https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/
- https://mariadb.org/
- https://httpd.apache.org/

---

## 👨‍💻 Author

**Arrival Sudrajat**

S1 Sistem Informasi

Telkom University

2026