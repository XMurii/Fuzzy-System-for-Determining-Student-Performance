# Penjelasan Sistem Fuzzy Penilaian (Mamdani & Sugeno)

## Deskripsi Umum

Kode ini merupakan implementasi sistem penilaian berbasis fuzzy logic menggunakan dua metode: **Mamdani** dan **Sugeno**. Sistem ini digunakan untuk menentukan nilai akhir dan grade mahasiswa berdasarkan total nilai QUIZ, UJIAN, dan TUGAS (masing-masing hasil penjumlahan 4 CLO, range 0–400).

## Bobot Penilaian

- **QUIZ**: (CLO1 + CLO2 + CLO3 + CLO4) × 5% (maksimal 20)
- **UJIAN**: (CLO1 + CLO2 + CLO3 + CLO4) × 12.5% (maksimal 50)
- **TUGAS**: (CLO1 + CLO2 + CLO3 + CLO4) × 7.5% (maksimal 30)
- **Total Nilai Maksimal**: 100

## 1. Fuzzy Mamdani

### a. Definisi Variabel

- **Input**: quiz, exam, assignment (range 0–400)
- **Output**: final_score (range 0–100)

### b. Fungsi Keanggotaan

- Input (quiz, exam, assignment): low, medium, high (dengan trimf pada range 0–400)
- Output (final_score): F, D, C, B, A (dengan trimf pada range 0–100)

### c. Aturan Fuzzy

Contoh aturan:

- Jika quiz, exam, assignment **high** → final_score **A**
- Jika salah satu **low** → final_score **F**
- Kombinasi lain menghasilkan B, C, D

### d. Proses

- Input nilai quiz, exam, assignment (0–400)
- Sistem fuzzy menghasilkan nilai akhir (defuzzifikasi)
- Nilai akhir dikonversi ke grade:
  - > = 80: A
  - > = 70: AB
  - > = 65: B
  - > = 60: BC
  - > = 50: C
  - > = 40: D
  - < 40: E

## 2. Fuzzy Sugeno

### a. Fungsi Keanggotaan

- Sama seperti Mamdani (low, medium, high)

### b. Aturan Sugeno

- Output aturan berupa fungsi linear:  
  `nilai_akhir = (quiz/400)*20 + (exam/400)*50 + (assignment/400)*30`
- Nilai akhir dihitung dengan weighted average dari semua aturan yang aktif.

### c. Proses

- Input nilai quiz, exam, assignment (0–400)
- Sistem fuzzy menghasilkan nilai akhir (langsung crisp)
- Nilai akhir dikonversi ke grade (aturan sama seperti Mamdani)

## 3. Output

Kode akan menampilkan:

- Nilai akhir (Mamdani) dan grade-nya
- Nilai akhir (Sugeno) dan grade-nya

## 4. Perbedaan Mamdani & Sugeno

- **Mamdani**: Output aturan berupa fuzzy set, perlu defuzzifikasi.
- **Sugeno**: Output aturan berupa fungsi matematis, hasil langsung crisp.

---

**Contoh Output:**

```
Nilai akhir (Mamdani) : 78.45
Grade Mamdani: AB
Nilai akhir (Sugeno) : 80.25
Grade Sugeno: A
```
