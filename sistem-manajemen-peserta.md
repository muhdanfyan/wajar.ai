# WAJAR.AI — Sistem Manajemen Peserta & Alur Belajar

---

## 🎯 VISI SISTEM

Setiap peserta punya **progress belajar terpisah**, tercatat rapi, dan Aiman bisa menyesuaikan pelayanan berdasarkan role, kelas, dan histori pembayaran.

---

## 📋 DAFTAR ROLE PENGGUNA

| Role | Akses | Contoh |
|------|-------|--------|
| **Tamu (Guest)** | Gratis 8.000 kata, belum registrasi | Orang baru chat |
| **Santri Aktif** | Sudah daftar, akses sesuai paket | Pelajar, mahasiswa |
| **Premium** | Sudah bayar, akses penuh sesuai durasi | User berbayar |
| **VIP / Tutor** | Kolaborator, pembuat konten | Ustadz, mentor |

---

## 🔄 ALUR LENGKAP PENGGUNA

### FASE 1: DAFTAR (Registrasi)

```
User chat "Mau belajar" / "Daftar"
         ↓
Aiman: "Asik! Siapa nama kamu? Mau belajar apa?"
         ↓
User: [nama, umur, minat]
         ↓
Aiman catat ke database (aiman_chat.db):
  - tb_kontak: nama, nomor, kategori = "santri_wajar"
  - tb_interview: minat, umur, tujuan
         ↓
Aiman: "Sip! Kamu dapet 8.000 kata GRATIS.
        Mau mulai dari mana?"
```

### FASE 2: PILIH KELAS / KATEGORI BELAJAR

Kategori belajar yang tersedia:

**📚 AKADEMIK**
- Matematika (SD/SMP/SMA)
- Fisika, Kimia, Biologi
- Bahasa Inggris, Bahasa Arab
- Sejarah, Geografi

**💻 IT & TEKNOLOGI**
- Coding Dasar (Python, HTML/CSS, JavaScript)
- Web Development
- Aplikasi & Tools AI

**🕌 AGAMA**
- Ngaji Al-Qur'an (Tahsin, Tahfidz)
- Fiqih, Aqidah
- Kisah Nabi & Sejarah Islam

**🎨 KREATIF**
- Desain Grafis (Canva, Figma)
- Konten Kreator
- Menulis & Copywriting

### FASE 3: MULAI BELAJAR (Akses Gratis)

```
User pilih kategori → Aiman catat di progress
         ↓
Aiman kasih materi pertama sesuai kategori
         ↓
User belajar, tanya jawab dengan Aiman
         ↓
Aiman catat:
  - Topik yang dibahas
  - Level pemahaman user
  - Progress harian
```

### FASE 4: HABIS GRATIS → BAYAR

```
Sisa kata < 500 → Aiman ingetin:
  "Jatah gratis tinggal sedikit. 
   Mau lanjut? Rp1.000/jam aja."
         ↓
User: "Mau bayar"
         ↓
Aiman kirim QRIS + kode unik
         ↓
User transfer → kirim bukti
         ↓
Aiman verifikasi → aktivasi premium
         ↓
Aiman kirim: "Aktivasi berhasil! 
  Kamu dapet akses 4 jam (kode: WAJAR-1732).
  Sisa waktu akan Aiman catat."
```

### FASE 5: SELAMA MENIKMATI LAYANAN

```
Setiap kali user chat:
  - Aiman cek status (premium/sisa waktu)
  - Catat topik diskusi
  - Update progress
  - Kalau sisa waktu < 10% → ingetin
         ↓
User selesai sesi → Aiman catat:
  - Berapa kata terpakai
  - Durasi terpakai
  - Topik apa yang dibahas
  - Level pemahaman terbaru
```

### FASE 6: SURVEI KEPUASAN

Survey dikirim otomatis setelah:
1. ✅ Selesai masa gratis (8.000 kata habis)
2. ✅ Selesai sesi premium (waktu habis)
3. ✅ Setiap 1 minggu sekali untuk pengguna aktif
4. ✅ Setelah pembelian pertama

**Pertanyaan Survey:**
```
1. 1-10, seberapa puas dengan WAJAR.AI?
2. Apa yang paling kamu suka?
3. Apa yang perlu diperbaiki?
4. Ada topik baru yang mau dipelajari?
5. Rekomendasi WAJAR.AI ke teman? (Ya/Tidak)
```

---

## 🗄️ STRUKTUR DATABASE

### Tabel Baru: tb_progress_belajar

| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id_progress | INTEGER PK | Auto increment |
| nomor_user | TEXT | Nomor WA user |
| nama_user | TEXT | Nama |
| kategori | TEXT | Kelas yang dipilih |
| topik_aktif | TEXT | Topik yang sedang dibahas |
| total_kata | INTEGER | Total kata pernah dipakai |
| total_durasi_menit | INTEGER | Total waktu belajar |
| level | TEXT | Pemula/Menengah/Lanjut |
| status | TEXT | Gratis/Premium/Expired |
| sisa_waktu_menit | INTEGER | Sisa waktu premium |
| kode_unik | TEXT | Kode transaksi aktif |
| terdaftar_at | DATETIME | Saat daftar |
| terakhir_belajar | DATETIME | Terakhir chat |
| survey_terakhir | DATETIME | Terakhir isi survey |

### Tabel Baru: tb_log_belajar

| Kolom | Tipe | Keterangan |
|-------|------|------------|
| id_log | INTEGER PK | Auto increment |
| nomor_user | TEXT | Nomor WA |
| sesi_ke | INTEGER | Sesi ke berapa |
| topik | TEXT | Topik yang dibahas |
| kata_digunakan | INTEGER | Berapa kata |
| durasi_menit | INTEGER | Lama sesi |
| rating | INTEGER | 1-5 (dari survey) |
| catatan | TEXT | Catatan Aiman |
| waktu | DATETIME | Waktu sesi |

---

## 📊 VISUALISASI PROGRESS YANG BISA DIBUAT

**Untuk User:**
- "Kamu sudah belajar X topik, Y jam, Z kata"
- "Topik favorit kamu: Matematika"
- "Level kamu: Pemula → Menengah"

**Untuk Bang Dadan:**
- Total user aktif
- Total pemasukan
- Topik paling populer
- Rating kepuasan rata-rata
- User yang hampir expired

---

## 🎯 PRIORITAS IMPLEMENTASI

**Minggu 1 (Sekarang):**
1. Sistem registrasi sederhana (nama + kategori via chat)
2. Catat progress ke SQLite (tb_progress_belajar + tb_log_belajar)

**Minggu 2:**
1. Survey otomatis setelah sesi
2. Reminder otomatis ketika hampir expired

**Minggu 3:**
1. Dashboard progress (via chat — Aiman bisa kasih laporan)
2. Integrasi n8n untuk notifikasi Bang Dadan

---

## 📝 CATATAN UNTUK AIMAN

Setiap kali user chat, WAJIB:
1. Cek nomor di tb_progress_belajar
2. Kalau ada → update `terakhir_belajar` + `total_kata`
3. Kalau tidak ada → tanya nama & kategori → insert baru
4. Kalau user selesai ngobrol → insert tb_log_belajar

Ini memastikan:
- ✅ Setiap user punya progress terpisah
- ✅ Aiman tahu level & topik masing-masing
- ✅ Bang Dadan bisa lihat statistik
- ✅ Survey bisa dikirim tepat waktu
