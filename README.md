# Saweria QRIS Generator

API tidak resmi saweria.co yang dapat membuat dan memeriksa kode QRIS secara otomatis

[![NPM Version](https://img.shields.io/npm/v/saweria-qris.svg)](https://www.npmjs.com/package/saweria-qris)
[![License](https://img.shields.io/npm/l/saweria-qris.svg)](https://github.com/AutoFTbot/saweria-qris/blob/master/LICENSE)

## Fitur

- Membuat kode pembayaran QRIS
- Integrasi template DANA opsional
- Pembuatan nama pengirim secara acak
- Pengecekan status pembayaran
- API yang sederhana dan mudah digunakan

## Instalasi

```bash
npm install saweria-qris
```

## Mulai Cepat

```javascript
const saweriaQris = require('saweria-qris');

// Membuat kode QR dengan template DANA
const [qrString, transactionId, qrImagePath] = await saweriaQris.createPaymentQr(
    'nama_saweria',    // Nama pengguna Saweria Anda
    10000,             // Jumlah dalam IDR (minimum 10000)
    'donatur@email.com' // Email donatur
);

// Memeriksa status pembayaran
const isPaid = await saweriaQris.paidStatus(transactionId);
```

## Referensi API

### createPaymentQr(saweriaUsername, amount, email[, outputPath, useTemplate])

Membuat kode pembayaran QRIS dan menghasilkan gambar QR.

#### Parameter:
- `saweriaUsername` (string) - Nama pengguna Saweria Anda
- `amount` (number) - Jumlah donasi dalam IDR (minimum 10000)
- `email` (string) - Alamat email donatur
- `outputPath` (string, opsional) - Path untuk gambar QR code (default: 'qris.png')
- `useTemplate` (boolean, opsional) - Apakah akan menggunakan template DANA (default: true)

#### Return:
Promise yang mengembalikan `[qrString, transactionId, qrImagePath]`:
- `qrString` - String pembayaran QRIS
- `transactionId` - ID transaksi untuk pengecekan status
- `qrImagePath` - Path tempat gambar QR disimpan

### paidStatus(transactionId)

Memeriksa apakah pembayaran telah selesai.

#### Parameter:
- `transactionId` (string) - ID transaksi dari createPaymentQr

#### Return:
Promise yang mengembalikan `boolean` - `true` jika sudah dibayar, `false` jika belum dibayar

## Contoh
### Membuat TestFull

```javascript
WATING
```

### Membuat QR dengan Template

```javascript
const saweriaQris = require('saweria-qris');

async function createPayment() {
    try {
        const [, transactionId, qrPath] = await saweriaQris.createPaymentQr(
            'saweriaku',
            15000,
            'donatur@email.com',
            'pembayaran.png',
            true // gunakan template
        );
        
        console.log('QR Code dibuat:', qrPath);
        console.log('ID Transaksi:', transactionId);
    } catch (error) {
        console.error('Error:', error.message);
    }
}
```

### Membuat QR tanpa Template

```javascript
const [, transactionId, qrPath] = await saweriaQris.createPaymentQr(
    'saweriaku',
    15000,
    'donatur@email.com',
    'pembayaran.png',
    false // tanpa template
);
```

### Memantau Status Pembayaran

```javascript
const saweriaQris = require('saweria-qris');

async function checkPayment(transactionId) {
    while (true) {
        const isPaid = await saweriaQris.paidStatus(transactionId);
        if (isPaid) {
            console.log('Pembayaran diterima!');
            break;
        }
        await new Promise(resolve => setTimeout(resolve, 5000)); // Periksa setiap 5 detik
    }
}
```

## Catatan

- Jumlah trx minimum adalah 1.000 IDR
- Nama pengirim dibuat secara otomatis
- Pesan dukungan acak disertakan dengan setiap donasi
- Template DANA bersifat opsional

## Lisensi

MIT

## Kontribusi

Kontribusi, masalah, dan permintaan fitur sangat diterima! Silakan periksa [halaman issues](https://github.com/AutoFTbot/saweria-qris/issues).
