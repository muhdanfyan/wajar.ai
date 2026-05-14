# WAJAR.AI — Ringkasan Skema Pembayaran

---

## SKEMA PEMBAYARAN GABUNGAN

| Nominal | Metode | Keterangan |
|:-------:|--------|------------|
| Rp0 | Gratis | 8.000 kata percobaan |
| Rp1.000 - Rp4.000 | **Lynk.id** | Lewat lynk.id Bang Dadan |
| Rp10.000 | **Lynk.id** | Lewat lynk.id |
| Rp50.000 | **Midtrans/Lynk** | Bisa lynk.id atau Midtrans |
| Rp150.000 | **Midtrans** | Midtrans lebih aman |
| ≥Rp20.000 | **Midtrans** ✅| Rekomendasi pake Midtrans |

## ALUR PEMBAYARAN

```
User: "Mau bayar Rp4rb"
Aiman: kirim link Lynk.id (atau QRIS)
     → User bayar lewat Lynk.id
     → Aiman cek notifikasi
     → Aktivasi

User: "Mau bayar Rp150rb"  
Aiman: kirim link Midtrans (atau QRIS verif manual)
     → User bayar lewat Midtrans
     → API konfirmasi pembayaran ke n8n
     → Notifikasi ke Aiman & Bang Dadan
     → Aktivasi otomatis
```

## YANG DIPERLUKAN

**Dari Bang Dadan:**
1. Link Lynk.id — untuk pembayaran <Rp20rb
2. Akun Midtrans Merchant — untuk ≥Rp20rb (nanti aja, bisa nyusul)
3. QRIS — udah ada ✅

**Besok pagi cukup pake QRIS + Lynk.id dulu.**
Midtrans nyusul kalau udah ada transaksi besar.
