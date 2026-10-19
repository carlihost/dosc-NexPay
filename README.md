Edit dengan apl Dokumen
Membuat penyesuaian, memberi komentar, dan berbagi dengan yang lain agar dapat mengedit secara bersamaan.
LAIN KALIGUNAKAN APLIKASI
README.md
🚀 NexPay Gateway - Panduan Integrasi Merchant
Selamat datang di dokumentasi resmi NexPay Gateway. Panduan ini dirancang khusus untuk membantu Anda (Merchant/Pengguna) mengintegrasikan sistem pembayaran GoPay (GoBiz) dan ShopeePay ke dalam aplikasi, bot, atau website Anda.

🌐 Informasi Gateway
<table width="100%"> <tr> <td width="20%"><b>Base URL API</b></td> <td><code>https://gopay.nexsora.biz.id</code></td> </tr> <tr> <td><b>Metode Request</b></td> <td><code>POST</code></td> </tr> <tr> <td><b>Format Data</b></td> <td><code>application/json</code></td> </tr> </table>

🟢 1. GoPay Merchant Endpoints
A. Pendaftaran Akun GoPay
Mendaftarkan nomor merchant Anda ke sistem menggunakan API Key Aktivasi yang diberikan oleh admin.

URL: <code>POST /api/gopay/daftar</code>
Request Body:
{
 "phone": "6281272960315",
 "activation_key": "NEXACT_...",
 "username": "namatoko",
 "password": "password_anda",
 "telegram_chat_id": "ID_TELEGRAM_ANDA"
}

Contoh Response:
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

URL: <code>POST /api/gopay/login</code>
Request Body:
{
 "phone": "6281272960315",
 "otp": "7119",
 "username": "namatoko",
 "password": "password_anda",
 "telegram_chat_id": "ID_TELEGRAM_ANDA"
}

Contoh Response (Mendapatkan API Key):
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

⚠️ Penting: Simpan <code>api_key</code> Anda dengan aman! Key ini wajib disertakan pada setiap request API GoPay Anda melalui Header: <code>Authorization: Bearer <API_KEY></code>

C. Endpoint Lainnya (GoPay)
<details> <summary><b>Klik untuk melihat daftar endpoint GoPay selengkapnya</b></summary>

C. Informasi Akun GoPay
URL: <code>POST /api/gopay/account-info</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
D. Atur URL Webhook (Callback)
URL: <code>POST /api/gopay/set-webhook</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
Body: <code>{ "webhook_url": "https://domain-anda.com/path/callback" }</code>
E. Test Webhook GoPay
URL: <code>POST /api/gopay/test-webhook</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
F. Atur QRIS Statis
URL: <code>POST /api/gopay/set-qris</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
Body: <code>{ "phone": "6281272960315", "qr_string": "000201..." }</code>
G. Buat QRIS Dinamis
URL: <code>POST /api/gopay/create-qris</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
Body: <code>{ "amount": 10000 }</code>
H. Cek Status Transaksi
URL: <code>POST /api/gopay/status</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
Body: <code>{ "transaction_id": "GOPAY-..." }</code>
I. Batalkan Transaksi / QRIS
URL: <code>POST /api/gopay/cancel-qris</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
Body: <code>{ "transaction_id": "GOPAY-..." }</code>
J. List Transaksi Pending
URL: <code>POST /api/gopay/pending-transactions</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
K. Logout Akun GoPay
URL: <code>POST /api/gopay/logout</code>
Headers: <code>Authorization: Bearer GPAY_...</code>
</details>

🟠 2. ShopeePay Merchant Endpoints
A. Pendaftaran & Login ShopeePay
Mendaftarkan atau menghubungkan akun ShopeePay Anda menggunakan key aktivasi.

URL: <code>POST /api/shopee/daftar</code> atau <code>POST /api/shopee/login</code>
Request Body:
{
 "phone": "6285657179231",
 "activation_key": "NEXACT_...",
 "username": "namatoko",
 "password": "password_anda",
 "qris_string": "00020101021126610014...",
 "telegram_chat_id": "ID_TELEGRAM_ANDA"
}

B. Endpoint Lainnya (ShopeePay)
<details> <summary><b>Klik untuk melihat daftar endpoint ShopeePay selengkapnya</b></summary>

B. Informasi Akun ShopeePay
URL: <code>POST /api/shopee/account-info</code>
Body: <code>{ "phone": "6285657179231", "api_key": "SHP_KEY_..." }</code>
C. Atur URL Webhook ShopeePay
URL: <code>POST /api/shopee/set-webhook</code>
Body: <code>{ "phone": "6285657179231", "api_key": "SHP_KEY_...", "webhook_url": "https://..." }</code>
D. Test Webhook ShopeePay
URL: <code>POST /api/shopee/test-webhook</code>
Body: <code>{ "phone": "6285657179231", "api_key": "SHP_KEY_..." }</code>
E. Buat QRIS Dinamis ShopeePay
URL: <code>POST /api/shopee/create-qris</code>
Body: <code>{ "phone": "6285657179231", "api_key": "SHP_KEY_...", "amount": 10000 }</code>
F. Cek Status Transaksi ShopeePay
URL: <code>POST /api/shopee/status</code>
Body: <code>{ "phone": "6285657179231", "api_key": "SHP_KEY_...", "transaction_id": "SHP-..." }</code>
G. Batalkan QRIS ShopeePay
URL: <code>POST /api/shopee/cancel-qris</code>
Body: <code>{ "phone": "6285657179231", "api_key": "SHP_KEY_...", "transaction_id": "SHP-..." }</code>
H. List Transaksi Pending ShopeePay
URL: <code>POST /api/shopee/pending-transactions</code>
Body: <code>{ "phone": "6285657179231", "api_key": "SHP_KEY_..." }</code>
I. Logout Akun ShopeePay
URL: <code>POST /api/shopee/logout</code>
Body: <code>{ "phone": "6285657179231", "api_key": "SHP_KEY_..." }</code>
</details>

🔔 Webhook & Keamanan (HMAC Verification)
Setiap notifikasi webhook yang dikirim ke server Anda dilengkapi dengan header pengaman HMAC SHA256:

Header Key: <code>x-signature</code>
Cara Verifikasi (Node.js):
const crypto = require('crypto');
const signature = req.headers['x-signature'];
const expectedSignature = crypto
  .createHmac('sha256', API_KEY)
  .update(JSON.stringify(req.body.data))
  .digest('hex');

if (signature !== expectedSignature) {
  return res.status(403).send('Invalid Signature');
}

Contoh Payload Webhook (Saat Pembayaran Sukses):
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
