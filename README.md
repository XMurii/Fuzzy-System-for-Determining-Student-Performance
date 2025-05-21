# Proyek Sistem Fuzzy untuk Penilaian Performa Siswa
## Gambaran Umum

Proyek ini mengimplementasikan sistem inferensi fuzzy untuk menilai performa siswa berdasarkan beberapa parameter akademik dan non-akademik. Sistem ini dirancang menggunakan dua metode inferensi fuzzy yang populer: Mamdani dan Sugeno. Tujuan dari proyek ini adalah untuk menyediakan alat yang fleksibel dan interpretatif untuk mengevaluasi performa siswa, yang dapat membantu pendidik dalam mengidentifikasi siswa yang membutuhkan perhatian lebih atau pengakuan atas kinerja yang luar biasa.

## Latar Belakang

Penilaian performa siswa seringkali melibatkan banyak faktor subjektif dan objektif. Sistem fuzzy logic adalah pendekatan yang cocok untuk masalah seperti ini karena kemampuannya untuk menangani ketidakpastian dan informasi yang tidak presisi, serta memodelkan penalaran manusia yang berdasarkan aturan "IF-THEN".

Dataset yang digunakan untuk proyek ini memiliki kolom-kolom berikut:
- `Student_ID`
- `First_Name`, `Last_Name`
- `Email`
- `Gender`, `Age`
- `Department`
- `Attendance (%)`
- `Midterm_Score`, `Final_Score`
- `Assignments_Avg`, `Quizzes_Avg`
- `Participation_Score`, `Projects_Score`
- `Total_Score`, `Grade`
- `Study_Hours_Per_Week`
- `Extracurricular_Activities`
- `Internet_Access_at_Home`
- `Parent_Education_Level`
- `Family_Income_Level`
- `Stress_Level`
- `Sleep_Hours_Per_Night`

Beberapa isu dalam dataset:

- `Missing values` (nulls) di beberapa catatan.
- `Bias` dalam data (misalnya, siswa dengan kehadiran tinggi cenderung mendapat nilai sedikit lebih baik).
- `Imbalanced distributions` (misalnya, beberapa departemen memiliki lebih banyak siswa).

## Fitur

- Implementasi sistem fuzzy menggunakan Metode Mamdani.
- Implementasi sistem fuzzy menggunakan Metode Sugeno (Orde 0).
- Input yang disederhanakan untuk kemudahan implementasi:
    - `Kehadiran`: Persentase kehadiran siswa (0-100%).
    - `Nilai_Akademik`: Rata-rata nilai akademik (gabungan Midterm, Final, Assignments, Quizzes) (0-100).
    - `Partisipasi_Proyek`: Rata-rata nilai partisipasi dan proyek (0-100).
- Output berupa nilai crisp `Performa_Siswa` (0-100), di mana 0 adalah performa sangat buruk dan 100 adalah performa sangat baik.
- Dapat dengan mudah dikustomisasi untuk penyesuaian fungsi keanggotaan dan aturan fuzzy.

## Struktur Proyek
```bash
.
├── README.md
├── student_performance_fuzzy_system.ipynb
└── data/                               
    └── student_data.csv               

```

## Persyaratan Sistem

Proyek ini membutuhkan Python dan beberapa pustaka:
- Python 3.x
- numpy
- scikit-fuzzy (skfuzzy)
- matplotlib (untuk visualisasi opsional)

Anda dapat menginstal dependensi ini menggunakan pip:
```bash
pip install numpy scikit-fuzzy matplotlib
```
