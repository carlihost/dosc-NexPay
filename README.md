Ah paham sekarang, pas di-upload ke GitHub Markdown dia malah hancur jadi berantakan satu baris/paragraf karena kurang spasi baris baru (line breaks) dan blok kodenya (```).
Nih, gue benerin format Markdown-nya supaya pas diposting atau di-save ke file .md langsung otomatis rapi, pakai blok kode yang proper, dan gampang banget disalin. Cukup Copy semua isi di dalam kotak di bawah ini:
# 🚀 NexPay Gateway - Panduan Integrasi Merchant

Selamat datang di dokumentasi resmi **NexPay Gateway**. Panduan ini dirancang untuk membantu Anda (Merchant/Pengguna) mengintegrasikan sistem pembayaran **GoPay (GoBiz)** dan **ShopeePay** ke dalam aplikasi, bot, atau website Anda secara mudah dan aman.

---

## 🌐 Informasi Gateway
- **Base URL API**: `[https://gopay.nexsora.biz.id](https://gopay.nexsora.biz.id)`
- **Metode Request**: `POST`
- **Format Data**: `application/json`

---

## 🟢 1. GoPay Merchant Endpoints

### A. Pendaftaran Akun GoPay
Mendaftarkan nomor merchant Anda ke sistem menggunakan API Key Aktivasi yang diberikan oleh admin.
- **URL**: `POST /api/gopay/daftar`
- **Request Body**:
```json
{
  "phone": "6281272960315",
  "activation_key": "NEXACT_...",
  "username": "namatoko",
  "password": "password_anda",
  "telegram_chat_id": "ID_TELEGRAM_ANDA"
}

 * Contoh Response:
{
  "success": true,
  "message": "Pendaftaran berhasil. Silakan lakukan verifikasi OTP...",
  "data": { 
    "phone": "6281272960315",
    "status": "waiting_for_otp"
  }
}

B. Login & Verifikasi OTP GoPay
Memasukkan kode OTP untuk menyelesaikan proses login dan mengaktifkan API Key merchant Anda.
 * URL: POST /api/gopay/login
 * Request Body:
{
  "phone": "6281272960315",
  "otp": "7119",
  "username": "namatoko",
  "password": "password_anda",
  "telegram_chat_id": "ID_TELEGRAM_ANDA"
}

 * Contoh Response (Mendapatkan API Key):
{
  "success": true,
  "message": "Login GoPay berhasil & API Key merchant telah diaktifkan!",
  "data": {
    "merchant_id": "G724842544",
    "phone": "6281272960315",
    "api_key": "GPAY_aacdd905c468fd2b492ae0e1e7acb9dc",
    "status": "connected"
  }
}

> ⚠️ Penting: Simpan api_key Anda dengan aman! Key ini wajib disertakan pada setiap request API GoPay Anda melalui Header: Authorization: Bearer <API_KEY>
> 
C. Informasi Akun GoPay
Melihat status akun, masa aktif, dan informasi merchant Anda.
 * URL: POST /api/gopay/account-info
 * Headers: Authorization: Bearer GPAY_...
D. Atur URL Webhook (Callback)
Mengatur endpoint server Anda agar otomatis menerima notifikasi saat pembayaran berhasil.
 * URL: POST /api/gopay/set-webhook
 * Headers: Authorization: Bearer GPAY_...
 * Request Body:
{
  "webhook_url": "https://domain-anda.com/path/callback"
}

E. Test Webhook GoPay
Mengirimkan simulasi transaksi sukses ke webhook Anda untuk memastikan sistem callback berjalan dengan baik.
 * URL: POST /api/gopay/test-webhook
 * Headers: Authorization: Bearer GPAY_...
F. Atur QRIS Statis
Mengatur atau memperbarui string QRIS statis toko Anda.
 * URL: POST /api/gopay/set-qris
 * Headers: Authorization: Bearer GPAY_...
 * Request Body:
{
  "phone": "6281272960315",
  "qr_string": "00020101021126610014COM.GO-JEK.WWW..."
}

G. Buat QRIS Dinamis
Membuat tagihan QRIS instan dengan nominal tertentu beserta gambar QR-nya.
 * URL: POST /api/gopay/create-qris
 * Headers: Authorization: Bearer GPAY_...
 * Request Body:
{
  "amount": 10000
}

H. Cek Status Transaksi
Mengecek status pembayaran berdasarkan ID transaksi.
 * URL: POST /api/gopay/status
 * Headers: Authorization: Bearer GPAY_...
 * Request Body:
{
  "transaction_id": "GOPAY-1792410048386"
}

I. Batalkan Transaksi / QRIS
Membatalkan tagihan transaksi yang masih berstatus pending.
 * URL: POST /api/gopay/cancel-qris
 * Headers: Authorization: Bearer GPAY_...
 * Request Body:
{
  "transaction_id": "GOPAY-1792410048386"
}

J. List Transaksi Pending
Melihat daftar seluruh transaksi Anda yang sedang berstatus pending.
 * URL: POST /api/gopay/pending-transactions
 * Headers: Authorization: Bearer GPAY_...
K. Logout Akun GoPay
Menghapus sesi dan data merchant dari server gateway.
 * URL: POST /api/gopay/logout
 * Headers: Authorization: Bearer GPAY_...
🟠 2. ShopeePay Merchant Endpoints
A. Pendaftaran & Login ShopeePay
Mendaftarkan atau menghubungkan akun ShopeePay Anda menggunakan key aktivasi.
 * URL: POST /api/shopee/daftar atau POST /api/shopee/login
 * Request Body:
{
  "phone": "6285657179231",
  "activation_key": "NEXACT_...",
  "username": "namatoko",
  "password": "password_anda",
  "qris_string": "00020101021126610014...",
  "telegram_chat_id": "ID_TELEGRAM_ANDA"
}

B. Informasi Akun ShopeePay
Melihat informasi akun ShopeePay Anda.
 * URL: POST /api/shopee/account-info
 * Request Body:
{
  "phone": "6285657179231",
  "api_key": "SHP_KEY_..."
}

C. Atur URL Webhook ShopeePay
Mengatur endpoint penerima notifikasi otomatis untuk ShopeePay.
 * URL: POST /api/shopee/set-webhook
 * Request Body:
{
  "phone": "6285657179231",
  "api_key": "SHP_KEY_...",
  "webhook_url": "https://domain-anda.com/path/callback"
}

D. Test Webhook ShopeePay
Mengirim sinyal tes webhook ke URL callback Anda.
 * URL: POST /api/shopee/test-webhook
 * Request Body:
{
  "phone": "6285657179231",
  "api_key": "SHP_KEY_..."
}

E. Buat QRIS Dinamis ShopeePay
Membuat QRIS tagihan instan untuk ShopeePay.
 * URL: POST /api/shopee/create-qris
 * Request Body:
{
  "phone": "6285657179231",
  "api_key": "SHP_KEY_...",
  "amount": 10000
}

F. Cek Status Transaksi ShopeePay
Mengecek status pembayaran ShopeePay.
 * URL: POST /api/shopee/status
 * Request Body:
{
  "phone": "6285657179231",
  "api_key": "SHP_KEY_...",
  "transaction_id": "SHP-1792235912345"
}

G. Batalkan QRIS ShopeePay
Membatalkan tagihan ShopeePay yang aktif.
 * URL: POST /api/shopee/cancel-qris
 * Request Body:
{
  "phone": "6285657179231",
  "api_key": "SHP_KEY_...",
  "transaction_id": "SHP-1792235912345"
}

H. List Transaksi Pending ShopeePay
Melihat daftar transaksi ShopeePay Anda yang masih berstatus pending.
 * URL: POST /api/shopee/pending-transactions
 * Request Body:
{
  "phone": "6285657179231",
  "api_key": "SHP_KEY_..."
}

I. Logout Akun ShopeePay
Menghapus sesi merchant ShopeePay dari server.
 * URL: POST /api/shopee/logout
 * Request Body:
{
  "phone": "6285657179231",
  "api_key": "SHP_KEY_..."
}

🔔 Webhook & Keamanan (HMAC Verification)
Setiap notifikasi webhook yang dikirim ke server Anda dilengkapi dengan header pengaman HMAC SHA256:
 * Header Key: x-signature
 * Cara Verifikasi (Node.js):
const crypto = require('crypto');
const signature = req.headers['x-signature'];
const expectedSignature = crypto
   .createHmac('sha256', API_KEY)
   .update(JSON.stringify(req.body.data))
   .digest('hex');

if (signature !== expectedSignature) {
   return res.status(403).send('Invalid Signature');
}

 * Contoh Payload Webhook (Saat Pembayaran Sukses):
{
  "success": true,
  "event": "transaction.update",
  "data": {
    "transaction_id": "GOPAY-1792410048386",
    "merchant_id": "G724842544",
    "phone": "6281272960315",
    "amount": 10000,
    "total": 10000,
    "status": "sukses",
    "time": "19/10/2026, 18:45:48"
  }
}


