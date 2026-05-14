# Workflow n8n — WAJAR.AI Automation

---

## WORKFLOW 1: CHAT LOGGER (SUDAH AKTIF ✅)

**Webhook:** `http://127.0.0.1:5678/webhook/aiman-chat` (POST)

**Trigger:** Setiap selesai chat dengan user WAJAR.AI

**Data yang dikirim:**
```json
{
  "user_id": "62812xxxxxx",
  "topic": "matematika|ngaji|curhat|dll",
  "message": "isi chat terakhir atau ringkasan",
  "is_complaint": false,
  "response_time": 45,
  "status": "resolved|pending"
}
```

**Action:** Simpan ke database `aiman_chat.db` → tabel `tb_log_chat`

---

## WORKFLOW 2: PAYMENT TRACKER (SUDAH AKTIF ✅)

**Webhook:** `http://127.0.0.1:5678/webhook/aiman-payment` (POST)

**Trigger:** User melakukan pembayaran

**Data yang dikirim:**
```json
{
  "nomor_user": "62812xxxxxx",
  "kode_unik": "WAJAR-1732",
  "nominal": 4000,
  "metode": "qris",
  "status": "pending|verified"
}
```

**Action:**
1. Catat di database
2. Hitung durasi berdasarkan nominal
3. Update status jadi "active" setelah verifikasi

**Mapping nominal ke durasi:**
| Nominal | Durasi |
|:-------:|:------:|
| Rp1.000 | 1 jam |
| Rp4.000 | 4 jam |
| Rp10.000 | 1 hari |
| Rp50.000 | 5 hari |
| Rp150.000 | 30 hari |

---

## WORKFLOW 3: REMINDER USER DIAM (BARU)

**Trigger:** Cron — setiap 6 jam

**Action:**
1. Cek di database: user yang daftar (gratis) tapi udah 24 jam gak chat lagi
2. Kirim WA: *"Halo! Masih punya jatah 5.000 kata gratis dari WAJAR.AI. Ada yang mau ditanyain?"*
3. Catat di log

**Cara setup:**
- n8n → New Workflow → Trigger: Cron (every 6 hours)
- HTTP Request → GET ke endpoint (nanti Aiman buatkan)
- WhatsApp → kirim pesan

---

## WORKFLOW 4: MONITORING TRANSAKSI (BARU)

**Trigger:** Cron — setiap jam dari 08:00-22:00

**Action:**
1. Cek database: ada transaksi baru dalam 1 jam terakhir?
2. Kalau ada nominal >Rp50rb → kirim notif ke Bang Dadan via WA
3. Kalau ada transaksi berhasil → catat di log

---

## WORKFLOW 5: LAPORAN HARIAN (BARU)

**Trigger:** Cron — setiap hari jam 20:00

**Action:**
1. Kumpulkan data hari ini:
   - Total user chat
   - Total user baru
   - Total pembayaran
   - Total nominal
   - Komplain (kalau ada)
2. Format pesan:
   *"📊 Laporan WAJAR.AI — [tanggal]
   👥 User chat: X orang
   🆕 User baru: X orang
   💰 Transaksi: X (RpX.XXX)
   ⚠️ Komplain: X"*
3. Kirim ke Bang Dadan via WA

---

## 🚀 PRIORITAS SETUP n8n

| Prioritas | Workflow | Status | Bisa dijalankan? |
|:---------:|----------|:------:|:----------------:|
| 1 | Chat Logger | ✅ Aktif | Jalan terus |
| 2 | Payment Tracker | ✅ Aktif | Jalan terus |
| 3 | **Reminder User Diam** | ❌ Baru | Perlu setup webhook endpoint dari Aiman |
| 4 | **Monitoring Transaksi** | ❌ Baru | Perlu setup cron + notifikasi |
| 5 | **Laporan Harian** | ❌ Baru | Bisa jalan sendiri pake cron OpenClaw |

---

## ⚠️ CATATAN

- Workflow 3, 4, 5 butuh endpoint API yang bisa dipanggil n8n
- Aiman bisa buatkan script endpoint sederhana (Python/Node.js)
- Atau Aiman handle manual lewat cron OpenClaw untuk sementara
- **Saran:** Untuk besok, jalan dulu manual. n8n workflow lengkap nyusul.
