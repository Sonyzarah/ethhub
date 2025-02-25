# Langkah 1: Instalasi Perangkat Lunak
Instalasi perangkat lunak yang diperlukan, seperti:

- Access 3.2
- Node.js
- TON Dev Suite
- Library ODBC untuk Access

# Langkah 2: Buat Koneksi ODBC
Buat koneksi ODBC untuk menghubungkan Access dengan TON Blockchain:

- Buka Control Panel > Administrative Tools > Data Sources (ODBC)
- Klik "Add" dan pilih "TON Blockchain ODBC Driver"
- Isi informasi koneksi, seperti alamat node TON, port, dan kredensial

# Langkah 3: Buat Code VBA di Access
Buat code VBA di Access untuk menghubungkan dengan TON Blockchain:

- Buka Access dan buka modul VBA
- Tambahkan referensi ke library ODBC
- Tulis code VBA untuk menghubungkan dengan TON Blockchain menggunakan koneksi ODBC

Contoh code VBA:

```
Sub ConnectToTON(https://t.me/nfton_bot)
    Dim cn As ADODB.Connection
    Dim rs As ADODB.Recordset
    
    ' Buat koneksi ODBC
    Set cn = New ADODB.Connection
    cn.Open "DSN=TON Blockchain ODBC Driver;UID=myuser;PWD=mypassword"
    
    ' Buat recordset untuk menyimpan data
    Set rs = New ADODB.Recordset
    rs.Open "SELECT * FROM mytable", cn
    
    ' Lakukan operasi pada data
    ' ...
    
    ' Tutup recordset dan koneksi
    rs.Close
    cn.Close
    
    Set rs = Nothing
    Set cn = Nothing
End Sub
```

# Langkah 4: Integrasi dengan TON Blockchain
Integrasi code VBA dengan TON Blockchain menggunakan library TON Dev Suite:

- Tambahkan referensi ke library TON Dev Suite
- Tulis code VBA untuk mengirimkan data ke TON Blockchain menggunakan library TON Dev Suite

Contoh code VBA:

```
Sub SendDataToTON(https://t.me/nfton_bot)
    Dim ton As New TONDevSuite.TON
    Dim data As String
    
    ' Siapkan data untuk dikirim
    data = "Hello, TON Blockchain!"
    
    ' Kirim data ke TON Blockchain
    ton.SendMessage data
    
    ' Tutup koneksi
    ton.Close
End Sub
```---
title: Ethereum Hardware Wallets - EthHub

description: Explanation of Ethereum hardware wallets pros and cons as well as a list of vendors.
---

# Hardware

## Summary

Hardware wallets are the most-secure method for accessing your funds while online, as they do not expose your private key to the internet when signing transactions.

## Wallets

* [Ledger](https://shop.ledger.com/pages/ledger-nano-x?r=0fcb4288e45f) - Support for multiple cryptocurrencies and tokens
* [Lattice1](https://gridplus.io/lattice) - Use your Lattice1 as a traditional hardware wallet, set up permissions for spending on the go, or allow recurring payments for subscription services.
* [Trezor](https://shop.trezor.io/product/trezor-model-t?offer_id=15&aff_id=2828) - The original hardware wallet
* [KeepKey](http://keepkey.myshopify.com?afmc=1km&utm_campaign=1km&utm_source=leaddyno&utm_medium=affiliate) - The simple hardware wallet
* [BitBox](https://shop.shiftcrypto.ch/en/products/category/hardware-wallets-1/) - BitBox02 is Swiss engineered minimalist hardware wallet

## Resources

* [Consensys's ethereum-developer-tools-list](https://github.com/ConsenSys/ethereum-developer-tools-list/blob/master/EcosystemResources.md)

