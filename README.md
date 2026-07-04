# 🥥 MKS SCADA — Sistem Monitoring Mesin Kupas Sabut Kelapa

> **PT Riau Sakti United Plantations (PT RSUP)**  
> Platform: Haiwell Cloud SCADA | Protokol: Modbus TCP | Resolusi HMI: 1024×600

---

## 📋 Deskripsi

Sistem monitoring dan kontrol terpadu untuk **5 jalur Mesin Kupas Sabut (MKS)** di fasilitas pengolahan kelapa PT RSUP. Sistem ini dibangun di atas platform **Haiwell Cloud SCADA** dan menggabungkan kontrol PLC, AI Vision Counter berbasis Raspberry Pi, serta komunikasi Modbus TCP secara real-time.

---

## 🏗️ Arsitektur Sistem

```
Kelapa Masuk
     ↓
Conveyor Utama (Sensor Proximity X5)
     ↓
┌─────────────────────────────┐
│   Distribusi 5 Jalur Mesin  │
│   M1 | M2 | M3 | M4 | M5   │
└─────────────────────────────┘
     ↓
Raspberry Pi (per mesin)
  → AI Vision Counter (kamera)
  → Modbus TCP → SCADA
     ↓
PLC → Modbus TCP → SCADA
     ↓
Haiwell Cloud SCADA (HMI)
```

---

## ⚙️ Komponen Utama

### Hardware
| Komponen | Keterangan |
|----------|------------|
| Conveyor Utama | Jalur input kelapa dengan sensor proximity X5 |
| Mesin Kupas Sabut (M1–M5) | Motor conveyor, pneumatic gate, zona penampungan |
| Raspberry Pi (×5) | AI Vision Camera — hitung biji kelapa per mesin |
| PLC | Kontrol aktuator conveyor & gate pneumatic |

### Software & Protokol
| Item | Detail |
|------|--------|
| Platform SCADA | Haiwell Cloud SCADA |
| Protokol | Modbus TCP (PLC ↔ SCADA, RPi ↔ SCADA) |
| IP RPi | 192.168.12.41 – 192.168.12.45 |
| Kamera Preview | Web HTML terintegrasi ke SCADA |

---

## 🖥️ Daftar Screen

| Screen | Fungsi | Status |
|--------|--------|--------|
| **Overview** | Status seluruh sistem, animasi conveyor, counter per mesin |✅ Selesai|
| **Global Manual** | Kontrol gate pneumatic per mesin + timer | ✅ Selesai |
| **Global Diagnostic** | Status komunikasi RPi (ONLINE/DELAY/OFFLINE) + timestamp | ✅ Selesai |
| **Maintenance Management** | Lock/unlock mesin untuk perbaikan/pembersihan | ✅ Selesai |
| **Emergency Stop** | Auto-tampil saat E-Stop fisik ditekan, shutdown total | ✅ Selesai |
| **Detail M1–M5** | Monitoring spesifik per mesin | ✅ Selesai |

---

## 📊 Variabel Sistem

Total **60 internal variable** yang mencakup:

| Kelompok | Jumlah |
|----------|--------|
| Global System | 5 |
| Mode Mesin (AUTO/MAN) | 5 |
| Gate Status | 5 |
| Conveyor Status | 5 |
| Counter Biji Kelapa | 5 |
| Kapasitas Max Zona | 5 |
| Maintenance Lock | 5 |
| Communication Status | 5 |
| Timer Setting | 5 |
| Timer Elapsed | 5 |
| Seconds Since Update | 5 |
| Last Update Time | 5 |
| Last Update Display | 5 |

> ⚠️ Saat ini semua variable bersifat **Internal** (mode simulasi desain). Akan diremap ke **External Variable** saat device fisik terhubung.

---

## 🔧 Catatan Teknis

- **Script `lastUpdate`** berjalan tiap 1 detik via Script Task — menghitung selisih waktu sejak heartbeat terakhir RPi dan memformat output `"HH:MM:SS (Xs lalu)"`
- **Threshold komunikasi:**
  - `DELAY` jika tidak ada heartbeat > 15 detik
  - `OFFLINE` jika tidak ada heartbeat > 60 detik
- **Emergency Stop** memicu shutdown total: semua motor conveyor berhenti, semua gate terkunci
- **Maintenance Lock** mencegah aktuasi gate saat mesin dalam mode perbaikan

---

## 📦 Status Pengembangan

| Komponen | Status |
|----------|--------|
| Variable Internal (60 tag) | ✅ Selesai |
| Screen Overview | ✅ Selesai |
| Screen Global Manual | ✅ Selesai |
| Screen Global Diagnostic | ✅ Selesai|
| Screen Maintenance | ✅ Selesai |
| Screen Emergency Stop | ✅ Selesai|
| Screen Detail M1–M5 | ✅ Selesai |
| Koneksi device fisik (PLC + RPi) | ⏳ Tahap desain dummy |

---

## 🏢 Tentang Project

**Klien:** PT Riau Sakti United Plantations (PT RSUP)  
**Departemen:** RMR / IT Department  
**Platform SCADA:** Haiwell Cloud  
**Tahun:** 2026
