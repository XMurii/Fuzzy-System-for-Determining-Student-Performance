# Penjelasan Sistem Fuzzy Penilaian (Mamdani & Sugeno)

## Deskripsi Umum

Kode ini merupakan implementasi sistem penilaian berbasis fuzzy logic menggunakan dua metode: **Mamdani** dan **Sugeno**. Sistem ini digunakan untuk menentukan nilai akhir dan grade mahasiswa berdasarkan total nilai QUIZ, UJIAN, dan TUGAS (masing-masing hasil penjumlahan 4 CLO, range 0–400).

## Bobot Penilaian

```bash
QUIZ :  (CLO1 + CLO2 + CLO3 + CLO4) * 5%
UJIAN:  (CLO1 + CLO2 + CLO3 + CLO4) * 12.5%
TUGAS:  (CLO1 + CLO2 + CLO3 + CLO4) * 7.5%

EXAMPLE
QUIZ  => (100 + 100 + 100 + 100) * 5%    = 20
UJIAN => (100 + 100 + 100 + 100) * 12.5% = 50
TUGAS => (100 + 100 + 100 + 100) * 7.5%  = 30

TOTAL NILAI = 100
```

```
Nilai akhir (Mamdani) : 78.45
Grade Mamdani: AB
Nilai akhir (Sugeno) : 80.25
Grade Sugeno: A
```
