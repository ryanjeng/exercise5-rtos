# **Demonstrasi Masalah Kontensi Akses pada Sistem Multitasking**

## **Deskripsi**
Repositori ini berisi implementasi dari *Exercise 5 – Demonstrate Access Contention Problems in a Multitasking System*. Latihan ini dirancang untuk menunjukkan bahwa kontensi akses terhadap sumber daya bersama dalam sistem multitasking dapat menyebabkan data korup, tugas tidak berjalan sesuai harapan, dan perilaku sistem yang tidak diinginkan. 

Melalui latihan ini, kita akan memahami pentingnya mengelola sumber daya bersama dengan mekanisme perlindungan seperti *mutex* atau *semaphores* untuk mencegah akses simultan yang tidak diinginkan.

---

## **Struktur Sistem**
Sistem terdiri dari:
1. **Dua tugas utama**:
   - **Task 1 (FlashGreenLedTask)**: Mengakses sumber daya bersama sambil menyalakan LED hijau.
   - **Task 2 (FlashRedLedTask)**: Mengakses sumber daya bersama sambil menyalakan LED merah.
2. **Sumber daya bersama**:
   - Disimulasikan sebagai proses baca/tulis dengan *software delay*.
   - Kontensi akses dideteksi dengan menggunakan flag (*Start flag*).
3. **Indikasi Kontensi**:
   - Jika terjadi kontensi, LED biru akan menyala untuk menunjukkan bahwa dua tugas mencoba mengakses sumber daya secara bersamaan.

---

## **Struktur Proyek**
- **Task 1 (FlashGreenLedTask)**:
  - Menyalakan LED hijau.
  - Mengakses sumber daya bersama.
  - Mematikan LED hijau.
  - *Delay* selama 0,5 detik.
- **Task 2 (FlashRedLedTask)**:
  - Menyalakan LED merah.
  - Mengakses sumber daya bersama.
  - Mematikan LED merah.
  - *Delay* selama 0,1 detik.
- **Akses Sumber Daya Bersama**:
  - Mengecek status flag:
    - Jika `Up`, set flag ke `Down` dan lanjutkan akses.
    - Jika `Down`, nyalakan LED biru untuk menunjukkan adanya kontensi.
  - Simulasi akses dengan *software delay* selama 0,5 detik.
  - Set flag kembali ke `Up` setelah selesai.

---

## **Langkah Penggunaan**
1. **Setup Hardware**:
   - Gunakan mikrokontroler (seperti STM32).
   - Sambungkan LED hijau, merah, dan biru ke pin yang sesuai.

2. **Implementasi dan Testing**:
   - Implementasikan tugas satu per satu:
     - Periksa apakah setiap tugas berjalan sesuai dengan waktu yang ditentukan.
     - Pastikan tugas dapat mengakses sumber daya tanpa masalah jika berjalan sendiri.
   - Aktifkan kedua tugas:
     - Set Task 2 (FlashRedLedTask) memiliki prioritas lebih tinggi.
     - Perhatikan jika LED biru menyala, menunjukkan adanya kontensi.

3. **Penyesuaian Prioritas** *(Opsional)*:
   - Tukar prioritas kedua tugas.
   - Uji kembali sistem dan perhatikan hasilnya.

4. **Eksperimen Tambahan** *(Opsional)*:
   - Ubah kode untuk membuat LED biru berkedip saat terjadi kontensi. Hal ini akan memberikan gambaran kasar tentang frekuensi kontensi.

![Demo]([https://imgur.com/a/HuffCr6](https://imgur.com/Z2dEXyr))

---

## **Pelajaran yang Didapat**
- **Masalah Kontensi**:
  - Akses simultan ke sumber daya bersama dapat menyebabkan kerusakan data.
  - Masalah ini sering kali tidak terdeteksi tanpa mekanisme perlindungan.
- **Pentingnya Perlindungan Akses**:
  - Menggunakan *mutex* atau *semaphores* untuk mencegah akses simultan.
  - Menyusun desain multitasking yang aman dan efisien.
- **Pengelolaan Tugas Multitasking**:
  - Prioritas tugas yang salah dapat menyebabkan masalah pada sistem.
  - Tugas dengan prioritas rendah lebih rentan terhadap preempasi.

---

## **Persyaratan Sistem**
- Mikrokontroler dengan dukungan RTOS.
- Perangkat keras tambahan: LED hijau, merah, biru.
- Perangkat lunak: IDE untuk pengembangan firmware (misalnya STM32CubeIDE).

---

Dengan menjalankan latihan ini, Anda akan memahami tantangan pengelolaan sumber daya bersama dalam sistem multitasking dan bagaimana cara mencegah masalah tersebut secara efektif.
