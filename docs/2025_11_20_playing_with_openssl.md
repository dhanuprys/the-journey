# Playing With OpenSSL

Hari ini, sedikit dari keresahan saya terhadap certificate generation sudah terjawab. Saya menyebut ini sebagai certificate-phobia. Wkwkwk iya, _certificate-phobia_ kondisi di mana saya selalu takut dengan konfigurasi-konfigurasi yang melibatkan pembuatan certificate maupun penggunaannya. Namun setelah saya belajar sedikit tentang bagaimana cara kerjanya, bagaimana cara menggunakannya, hingga bagaiamana cara menggunakan tools yang bernama **openssl** untuk membuat certificate dan melakukan signing. Hidup saya terasa seperti menemukan air di gurun. (tulisan ini sudah cukup membuat freak belum? wkwkwk).

Okay lanjut saja, pada proses belajar kali ini saya ditemani oleh teman terbaik saya, Gemini. Iya Gemini. Gemini baru saja merilis model Gemini 3-nya jadi harus langsung dihajar dong. Selain itu saya juga menggunakan youtube sebagai media pembelajaran dalam memahami penggunaannya secara lebih interaktif.

Tanpa berlama-lama lagi, langsung saja kita coba implementasikan apa yang sudah saya pelajari tadi.

## Dasar-dasar command
### 1. Membuat private key
```txt
openssl genpkey .... <- generate ECC (Ellipse Curve Cryptography)
openssl genrsa ..... <- generate RSA (udah tua)
```
> Source: [Geeksforgeeks (ECC)](https://www.geeksforgeeks.org/ethical-hacking/blockchain-elliptic-curve-cryptography/),
> [Wikipedia (RSA)](https://en.wikipedia.org/wiki/RSA_cryptosystem)

Command tersebut pada umumnya digunakan untuk membuat private key.

#### 1.1. `openssl genpkey` subcommand
```bash
openssl genpkey -algorithm ed25519 -out root-ca.key
```

Uraian:
- `-algorithm ed25519`: menentukan algoritma apa yang akan digunakan untuk membuat private key
- `-out root-ca.key`: menentukan lokasi file output dari private key

#### 1.2. `openssl genrsa` subcommand
```bash
openssl genrsa -aes256 -out root-ca.key 4096
```

Uraian:
- `out root-ca.key`: menentukan lokasi file output dari private key
- `4096`: ukuran dari private key dalam bentuk bit

### 2. Membuat public key dari private key yang sudah ada
```bash
openssl req -x509 -new -key private.key -out cert.pem -days 3650
```

Uraian:
- `-x509`: langsung membuat public key tanpa signing request
- `-new`: request cert baru
- `-key private.key`: lokasi file private key yang akan dibuatkan public key nya
- `-out cert.pem`: lokasi penyimpanan public key / output
- `-days 3650`: cert akan valid selama 3650 hari / 10 tahun

### 3. Membuat CSR (Certificate Signing Request)
```bash
openssl req -new -key private.key -out cert.csr
```

## Implementasi

### Membuat public dan private key pair dalam satu baris command
```bash
openssl req -x509 -newkey rsa:2048 -keyout server.key -out server.crt -days 365 -noenc -subj "/CN=localhost"
```

### Membuat root CA dan signing root CA ke public key
```bash
# Membuat public and private key pair root-ca
openssl req -x509 -newkey ed25519 -keyout root-ca.key -out root-ca.crt -days 3650 -subj "/CN=localhost"

# Membuat private key untuk webserver
openssl genpkey -algorithm ed25519 -out server.key

# Membuat CSR untuk webserver
openssl req -new -key server.key -out server.csr -subj "/CN=localhost"

# Signing csr menggunakan root ca
openssl x509 -req -in server.csr -days 365 -CA root-ca.crt -CAkey root-ca.key -CAcreateserial -sha256
```

Yang ada pada webserver/production hanya:
- server.key
- server.crt
- root-ca.crt

> root-ca.key harus ada pada perangkat lokal atau pun tempat penyimpanan yang benar-benar aman dan tidak memiliki kerentanan.
