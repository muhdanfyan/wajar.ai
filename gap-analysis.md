# WAJAR.AI — Gap Analysis & Celah yang Terlewat

Setelah Aiman bayangkan dari sudut pandang user real, ini yang masih kurang:

---

## ❌ CELAH #1: TIDAK ADA RESPON CEPAT JIKA USER DIAM

**Masalah:** User daftar, dapet gratis 8.000 kata, lalu... user nggak balas chat lagi. Atau user tanya 1-2 pertanyaan lalu hilang berhari-hari.

**Solusi:**
- Kalau user diam >24 jam setelah daftar → Aiman kirim: "Hai, masih ada 7.500 kata gratis kamu. Mau lanjut belajar?"
- Kalau user diam >3 hari setelah bayar → Aiman kirim: "Hai, sisa waktu premium kamu masih 3 jam. Mau pakai?"
- **Auto-reminder via n8n** yang trigger dari tb_progress_belajar

---

## ❌ CELAH #2: USER LUPA KALO UDAH BAYAR

**Masalah:** User transfer Rp10.000, Aiman aktivasi 1 hari. User pake 1 jam terus besoknya lupa kalau masih punya sisa.

**Solusi:**
- Setiap kali user chat, Aiman bilang: "Sisa waktu premium kamu: X jam lagi ✅"
- Sebelum expired: "Sisa 30 menit lagi. Mau perpanjang?"
- Setelah expired: "Masa premium udah habis. Mau lanjut? Rp1.000/jam"

---

## ❌ CELAH #3: TIDAK ADA JADWAL BELAJAR

**Masalah:** User belajar kapan aja suka — kadang seminggu baru chat lagi. Progress jadi lambat.

**Solusi:**
- Kalau user minta, Aiman bisa bikin jadwal rutin: "Setiap hari jam 19:00 belajar Matematika 30 menit"
- Aiman ingetin sesuai jadwal

---

## ❌ CELAH #4: TIDAK ADA RIWAYAT BELAJAR UNTUK USER

**Masalah:** User tanya sesuatu, besoknya tanya lagi topik yang mirip. Aiman jawab lagi dari awal — buang kata & boros.

**Solusi:**
- Aiman catat topik yang udah dibahas per user
- Kalau user tanya lagi: "Ini mirip yang kemarin kamu tanya. Mau Aiman jelasin ulang atau lanjut aja?"
- **Efisiensi** — user hemat jatah kata, Aiman gak jawab ulang

---

## ❌ CELAH #5: TIDAK ADA LEVEL / SERTIFIKASI

**Masalah:** User belajar terus, tapi gak tau progressnya gimana. Gak ada motivasi lanjutan.

**Solusi:**
- Setiap 10 sesi → Aiman kasih ringkasan: "Kamu udah naik level! Awalnya Pemula, sekarang Udah Menengah."
- Format ringkasan:
  ```
  🎓 LAPORAN BELAJAR — [Nama]
  📚 Topik: Matematika
  📈 Level: Pemula → Menengah
  📝 Total: 15 sesi, 4 jam, 2.500 kata
  ⭐ Rating: 4.5/5
  💡 Saran: Coba tantangan soal cerita
  ```

---

## ❌ CELAH #6: USER TANYA HAL DI LUAR KOMPETENSI

**Masalah:** User minta Aiman ngerjain tugas/PR atau nulisin esai buat mereka — masuk ranah plagiarisme.

**Solusi:**
- Aiman harus punya **filter konten**: bantu pahami, bukan kerjain
- Kalau user minta: "Tulisin PR Matematika aku dong" → Aiman tolak halus: "Aiman bantu pahamin caranya, bukan ngerjain langsung ya. Coba kita bahas soalnya pelan-pelan"
- Catat di log kalau user coba curang

---

## ❌ CELAH #7: TIDAK ADA MODE BELAJAR OFFLINE / TERTULIS

**Masalah:** Kadang user minta materi yang bisa dipelajari ulang, bukan cuma chat. Misal user minta rangkuman atau catatan.

**Solusi:**
- Aiman bisa kirim resume dalam bentuk teks yang rapi: "Ini rangkuman belajar kamu hari ini..."
- Kalau penting, user bisa minta Kirim ke Email (tapi ini nyusul)

---

## ❌ CELAH #8: PEMANTAUAN WAKTU PREMIUM TIDAK KETAT

**Masalah:** User premium (Rp1rb/jam) — apakah dihitung sejak chat pertama atau sejak aktivasi? Kalau sejak aktivasi, user yang chat 5 menit trus balik 3 jam lagi — rugi.

**Solusi:**
- **Sistem counter aktif**: waktu premium jalan hanya ketika user lagi chat aktif
- Kalau user diam >15 menit → timer pause
- Kalau user chat lagi → timer lanjut
- Aiman: "Waktu premium kamu berjalan selama chat aktif. Kalau lagi nggak chat, waktu gak berkurang."

---

## RINGKASAN PRIORITAS GAP

| # | Gap | Urgensi | Dampak |
|---|-----|---------|--------|
| 1 | Auto-reminder user diam | 🔴 Tinggi | User hilang |
| 2 | Info sisa waktu tiap chat | 🔴 Tinggi | User bingung |
| 4 | Riwayat belajar user | 🟡 Sedang | Efisiensi |
| 5 | Laporan progress | 🟡 Sedang | Motivasi |
| 8 | Timer premium aktif | 🟡 Sedang | Keadilan harga |
| 6 | Filter plagiarisme | 🔴 Tinggi | Etika |
| 3 | Jadwal belajar | 🟢 Rendah | Opsional |
| 7 | Materi offline | 🟢 Rendah | Nyusul |
