## Author

Cheesecake

## Challenge

message from mom

## Description

Kamu baru saja menerima sebuah email otomatis yang terjadwal dari belasan tahun yang lalu. Pengirimnya adalah ibumu, seorang peneliti utama di Project Aethelgard yang dikabarkan hilang membawa rahasia besar bersamanya.

## Flag

FindITCTF{e4Zy_p1zY_l3M0n_sQu1zYyyY}


## Solution

## Solution

- **__Ekstrak__** file foto `2010.jpg` menggunakan `steghide` untuk menemukan petunjuk tersembunyi. Sesuai pesan Ibu tentang *"behind our smiles"*, terdapat data yang disisipkan di sana.
    ```bash
    steghide extract -sf 2010.jpg
    ```
    Hasilnya adalah username Instagram: `@dr_elenaa_`.

- **__Investigasi__** profil Instagram tersebut. Cari petunjuk di **Highlight Story** atau postingan lama. Anda akan menemukan sebuah **QR Code** yang tersembunyi. Scan QR tersebut untuk mendapatkan link Google Drive berisi `experiment_archive.zip`.

- **__Analisis__** isi ZIP yang telah diunduh. Di dalamnya terdapat file `log_experiment.txt` berisi 1.000 baris data sampah. Ingat prinsip Ibu: *"History never lies"*. Periksa folder tersembunyi `.git` untuk melihat riwayat repository.

- **__Temukan__** angka kunci dari postingan Instagram Ibu yang menyebutkan *"Experiment #742 was the turning point"*. Gunakan angka ini untuk mencari commit spesifik di masa lalu.
    ```bash
    git log --grep="24"

- **__Lakukan__** perpindahan waktu (checkout) ke hash commit yang ditemukan untuk mengembalikan isi file ke kondisi saat eksperimen berhasil.
    ```bash
    git checkout <hash_commit>
    ```

- **__Dapatkan__** flag akhir yang muncul di dalam file `log_experiment.txt` setelah proses checkout berhasil:
    `FindITCTF{e4Zy_p1zY_l3M0n_sQu1zYyyY}`
