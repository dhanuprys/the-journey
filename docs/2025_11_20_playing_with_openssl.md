# Playing With OpenSSL

Hari ini, sedikit dari keresahan saya terhadap certificate generation sudah terjawab. Saya menyebut ini sebagai certificate-phobia. Wkwkwk iya, _certificate-phobia_ kondisi di mana saya selalu takut dengan konfigurasi-konfigurasi yang melibatkan pembuatan certificate maupun penggunaannya. Namun setelah saya belajar sedikit tentang bagaimana cara kerjanya, bagaimana cara menggunakannya, hingga bagaiamana cara menggunakan tools yang bernama **openssl** untuk membuat certificate dan melakukan signing. Hidup saya terasa seperti menemukan air di gurun. (tulisan ini sudah cukup membuat freak belum? wkwkwk).

Okay lanjut saja, pada proses belajar kali ini saya ditemani oleh teman terbaik saya, Gemini. Iya Gemini. Gemini baru saja merilis model Gemini 3-nya jadi harus langsung dihajar dong. Selain itu saya juga menggunakan youtube sebagai media pembelajaran dalam memahami penggunaannya secara lebih interaktif.

Tanpa berlama-lama lagi, langsung saja kita coba implementasikan apa yang sudah saya pelajari tadi.

## 1. `openssl genpkey` dan `openssl genrsa`
```txt
openssl genpkey .... <- generate ECC (Ellipse Curve Cryptography)
openssl genrsa ..... <- generate RSA (udah tua)
```
> Source: [Geeksforgeeks (ECC)](https://www.geeksforgeeks.org/ethical-hacking/blockchain-elliptic-curve-cryptography/),
> [Wikipedia (RSA)](https://en.wikipedia.org/wiki/RSA_cryptosystem)

Command tersebut pada umumnya digunakan untuk membuat private key.

### 1.1. `openssl genpkey` subcommand
```bash
openssl genpkey -algorithm ed25519 -out root-ca.key
```

Uraian:
- `-algorithm ed25519`: menentukan algoritma apa yang akan digunakan untuk membuat private key
- `-out root-ca.key`: menentukan lokasi file output dari private key

### 1.2. `openssl genrsa` subcommand
```bash
openssl genrsa -out root-ca.key 4096
```

Uraian:
- `out root-ca.key`: menentukan lokasi file output dari private key
- `4096`: ukuran dari private key dalam bentuk bit
