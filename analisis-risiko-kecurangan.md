# WAJAR.AI — Analisis Risiko, Kecurangan & Mitigasi Sistem

---

## 🔴 BAGIAN 1: SKENARIO KECURANGAN USER NAKAL

### 1.1 BERBAGI AKUN (Account Sharing)

**Skenario:** 
User A bayar Rp1.000 (1 jam). Lalu user A forward nomor WA Aiman ke temen-temennya. 10 orang chat Aiman dalam 1 jam — semuanya ngaku "saya user A" atau bikin akun baru.

**Mitigasi:**
- ✅ Setiap nomor WA = 1 akun. Aiman detek dari nomor pengirim.
- ✅ Kalau ada 10 orang chat dari 10 nomor beda dalam 1 jam, Aiman tau itu 10 user beda.
- ⚠️ **Masih celah:** User A bisa forward kontak Aiman ke 10 temen. Masing-masing dapet 8.000 kata gratis. Aman sih — itu memang jatah gratis tiap orang. Yang bahaya kalau mereka pake nomor beda tapi klaim "saya user A, udah bayar".
- ✅ **Solusi:** Kode unik transaksi terkait dengan nomor WA. User B that claims "saya sudah bayar dengan kode WAJAR-1732" → Aiman cek: kode WAJAR-1732 terdaftar atas nomor A → tolak.

### 1.2 PERPANJANG MANUAL (Waktu Tidak Habis)

**Skenario:**
User bayar Rp4.000 (4 jam). Pas jam ke-3, 30 menit user gak chat. Terus chat lagi jam ke-5 (seharusnya udah expired). User ngaku "masih ada sisa 1 jam kan? Saya kemarin cuma pake 3 jam."

**Mitigasi:**
- ✅ Timer aktif-only: waktu premium jalan cuma pas chat aktif (diam >15 menit = pause).
- ✅ Aiman catat real usage: "Kemarin chat 3 x 20 menit = 60 menit. Sisa 3 jam."
- ✅ Tidak ada "saya rasa masih ada" — semua tercatat objektif.

### 1.3 BUKTI TRANSFER PALSU

**Skenario:**
User edit screenshot bukti transfer. Misal transfer Rp1.000 di-edit jadi Rp150.000. Kirim ke Aiman: "Udah transfer Rp150rb, aktivasi 1 bulan."

**Mitigasi:**
- ❌ **CELAH:** Aiman di WA cuma bisa lihat gambar. Tidak bisa ngecek saldo real-time.
- ⚠️ **Sementara:** Aiman cek format & metadata gambar. Tapi screenshot editan susah dideteksi dari WA.
- 🔴 **Terbaik:** Kalau nominal besar (>Rp50rb), Aiman pending aktivasi sampai Bang Dadan cek manual di mutasi rekening.

**Keputusan:**
- Rp1.000 — Rp10.000: Risiko rendah, Aiman bisa langsung aktivasi
- Rp50.000 — Rp150.000: Perlu verifikasi manual Bang Dadan (cek mutasi)

### 1.4 REFUND / CHARGEBACK

**Skenario:**
User transfer Rp150rb, aktivasi 1 bulan. Hari ke-20 user minta refund: "Saya cuma pake 5 hari, kembalikan sisa 25 hari."

**Mitigasi:**
- ✅ Aturan dari awal: **PREMIUM TIDAK REFUNDABLE.** Aiman sampaikan sebelum aktivasi.
- ✅ Catat di log: "User X telah menyetujui syarat non-refund."
- ⚠️ **Bang Dadan bisa kasih kebijakan khusus** kalau user komplain keras — tapi itu keputusan Bang.

### 1.5 GRATIS BERKELANJUTAN (Buat Akun Baru Terus)

**Skenario:**
User habis 8.000 kata gratis. User beli SIM card baru, daftar lagi dari nomor baru, dapet gratis 8.000 kata lagi. Diulang-ulang.

**Mitigasi:**
- ✅ Aiman bisa deteksi nama yang sama dengan nomor beda: "Kak Andi dari nomor 0812xxx vs Kak Andi dari 0852xxx".
- ⚠️ Kalau user bedain nama tiap nomor, susah dilacak.
- 🔴 **Solusi lebih kuat (nanti):** Sandekan nomor berdasarkan nama perangkat / ID device (tapi WA API terbatas).

### 1.6 SPAM / ABUSE AIMAN

**Skenario:**
User iseng chat "coba jawab 1+1" trus "coba 2+2" trus "coba 3+3" — 100 pertanyaan receh buat ngabisin jatah kata atau ganggu.

**Mitigasi:**
- ✅ Aiman bedakan "belajar serius" vs "iseng". Kalau pola chat mencurigakan (banyak pertanyaan receh beruntun tanpa konteks), Aiman respon: "Ada yang bisa Aiman bantu serius?"
- ✅ Batas Wajar: Kalau dalam 5 menit user kirim >20 pesan receh, Aiman slow down: "Kak, coba ceritain dulu mau belajar apa?"
- ✅ Catat di log: pola spam tiap user.

---

## 🟡 BAGIAN 2: KEGAGALAN SISTEM & MITIGASI

### 2.1 DEEPSEEK DOWN / ERROR

**Skenario:** API DeepSeek error 500 atau timeout. Aiman gak bisa jawab.

**Mitigasi:**
- ✅ **Fallback ke OpenRouter** — Aiman punya 2 provider (sk-1721... & sk-or-v1-...)
- ✅ Kalau dua-duanya down → Aiman kirim ke user: "Maaf, sistem sedang perbaikan. Coba chat lagi 10 menit ya."
- ✅ Catat error + notifikasi ke Bang Dadan.

### 2.2 VPS MATI / RESTART

**Skenario:** VPS 103.150.196.183 restart. Aiman offline 5-10 menit.

**Mitigasi:**
- ✅ Aiman jalan di OpenClaw — auto-restart.
- ⚠️ **Celah:** Selama VPS restart, semua chat WA gak kejawab. 
- 🔴 **Solusi sementara:** User yang chat pas Aiman offline bisa dapet auto-reply dari WA Business API? (Tidak, karena Aiman pake OpenClaw, bukan WA Business API).

### 2.3 DATABASE CORRUPT / HABIS

**Skenario:** SQLite `aiman_chat.db` corrupt (size 0 atau write error).

**Mitigasi:**
- ✅ Backup harian jam 03:00 ke Google Drive.
- ✅ Backup ke 3 lokasi: VPS + Google Drive + rclone.
- ✅ Kalau corrupt → restore dari backup terakhir (max kehilangan 1 hari data).

### 2.4 N8N DOWN

**Skenario:** Container n8n restart atau error.

**Mitigasi:**
- ✅ `restart: unless-stopped` — auto-restart.
- ⚠️ Webhook aiman-payment & aiman-chat gak aktif selama n8n mati.
- ✅ Catat di log Aiman — "n8n webhook error" → Aiman retry manual nanti.

### 2.5 QRIS TIDAK TERBACA

**Skenario:** QRIS di landing page corrupt, atau file `qris.png` gak ke-deploy.

**Mitigasi:**
- ✅ Aiman cek tiap deploy: `ls -la qris.png` di Vercel build.
- ✅ Kalau di web rusak → Aiman kirim QRIS langsung via chat WA.
- ✅ Backup QRIS: landing page + WA chat + Drive.

### 2.6 KODE UNIK BENTROK

**Skenario:** 2 user dapet kode WAJAR-1732 di waktu bersamaan.

**Mitigasi:**
- ✅ Format: `WAJAR-XXXX` (4 digit random: 0000-9999). Probabilitas bentrok: 1/10.000.
- ✅ Aiman generate kode baru kalau sudah ada di database.
- ✅ Tambah timestamp di kode: `WAJAR-1732-1415` (kode + jam:menit) — virtually zero collision.

### 2.7 USER CHAT PAS TENGAH MALAM

**Skenario:** User chat jam 02:00 WIB. Aiman respon — wajar. Tapi Bang Dadan kena notifikasi jam 02:00.

**Mitigasi:**
- ✅ Notifikasi urgent (komplain, pembayaran besar) tetap terkirim ke Bang Dadan.
- ✅ Chat biasa (belajar, tanya) — tidak perlu notifikasi Bang Dadan.
- ✅ Auto-reply di luar jam Bang bangun: "Halo! Aiman tetap online 24 jam. Kalau ada urgent, nanti pagi akan diinfokan ke Kak Muhdan."

### 2.8 KEKURANGAN STORAGE VPS

**Skenario:** Storage VPS penuh (sekarang 38GB/58GB, 20GB free). Database SQLite terus membesar.

**Mitigasi:**
- ✅ Auto-cleanup backup >7 hari.
- ✅ Monitoring via cron: setiap minggu cek `df -h` → kalau <10GB, kirim warning ke Bang Dadan.
- ✅ Log chat lama bisa di-archive ke Google Drive setiap bulan.

---

## 📊 MATRIKS RISIKO

| Risiko | Probabilitas | Dampak | Level | Mitigasi |
|--------|:-----------:|:------:|:-----:|----------|
| DeepSeek down | Rendah | Tinggi | 🟡 | Fallback OpenRouter |
| VPS restart | Rendah | Tinggi | 🟡 | Auto-restart |
| Bukti transfer palsu | Sedang | Sedang | 🟡 | Verifikasi manual >Rp50rb |
| User share akun | Tinggi | Rendah | 🟢 | Detek nomor + kode unik |
| Spam user | Tinggi | Rendah | 🟢 | Pola deteksi + slow down |
| DB corrupt | Rendah | Tinggi | 🟡 | Backup harian 3 lokasi |
| Kode unik bentrok | Sangat Rendah | Rendah | 🟢 | +timestamp |
| User chat malam | Tinggi | Rendah | 🟢 | Filter notifikasi |

---

## ❌ BAGIAN 3: RISIKO YANG BELUM ADA SOLUSINYA (Perlu Diskusi)

### 3.1 TIDAK BISA CEK SALDO REAL-TIME

**Deskripsi:** Aiman cuma bisa lihat bukti transfer gambar. Tidak bisa akses mutasi rekening Bang Dadan.

**Dampak:** User nakal bisa edit screenshot transfer nominal kecil jadi besar.

**Diskusi:**
- Mau Bang buka akses mutasi (via mobile banking API)? → Risiko keamanan tinggi.
- Atau cukup verifikasi manual Bang untuk nominal >Rp50rb?
- Atau Bang buatkan **rekening khusus WAJAR.AI** yang bisa Aiman cek saldonya?

### 3.2 TIDAK BISA BLOKIR USER NAKAL

**Deskripsi:** Kalau ada user spam / abuse, Aiman gak bisa blokir nomor WA mereka.

**Dampak:** User bisa terus chat meski Aiman respon "jangan spam."

**Diskusi:**
- Bang Dadan bisakah blokir nomor user dari WA Bang?
- Atau Aiman ignore aja chat dari nomor tertentu?

### 3.3 USER MINTA REFUND SAMPAI KE PENGADUAN

**Deskripsi:** Kalau user ngadu ke UU ITE / YLKI / Polisi karena "tidak bisa refund."

**Dampak:** Reputasi, waktu, tenaga.

**Diskusi:**
- Perlu bikin Syarat & Ketentuan yang jelas di landing page?
- "Dengan melakukan pembayaran, user menyetujui bahwa layanan tidak dapat direfund."

### 3.4 USER KELUH "AIMAN SALAH JAWAB"

**Deskripsi:** AI kadang salah (halusinasi). User komplain: "Aiman ngasih jawaban salah tentang Matematika, anak saya jadi bingung."

**Dampak:** Kepercayaan hilang.

**Diskusi:**
- Perlu disclaimer: "WAJAR.AI adalah AI, tidak 100% akurat. Cross-check dengan guru."
- Atau Aiman selalu bilang "cek lagi ya" untuk jawaban kritis?
