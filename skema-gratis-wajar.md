# 📋 SKEMA WAJAR.AI — Gratis + Berbayar + Anti-Cheat

## 1. SIAPA DAPAT GRATIS?

**GRATIS = HANYA UNTUK TUJUAN BELAJAR yang legitimate.**

| 🟢 **Dapat Gratis** | 🔴 **Tidak Dapat Gratis** |
|:--------------------|:--------------------------|
| "Aku mau belajar Python dari dasar" | "Kerjain PR matematika aku dong" |
| "Ajarin aku bikin website" | "Buatkan essay 500 kata tentang..." |
| "Cara masak nasi goreng" | "Selesaikan tugas kuliahku" |
| "Bantu aku pahamin konsep AI" | "Tolong kerjain soal-soal ini" |
| Curhat ringan / konsultasi sehat | Copy-paste tugas sekolah langsung |
| Tanya-tanya tentang IT/Programming | "Bikinin makalah / laporan / skripsi" |

**Mekanisme screening:**
1. User kirim chat pertama
2. Aiman deteksi otomatis: apakah ini "belajar" atau "minta dikerjain"?
3. Kalau belajar → kasih gratis 2.000 kata
4. Kalau minta dikerjain → tolak halus: *"Maaf Kak, Aiman di sini untuk bantu belajar, bukan kerjain tugas. Tapi kalau mau les privat, ada paket mulai Rp500/sesi"*

## 2. BERAPA GRATIS?

**2.000 KATA — bukan 8.000.** Alasan:
- Cukup buat tes rasa: nanya 3-5x putaran chat
- Gak cukup buat nyelesain tugas besar gratis
- Kalau user serius, 2.000 kata habis dalam 5-10 menit → gak kerasa berat buat lanjut bayar

## 3. BAGI YANG CUMA MAU TANYA-TANYA / KONSULTASI RINGAN?

Ini celah kritis yang Bang Dadan maksud. Ada orang yang:
- "Cuma tanya-tanya soal IT / pondok / beasiswa"
- "Mau konsultasi karir"
- "Tanya harga produk pondok"
- "Curhat bentar"

**Solusi: SKEMA DIFFERENTIATED:**

| Tipe Chat | Jatah | Harga Setelah Jatah Habis |
|:----------|:-----:|:--------------------------|
| 📚 **Belajar Serius** (coding, akademik, skill) | 2.000 kata GRATIS | Rp500/sesi atau Rp5.000/hari |
| 🗣️ **Tanya Produk Pondok** (PPDB, digitalisasi, donasi) | ✅ GRATIS SELAMANYA — unlimited | Rp0 — ini bukan produk WAJAR |
| 🧠 **Curhat & Konsultasi** | 1.000 kata GRATIS | Rp1.000/jam |
| 💬 **Tanya-tanya ringan** (karir, rekomendasi, IT umum) | 1.000 kata GRATIS | Rp500/sesi |

**Kenapa dibedakan?**
- Produk pondok (PPDB, digitalisasi, donasi) = **GRATIS unlimited** karena itu bagian dari layanan Pondok Informatika, bukan WAJAR.AI.
- Tanya-tanya ringan = jatah kecil karena bukan belajar — kalau serius, user pasti lanjut bayar.
- Curhat = dukungan psikologis ringan, jatah kecil biar gak disalahgunakan.

## 4. ANTI-CHEAT: DETEKSI NOMOR GANDA

**Aturan: GRATIS 1x SEUMUR HIDUP per ORANG, bukan per NOMOR.**

| Skenario Cheat | Deteksi | Tindakan Aiman |
|:---------------|:--------|:---------------|
| User A habis gratis, bikin nomor baru | Nama sama, topik sama, gaya bahasa mirip | "Maaf Kak, sepertinya Kakak sudah pernah cobain WAJAR.AI. Gratis hanya 1x ya" |
| User A pake nomor istri/temen | Gaya nulis mirip, topik persis sama | Sama — tolak halus |
| User bikin 10 WA virtual number | Sulit dideteksi sendiri | 🔴 Laporkan ke pengelola — pengelola cek manual |

**Teknis:** Aiman catat di SQLite:
- tb_cache_konteks: simpan hash fingerprint (pola nulis, topik, jam aktif)
- Kalau hash mirip >70% dengan user lain → flag "potential duplicate"

## 5. FLOW LENGKAP WAJAR.AI

```
USER CHAT PERTAMA
        │
Aiman: "Assalamualaikum Kak! Aiman dari WAJAR.AI.
        Mau belajar apa hari ini?"
        │
── USER JAWAB ──────────────────────
        │
├── "Mau les coding / belajar" ───→ Deteksi: LEGIT → Gratis 2.000 kata
│                                    Aiman bantu belajar beneran
│                                    ↓ Habis → tawarin paket
│
├── "Tolong kerjain PR/tugas" ────→ Deteksi: CHEAT → Tolak halus
│                                    "Maaf Kak, Aiman untuk belajar, 
│                                     bukan ngerjain. Mau les online?
│                                     Rp500/sesi aja"
│
├── "Tanya soal pondok / PPDB" ───→ GRATIS UNLIMITED (bukan WAJAR.AI)
│                                    Aiman layani sebagai layanan pondok
│
├── "Curhat / konsultasi" ────────→ Gratis 1.000 kata
│                                    ↓ Habis → Rp1.000/jam
│
├── "Tanya-tanya ringan / karir" ──→ Gratis 1.000 kata
│                                    ↓ Habis → Rp500/sesi
│
└── "Cuma test / iseng" ──────────→ Gratis 500 kata
                                    ↓ Habis → treat sebagai umum
```

## 6. PAKET BERBAYAR (Setelah Jatah Gratis Habis)

| Paket | Harga | Cocok Untuk |
|:------|:-----:|:-----------|
| ☕ **Per Sesi** | Rp500 | Cuma nanya 1-2 soal |
| 🎯 **Per Jam** | Rp1.000 | Belajar serius 1 jam |
| 📅 **Per Hari** | Rp5.000 | Belajar full sehari |
| 📆 **Per Minggu** | Rp25.000 | Belajar rutin seminggu |
| 🌙 **Per Bulan** | Rp100.000 | Belajar tiap hari |

## 7. SUMMARY — SIAPA DAPAT APA?

| Siapa | Gratis | Bayar | Keterangan |
|:------|:------:|:-----:|:-----------|
| Calon santri PPDB | ∞ UNLIMITED | - | Layanan pondok, bukan WAJAR |
| Pondok mitra | ∞ UNLIMITED | - | Layanan pondok, bukan WAJAR |
| Donatur | ∞ UNLIMITED | - | Layanan pondok, bukan WAJAR |
| Pelajar serius | 2.000 kata | Rp500/sesi | Screening dulu |
| Curhat / konsultasi | 1.000 kata | Rp1.000/jam | Mental health support |
| Tanya-tanya ringan | 1.000 kata | Rp500/sesi | Karir / IT / rekomendasi |
| Iseng / test | 500 kata | Rp500/sesi | Anti-iseng |
| Minta ngerjain tugas | **0 kata** | Rp1.000/jam | HARUS bayar langsung |

## 8. PENGECUALIAN — Calon Klien yang Pingin Tanya-tanya Dulu

**PRODUK PONDOK = layanan yang ditawarkan Pondok Informatika, yaitu:**
1. 🏫 **Digitalisasi Pondok** — pembuatan web/aplikasi untuk pondok lain
2. 🎓 **PPPDB** — pendaftaran santri baru
3. 🤖 **WAJAR.AI** — les AI via WhatsApp (ini produknya)
4. 💰 **Donasi** — donasi untuk pondok
5. 🏠 **Program Mondok** — Boarding, Reguler, Online, After School

**YANG BUKAN PRODUK PONDOK (harus bayar):**
- ❌ Minta diajarin coding/IT untuk diri sendiri (ini WAJAR.AI)
- ❌ Minta ngerjain PR/tugas sekolah
- ❌ Konsultasi karir pribadi
- ❌ Curhat personal (ada jatah 1.000 kata)
- ❌ Tanya-tanya umum di luar produk

**ATURAN: Tanya soal PRODUK PONDOK = GRATIS UNLIMITED. Tidak dihitung jatah WAJAR.AI.**

Kenapa? Karena:
1. Ini marketing, bukan layanan belajar
2. Kalau dipotong jatah, orang malas tanya → gak jadi beli
3. Orang yang tanya produk biasanya jadi klien

**Deteksi:**
- Kalau chat berisi kata kunci produk pondok ("harga", "paket", "digitalisasi", "ppdb", "daftar mondok", "donasi", "wajar") → otomatis masuk MODE KONSULTASI PRODUK
- Jatah kata tidak berkurang selama mode ini

### ⚠️ ATURAN PENTING: TRANSISI DARI PRODUK PONDOK KE NON-PRODUK

Kalau user mulainya tanya produk pondok (GRATIS UNLIMITED), terus tiba-tiba berubah ke topik lain:

| User bilang | Kategorisasi | Aiman bertindak |
|:------------|:-------------|:----------------|
| "Ok makasih infonya. Ajarin aku Python dong" | BUKAN PRODUK PONDOK | ❌ POTONG → masuk kuota WAJAR 2.000 kata |
| "Mau tanya lagi... bikinin essay tentang lingkungan" | BUKAN PRODUK PONDOK | ❌ POTONG → bukan marketing → 0 gratis → langsung bayar |
| "Boleh minta tolong kerjain PR?" | BUKAN PRODUK PONDOK | ❌ POTONG → langsung bayar |
| "Saya jadi tertarik, kapan bisa mulai les WAJAR?" | ✅ PRODUK PONDOK (WAJAR) | 🟢 TETAP GRATIS |
| "Coba dulu dikit, ajarin aku bikin website pribadi" | BUKAN PRODUK PONDOK | ❌ POTONG → masuk kuota WAJAR 2.000 kata |
| "Berapa biaya mondok?" | ✅ PRODUK PONDOK (PPDB) | 🟢 TETAP GRATIS |
| "Gimana cara pesan aplikasi pondok?" | ✅ PRODUK PONDOK (Digitalisasi) | 🟢 TETAP GRATIS |

**Prinsip:**
- Selama masih seputar 5 PRODUK PONDOK di atas → 🟢 GRATIS UNLIMITED
- Begitu minta diajar, disuruh ngerjain, curhat personal, atau di luar produk → 🔴 POTONG, masuk kuota WAJAR masing-masing
- Kalau kuota habis → bayar sesuai paket

## 9. FLOW CUT: MOMEN TRANSISI

```
User: "Ok makasih penjelasannya. 
       Ajarin aku HTML dong"
        │
Aiman deteksi: ini BERALIH dari MARKETING ke BELAJAR
        │
Aiman: "Baik Kak! Karena Kakak mau mulai belajar,
        Aiman kasih 2.000 kata GRATIS dulu ya.
        Kalau habis, Rp500/sesi aja. 
        Mau mulai dari mana belajar HTML-nya?"
        │
Selanjutnya: hitung kuota 2.000 kata
```

## 10. ANTI PENYALAHGUNAAN GRATIS UNLIMITED MARKETING

User jahat bisa: "Tanya produk mulu biar gratis terus."

| Skenario | Deteksi | Tindakan |
|:---------|:--------|:---------|
| Chat: "Harga berapa?" "Ok. Kalo yg premium?" "Kalo cicilan?" "Kalo gratis?" — puter-puter terus | Topik cuma harga, gak pernah lanjut | Aiman: "Kak, kalau berminat, Aiman siap bantu daftar. Ada yang spesifik mau ditanyakan?" |
| Udah 20x tanya produk tapi gak pernah action | Jumlah chat >10, topik cuma marketing | Aiman: "Kalau masih bingung, konsultasi GRATIS 30 menit sama pengelola pondok, mau?" |
| Pura-pura tanya produk padahal cuma gratis chatting | Gak ada satunya pertanyaan produk yang genuine | Aiman cut: masuk kuota 2.000 |

---

**Versi: 1.1 | 14 Mei 2026 — Tambahan aturan transisi marketing→belajar**
