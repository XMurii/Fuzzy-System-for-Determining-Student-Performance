## Jumlah Nilai Linguistik untuk setiap Atribut
- **Absensi:** 3 nilai linguistik
    - Rendah
    - Sedang
    - Tinggi

- **Nilai:** 3 nilai linguistik
    - Rendah
    - Sedang
    - Tinggi

- **Performa(output):** 3 nilai linguistik
    - Rendah
    - Sedang
    - Tinggi

## Fungsi Keanggotaan/Membership
Didefinisikan dengan fungsi Gaussian:
```py
def gaussian_membership(x, center, sigma):
    return np.exp(-0.5 * ((x - center) / sigma) ** 2)
```
- Untuk Absensi:
    - Rendah: center=0, sigma=15
    - Sedang: center=50, sigma=15
    - Tinggi: center=100, sigma=15
- Untuk Nilai:
    - Rendah: center=0, sigma=15
    - Sedang: center=50, sigma=15
    - Tinggi: center=100, sigma=15