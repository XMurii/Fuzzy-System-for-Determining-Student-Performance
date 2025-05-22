# Penjelasan Sistem Fuzzy pada `sistem_fuzzy_performa_siswa.ipynb`

## 1. **Pendahuluan**
Sistem fuzzy adalah metode kecerdasan buatan yang digunakan untuk menangani data yang tidak pasti atau samar (fuzzy). Pada proyek ini, sistem fuzzy digunakan untuk menilai performa siswa berdasarkan dua kriteria utama: **absensi** dan **nilai**. Dua metode fuzzy yang digunakan adalah **Mamdani** dan **Sugeno**.

---

## 2. **Prapemrosesan Data**

### a. **Mengimpor Dataset**
Dataset siswa diimpor dari file CSV:
```python
df = pd.read_csv("data/dataset_siswa.csv")
```

### b. **Penanganan Missing Value**
- Dicek apakah ada nilai kosong (missing value) pada kolom `absensi` dan `nilai`.
- Jika ada, nilai kosong diisi dengan rata-rata kolom tersebut.
```python
df['absensi'] = df['absensi'].fillna(df['absensi'].mean())
df['nilai'] = df['nilai'].fillna(df['nilai'].mean())
```

### c. **Statistik dan Informasi Data**
- Menampilkan info dataset dan statistik deskriptif untuk memastikan data sudah bersih dan siap diproses.

### d. **Kategorisasi Performa**
- Fungsi `categorize_performance` digunakan untuk mengelompokkan performa siswa menjadi tiga kategori: **Buruk**, **Cukup**, dan **Bagus** berdasarkan nilai dan absensi.
```python
def categorize_performance(row):
    if row['nilai'] < 50 and row['absensi'] < 50:
        return 'Buruk'
    elif (50 <= row['nilai'] <= 75) or (50 <= row['absensi'] <= 75):
        return 'Cukup'
    elif row['nilai'] > 75 and row['absensi'] > 75:
        return 'Bagus'
```
- Hasil kategorisasi disimpan di kolom baru `performa`.

---

## 3. **Implementasi Sistem Fuzzy**

### a. **Fungsi Keanggotaan Gaussian**
- Fungsi keanggotaan Gaussian digunakan untuk menentukan derajat keanggotaan suatu nilai pada kategori tertentu (rendah, sedang, tinggi).
```python
def gaussian_membership(x, center, sigma):
    return np.exp(-0.5 * ((x - center) / sigma) ** 2)
```

### b. **Metode Mamdani**
- Menggunakan aturan berbasis threshold dan fungsi keanggotaan Gaussian.
- Output langsung berupa label kategori (`Buruk`, `Cukup`, `Bagus`).
```python
def mamdani(absensi, nilai):
    absensi_rendah = gaussian_membership(absensi, 0, 15)
    absensi_sedang = gaussian_membership(absensi, 50, 15)
    absensi_tinggi = gaussian_membership(absensi, 100, 15)
    nilai_buruk = gaussian_membership(nilai, 0, 15)
    nilai_cukup = gaussian_membership(nilai, 50, 15)
    nilai_bagus = gaussian_membership(nilai, 100, 15)
    if absensi_rendah > 0.5 and nilai_buruk > 0.5:
        return "Buruk"
    elif absensi_tinggi > 0.5 and nilai_bagus > 0.5:
        return "Bagus"
    elif absensi_sedang > 0.5 and nilai_cukup > 0.5:
        return "Cukup"
    else:
        return "Cukup"
```

### c. **Metode Sugeno**
- Juga menggunakan fungsi keanggotaan Gaussian, namun output berupa angka (0 = Buruk, 0.5 = Cukup, 1 = Bagus).
- Output numerik ini kemudian dikonversi ke label kategori untuk evaluasi.
```python
def sugeno(absensi, nilai):
    absensi_rendah = gaussian_membership(absensi, 0, 15)
    absensi_sedang = gaussian_membership(absensi, 50, 15)
    absensi_tinggi = gaussian_membership(absensi, 100, 15)
    nilai_buruk = gaussian_membership(nilai, 0, 15)
    nilai_cukup = gaussian_membership(nilai, 50, 15)
    nilai_bagus = gaussian_membership(nilai, 100, 15)
    if absensi_rendah > 0.5 and nilai_buruk > 0.5:
        return 0  # Buruk
    elif absensi_tinggi > 0.5 and nilai_bagus > 0.5:
        return 1  # Bagus
    elif absensi_sedang > 0.5 and nilai_cukup > 0.5:
        return 0.5  # Cukup
    else:
        return 0.5  # Cukup
```

---

## 4. **Evaluasi Kinerja Sistem Fuzzy**

### a. **Prediksi**
- Sistem fuzzy Mamdani dan Sugeno digunakan untuk memprediksi performa setiap siswa.
- Hasil prediksi disimpan di kolom baru.

### b. **Konversi Output Sugeno**
- Output numerik Sugeno dikonversi ke label kategori agar bisa dibandingkan dengan data asli.

### c. **Metrik Evaluasi**
- Digunakan **Akurasi** dan **F1-Score** untuk mengukur kinerja model.
- Fungsi evaluasi:
```python
def evaluate_model(predictions, actual):
    accuracy = accuracy_score(actual, predictions)
    f1 = f1_score(actual, predictions, average='weighted', labels=['Buruk', 'Cukup', 'Bagus'], zero_division=1)
    return accuracy, f1
```

### d. **Perbandingan Hasil**
- Hasil evaluasi Mamdani dan Sugeno dibandingkan secara langsung.
- Ditampilkan akurasi dan F1-score masing-masing metode.

---

## 5. **Analisis Hasil**

- **Perbedaan utama** antara Mamdani dan Sugeno adalah pada bentuk output dan cara pengambilan keputusan.
- **Mamdani** menghasilkan label kategori langsung, sehingga lebih sederhana dan cocok jika aturan sudah sesuai dengan pola data.
- **Sugeno** menghasilkan output numerik, yang lebih fleksibel namun perlu dikonversi ke label untuk evaluasi.
- Jika Mamdani lebih baik, kemungkinan aturan fuzzy Mamdani lebih cocok dengan distribusi data.
- Jika Sugeno lebih baik, berarti model numerik Sugeno lebih mampu menangkap variasi data.
- **Parameter fungsi keanggotaan** (misal, nilai sigma pada Gaussian) dan **aturan fuzzy** sangat mempengaruhi hasil akhir.
- Untuk meningkatkan kinerja, aturan fuzzy dan parameter fungsi keanggotaan bisa dioptimasi lebih lanjut, misal dengan eksperimen nilai sigma atau menambah aturan fuzzy.

---

## 6. **Kesimpulan**

- Sistem fuzzy berbasis Mamdani dan Sugeno dapat digunakan untuk menilai performa siswa secara otomatis.
- Proses prapemrosesan data sangat penting untuk memastikan hasil yang akurat.
- Evaluasi menggunakan metrik akurasi dan F1-score membantu memilih metode terbaik untuk kasus yang dihadapi.
- Sistem ini dapat dikembangkan lebih lanjut dengan menambah fitur, mengoptimasi aturan, atau menggunakan metode fuzzy lain.

---
