## Penjelasan Sistem Fuzzy Klasifikasi Performa Siswa

#### 1. Sumber dan Persiapan Data

- `data.csv` merupakan dataset real yang diambil dari Kaggle. Dataset ini berisi data lengkap mahasiswa, seperti absensi, nilai ujian, tugas, partisipasi, dan atribut lain yang relevan. Data ini digunakan sebagai sumber utama untuk analisis performa siswa secara nyata.

- `dataset_siswa.csv` dataset ini merupakan hasil manipulasi dari data asli (`data.csv`). Data telah disederhanakan dan difokuskan hanya pada dua fitur utama, yaitu **absensi** dan **nilai**. Tujuannya adalah agar sesuai dengan kebutuhan sistem fuzzy yang akan dibangun, sehingga proses inferensi fuzzy menjadi lebih sederhana dan terfokus.

#### 2. Sistem Fuzzy yang Dibangun

Sistem fuzzy yang kita buat terdiri dari dua pendekatan utama:

- **Sistem Fuzzy Mamdani**

  - Menggunakan metode Mamdani berbasis aturan (rule-based) dengan fungsi keanggotaan Gaussian.
  - Input: **absensi** dan **nilai** siswa.
  - Output: Kategori performa siswa (Buruk, Cukup, Bagus).
  - Inferensi dilakukan dengan aturan-aturan fuzzy yang menggabungkan kondisi absensi dan nilai, lalu dilakukan defuzzifikasi untuk mendapatkan skor akhir.
  - Implementasi dilakukan baik secara manual (tanpa library) maupun menggunakan library `skfuzzy`.

- **Sistem Fuzzy Sugeno**
  - Menggunakan metode Sugeno dengan output berupa fungsi linear dari input.
  - Input dan proses keanggotaan sama seperti Mamdani.
  - Output: Skor numerik yang kemudian dipetakan ke kategori performa.
  - Inferensi Sugeno diimplementasikan secara manual tanpa library fuzzy.

#### 3. Evaluasi dan Perbandingan

- Sistem fuzzy diuji pada data hasil manipulasi `dataset_siswa.csv` agar sesuai dengan skenario fuzzy.
- Evaluasi dilakukan menggunakan metrik **accuracy** dan **F1-score** dengan membandingkan hasil prediksi sistem fuzzy terhadap label performa aktual (ground truth).
- Hasil dari kedua metode (Mamdani & Sugeno) dibandingkan untuk melihat metode mana yang lebih baik dalam mengklasifikasikan performa siswa.

4. Catatan

- `data.csv` digunakan sebagai data real untuk memastikan sistem fuzzy dapat diaplikasikan pada data nyata.
- `dataset_siswa.csv` adalah data yang sudah disesuaikan agar sistem fuzzy dapat berjalan optimal dan mudah dievaluasi.
- Sistem fuzzy ini dapat dikembangkan lebih lanjut dengan menambah fitur atau mengubah aturan sesuai kebutuhan studi kasus.

## Cara Menjalankan Sistem Fuzzy

1. Menjalankan Sistem Fuzzy Tanpa Library (Manual)

- Buka file `system_fuzzy_without_library.ipynb` di Jupyter Notebook atau VS Code.
- Jalankan setiap cell secara berurutan.
- Secara default, kode akan membaca file `dataset_siswa.csv` yang sudah dimanipulasi (kolom: absensi, nilai).

2. Menjalankan Sistem Fuzzy Dengan Library (skfuzzy)

- Buka file `system_fuzzy_with_library.ipynb` di Jupyter Notebook atau VS Code.
- Jalankan setiap cell secara berurutan.
- Kode juga menggunakan `dataset_siswa.csv` secara default.

3. Menggunakan Data Asli (`data.csv` dari Kaggle)
   Jika ingin mencoba sistem fuzzy pada data asli (`data.csv`):

- Ubah nama kolom pada file `data.csv`:
  - Kolom absensi: ubah dari Attendance (%) menjadi absensi
  - Kolom nilai: ubah dari Total_Score menjadi nilai
- Ubah target file dari `dataset_siswa.csv` menjadi `data.csv`

```py
df = pd.read_csv("./data/dataset_siswa.csv")
```

```py
df = pd.read_csv("./data/data.csv")
```

- Simpan file hasil edit, lalu jalankan notebook seperti biasa.
- Jika menggunakan data yang sudah dimanipulasi (`dataset_siswa.csv`):
  - Tidak perlu mengubah apapun, cukup jalankan notebook.
