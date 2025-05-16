# Penjelasan Kode Sistem Fuzzy untuk Perhitungan Nilai

## 1. Pendahuluan
Kode ini mengimplementasikan sistem fuzzy untuk menghitung nilai akhir berdasarkan tiga komponen: nilai kuis, nilai ujian, dan nilai tugas. Sistem fuzzy yang digunakan adalah metode Mamdani dan Sugeno.

---

## 2. Metode Mamdani

### 2.1 Definisi Variabel Input dan Output
- **Input**: `quiz`, `exam`, dan `assignment` dengan rentang nilai dari 0 hingga 100.
- **Output**: `final_score` dengan rentang nilai dari 0 hingga 100.

### 2.2 Fungsi Keanggotaan Input
Untuk tiap input dibuat 3 fungsi keanggotaan menggunakan fungsi triangular (trimf):
- `low` (rendah): nilai di bawah 50
- `medium` (sedang): nilai antara sekitar 30 sampai 70
- `high` (tinggi): nilai di atas 50

### 2.3 Fungsi Keanggotaan Output
Output `final_score` memiliki fungsi keanggotaan dengan label grade:
- `F` (gagal): 0 - 50
- `D`: 40 - 60
- `C`: 50 - 70
- `B`: 65 - 85
- `A`: 80 - 100

### 2.4 Aturan Fuzzy (Rule Base)
Contoh aturan:
- Jika `quiz` tinggi, `exam` tinggi, dan `assignment` tinggi, maka `final_score` adalah `A`.
- Jika salah satu nilai rendah, maka `final_score` adalah `F`.
- Aturan-aturan lain sesuai kombinasi nilai.

### 2.5 Penggunaan dan Simulasi
Input nilai diberikan:
```python  
final_sim.input['quiz'] = 75  
final_sim.input['exam'] = 80  
final_sim.input['assignment'] = 70
```
Hasil output defuzzifikasi berupa nilai akhir.

## 3. Metode Sugeno
### 3.1 Fungsi Keanggotaan
Fungsi keanggotaan low, medium, dan high dibuat secara manual untuk tiap input.

### 3.2 Aturan Fuzzy
Setiap aturan memiliki bobot (degree of membership) dan fungsi linear untuk outputnya, misal:
```bash
Output = 0.5*quiz + 0.3*exam + 0.2*assignment
```
### 3.3 Proses Perhitungan
Output dihitung dengan rata-rata terbobot (weighted average) berdasarkan bobot aturan dan fungsi linear.

### 3.4 Contoh Penggunaan
Input nilai yang sama digunakan untuk menghitung nilai akhir metode Sugeno.

---

## 4. Kesimpulan
- **Mamdani** memberikan pendekatan berbasis inferensi fuzzy dengan fungsi keanggotaan lengkap dan defuzzifikasi.
- **Sugeno** menggunakan fungsi linear pada aturan, cocok untuk model yang ingin output numerik lebih langsung dan perhitungan lebih cepat.

---


## 5. Cara Menggunakan
1. Ganti nilai input `quiz`, `exam`, dan `assignment` dalam kode sesuai data Anda.
2. Jalankan script Python.
3. Lihat hasil nilai akhir dari kedua metode.
Jika ingin dikembangkan mengolah data dari file Excel secara batch, saya dapat bantu buatkan juga.

---

Catatan:
Kode menggunakan library scikit-fuzzy untuk metode Mamdani. Install dengan:

```bash
pip install scikit-fuzzy
```

Kalau Anda butuh file MD nya saya siapkan untuk di-download juga, silakan beri tahu!