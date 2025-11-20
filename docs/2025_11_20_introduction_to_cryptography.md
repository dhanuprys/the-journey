# Introduction to _Cryptography_

Beberapa waktu lalu (sekitar dari setahun lebih) saya sangat ingin membeli buku tentang kriptografi. Tujuan saya membeli buku tersebut
adalah untuk mengetahui bagaimana enkripsi bekerja, apa saja jenis-jenisnya, hingga algoritma yang sudah ada hingga saat ini. Namun seiring 
berjalannya waktu, saya selalu lupa dan tidak sempat untuk meluangkan uang saya untuk membeli buku-buku impian saya tersebut. Syukurnya, di 
tahun ini cara pembelajaran dan pencarian informasi sudah berubah pesat. Dengan adanya bantuan AI, saya jadi bisa lebih mudah dalam mencari
informasi tentang cryptography ini.

> **DISCLAIMER**: Cryptography yang dimaksud bukanlah blockchain, web3, atau hal-hal advanced lain. Cryptography yang disinggung di sini adalah
> dasar-dasar enkripsi, hashing, dan beberapa fundamental lainnya.

Berikut ini merupakan rangkuman yang bisa saya sampaikan tentang komponen-komponen yang ada pada cryptography.

## Pengertian

COMING SOON

## Jenis-jenis Key

### Symmetric Key

COMING SOON
```bash
openssl rand -base64 96
```

### Asymmetric Key

COMING SOON

```bash
openssl req -x509 -new -newkey ed25519 -keyout priv.key -out cert.pem -days 365
```

## Metode-metode Cryptography

### Encryption/Decryption

### Hash

Hash merupakan sebuah metode untuk mengubah sebuah data menjadi teks yang teracak, yang di mana teks ini tidak bisa dikembalikan seperti semula.
Contohnya, `dhanu` jika di-hash akan menjadi `as8923f09s8df09w0329sdf89`. Teks aneh yang tidak bisa dibaca tadi (`as89...`) merupakan hasil dari 
hash `dhanu`, dengan kata lain hasil hash tersebut tidak bisa dikembalikan menjadi data seperti semula (`as89...` => `dhanu` tidak akan bisa).
Mengapa? Karena itu memang sifat dasar dari hashing ini.

### Signing Key
