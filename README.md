# Proyek Sistem Fuzzy untuk Penilaian Performa Siswa
### Mahasiswa diharapkan setidaknya melakukan hal-hal berikut: 
- Prapemrosesan data untuk memastikan kualitas dataset, seperti pemilihan fitur, penanganan missing value, dll. 
- Mengimplementasikan Fuzzy System menggunakan metode Mamdani dan Sugeno 
- Mengevaluasi kinerja Fuzzy System metode Mamdani dan Sugeno pada dataset studi kasus. Gunakan metrik evaluasi seperti akurasi, F1-score, atau metrik lain yang sesuai. Bandingkan kinerja metode Mamdani dan Sugeno, dan lakukan analisis. 
- Bahasa pemrograman yang digunakan adalah Python. Jika mahasiswa membuat Fuzzy System 
tanpa library maka akan menjadi nilai tambah dalam Tugas Besar ini.

## DATA
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

## FITUR
### Input (Antecedents)
- `Attendance` 
    - Rentang [0 - 100] %
    - Fuzzy Set
        - low: Triangular dengan titik [0, 0, 50]
        - medium: Triangular dengan titik [0, 50, 100]
        - high: Triangular dengan titik [50, 100, 100]
        
- `Total_Score` (0 - 100)
    - Rentang [0 - 100] 
    - Fuzzy Set
        - low: Triangular dengan titik [0, 0, 50]
        - medium: Triangular dengan titik [0, 50, 100]
        - high: Triangular dengan titik [50, 100, 100]

- `Projects_Score` (0 - 100)
    - Rentang [0 - 100] 
    - Fuzzy Set
        - few: Triangular dengan titik [0, 0, 50]
        - average: Triangular dengan titik [0, 50, 100]
        - many: Triangular dengan titik [50, 100, 100]

- Output berupa nilai crisp `Performa_Siswa` (0-100)
    - Rentang [0 - 100] 
    - Fuzzy Set
        - poor: Triangular dengan titik [0, 0, 50]
        - average: Triangular dengan titik [0, 50, 100]
        - good: Triangular dengan titik [50, 100, 100]

---

### 📋 Tabel Aturan Fuzzy: `Attendance` × `Total_Score` × `Projects_Score` → `Performa_Siswa`
| No. | Attendance | Total\_Score | Projects\_Score | Performa\_Siswa |
| --- | ---------- | ------------ | --------------- | --------------- |
| 1   | low        | low          | few             | poor            |
| 2   | low        | low          | average         | poor            |
| 3   | low        | low          | many            | average         |
| 4   | low        | medium       | few             | poor            |
| 5   | low        | medium       | average         | average         |
| 6   | low        | medium       | many            | average         |
| 7   | low        | high         | few             | average         |
| 8   | low        | high         | average         | average         |
| 9   | low        | high         | many            | good            |
| 10  | medium     | low          | few             | poor            |
| 11  | medium     | low          | average         | average         |
| 12  | medium     | low          | many            | average         |
| 13  | medium     | medium       | few             | average         |
| 14  | medium     | medium       | average         | average         |
| 15  | medium     | medium       | many            | good            |
| 16  | medium     | high         | few             | average         |
| 17  | medium     | high         | average         | good            |
| 18  | medium     | high         | many            | good            |
| 19  | high       | low          | few             | average         |
| 20  | high       | low          | average         | average         |
| 21  | high       | low          | many            | good            |
| 22  | high       | medium       | few             | average         |
| 23  | high       | medium       | average         | good            |
| 24  | high       | medium       | many            | good            |
| 25  | high       | high         | few             | good            |
| 26  | high       | high         | average         | good            |
| 27  | high       | high         | many            | good            |


## Struktur Proyek
```bash
.
├── README.md
├── student_performance_fuzzy_system.ipynb
└── data/                               
    └── student_data.csv               


