# Saweria QRIS Generator
<p align="center">
  <img src="qriss.png" alt="QRIS Logo" width="150"/>
</p>

[![NPM Version](https://img.shields.io/npm/v/qris-saweria.svg)](https://www.npmjs.com/package/qris-saweria)
[![PyPI version](https://img.shields.io/pypi/v/qris-saweria.svg)](https://pypi.org/project/qris-saweria/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/AutoFTbot/saweria-qris/blob/master/LICENSE)

---

## ⚠️ Peringatan

Menggunakan segala jenis program otomatisasi di akun Anda dapat mengakibatkan akun Anda dilarang secara permanen oleh Saweria.  
Gunakan dengan risiko Anda sendiri.

---

## Fitur

- Membuat kode pembayaran QRIS
- Template DANA opsional (bawaan)
- Nama pengirim & pesan acak otomatis
- Cek status pembayaran
- API sederhana untuk Node.js & Python

---

## Instalasi

### Node.js (NPM)
```bash
npm install qris-saweria
```

### Python (PyPI)
```bash
pip install qris-saweria
```

---

## Penggunaan

### Node.js (NPM)

```javascript
const saweriaQris = require('qris-saweria');

// QRIS dengan template DANA (default)
const [qrString, transactionId, qrImagePath] = await saweriaQris.createPaymentQr(
    'nama_saweria',
    10000,
    'donatur@email.com',
    'qris_template.png', // output file
    true                // gunakan template (default: true)
);
console.log('QRIS dengan template:', qrImagePath);

// QRIS tanpa template (hanya QR code saja)
const [qrString2, transactionId2, qrImagePath2] = await saweriaQris.createPaymentQr(
    'nama_saweria',
    10000,
    'donatur@email.com',
    'qris_only.png',
    false               // tanpa template
);
console.log('QRIS tanpa template:', qrImagePath2);

// Cek status pembayaran
const isPaid = await saweriaQris.paidStatus(transactionId);
console.log('Sudah dibayar?', isPaid);
```

---

### Python (PyPI)

```python
from qris_saweria import create_payment_qr, check_paid_status

# QRIS dengan template DANA (default)
qr_string, transaction_id, qr_path = create_payment_qr(
    'nama_saweria',
    10000,
    'donatur@email.com',
    'qris_template.png',  # output file
    True                 # pakai template (default: True)
)
print('QRIS dengan template:', qr_path)

# QRIS tanpa template (hanya QR code saja)
qr_string2, transaction_id2, qr_path2 = create_payment_qr(
    'nama_saweria',
    10000,
    'donatur@email.com',
    'qris_only.png',
    False                # tanpa template
)
print('QRIS tanpa template:', qr_path2)

# Cek status pembayaran
is_paid = check_paid_status(transaction_id)
print('Sudah dibayar?', is_paid)
```

---

## Pilihan Output QRIS (Template/Non-Template)

- **Dengan template:** (default) QR code ditempel di atas template DANA bawaan.
- **Tanpa template:** Output hanya QR code saja (tanpa latar belakang).

---

## Catatan

- Minimal transaksi: 1.000 IDR
- Nama pengirim & pesan dibuat otomatis
- Template DANA sudah tersedia di package (tidak perlu download manual)
- Untuk template custom, bisa gunakan argumen `template_path` (Python) atau ganti file `template.png` (Node.js)

---

## Kontribusi

Kontribusi, masalah, dan permintaan fitur sangat diterima!  
Silakan periksa [halaman issues](https://github.com/AutoFTbot/saweria-qris/issues).

---

## Lisensi

MIT
