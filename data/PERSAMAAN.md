
# Pembentukan Persamaan Hubungan Debit dan Kedalaman Aliran serta Penyelesaian Numerik

## 1. Pembentukan Persamaan Debit dan Kedalaman Aliran

Hubungan antara debit aliran (Q) dan kedalaman aliran (y) pada saluran irigasi trapesium ditentukan menggunakan persamaan Manning. Persamaan ini digunakan karena aliran diasumsikan seragam permanen dengan nilai kekasaran saluran yang konstan.

Persamaan Manning:

Q = (1/n) * A * R^(2/3) * S^(1/2)

Parameter desain:

- Lebar dasar saluran (b) = 1,0 m
- Kemiringan talud (m) = 1,0
- Kemiringan dasar (S) = 0,0005
- Koefisien Strickler (k) = 70 m^(1/3)/s

Koefisien Manning:

n = 1/k = 1/70 = 0,014286

Luas penampang basah:

A = (b + m*y)*y

A = (1+y)*y

A = y+y^2

Keliling basah:

P = b + 2*y*sqrt(1+m^2)

P = 1 + 2*sqrt(2)*y

Jari-jari hidraulis:

R = A/P

R = (y+y^2)/(1+2*sqrt(2)*y)

Dengan substitusi seluruh parameter ke persamaan Manning diperoleh:

Q = (1/0,014286)*(y+y^2)*
    ((y+y^2)/(1+2*sqrt(2)*y))^(2/3)*
    sqrt(0,0005)

Setelah penyederhanaan:

Q(y) = 1,5652476*(y+y^2)*
       ((y+y^2)/(1+2,8284271*y))^(2/3)

Persamaan tersebut merupakan persamaan nonlinear yang menghubungkan debit dengan kedalaman aliran.

## 2. Penyelesaian Persamaan Secara Numerik

Untuk memperoleh kedalaman aliran berdasarkan debit yang diketahui, persamaan disusun menjadi:

f(y) = Q(y) - Q_target = 0

Penyelesaian dilakukan menggunakan metode Bisection atau metode bagi dua.

Tahapan penyelesaian:

1. Menentukan interval awal kedalaman antara 0 sampai 0,9 m.
2. Menghitung nilai tengah interval.
3. Memasukkan nilai tengah ke persamaan debit Manning.
4. Menghitung residual antara debit hasil perhitungan dan debit target.
5. Memperbarui interval berdasarkan tanda residual.
6. Mengulangi proses sampai memenuhi toleransi 10^-8.

## 3. Hasil Penyelesaian Numerik

### 3.1 Hasil Kelompok Kalibrasi

| Debit Q (m³/s) | Kedalaman y (m) |
|---:|---:|
| 0,150 | 0,242840 |
| 0,200 | 0,286777 |
| 0,300 | 0,361305 |
| 0,400 | 0,424471 |
| 0,500 | 0,480122 |
| 0,600 | 0,530314 |
| 0,800 | 0,618937 |
| 1,000 | 0,696329 |

Kelompok kalibrasi digunakan untuk membangun hubungan antara debit dan kedalaman aliran.

### 3.2 Hasil Kelompok Pengujian

| Debit Q (m³/s) | Kedalaman y (m) |
|---:|---:|
| 0,175 | 0,265533 |
| 0,250 | 0,325829 |
| 0,350 | 0,394006 |
| 0,450 | 0,453082 |
| 0,550 | 0,505809 |
| 0,700 | 0,576306 |
| 0,900 | 0,658799 |

Kelompok pengujian tidak digunakan dalam pembentukan kurva kalibrasi. Data ini digunakan sebagai pembanding untuk mengevaluasi ketelitian model interpolasi.

## 4. Evaluasi Parameter Hidraulika

Kecepatan aliran:

V = Q/A

Bilangan Froude:

Fr = V/sqrt(g*A/T)

Hasil perhitungan menunjukkan:

- Kecepatan aliran: 0,497–0,847 m/s.
- Bilangan Froude: 0,352–0,385.
- Kedalaman maksimum: 0,696329 m.

Tinggi jagaan pada debit maksimum:

F = H-y

F = 0,90-0,696329

F = 0,203671 m

Hasil tersebut memenuhi kriteria KP-03:

- Kecepatan maksimum 3 m/s.
- Bilangan Froude kurang dari 0,55.
- Tinggi jagaan minimum 0,20 m.

## 5. Kesimpulan

Berdasarkan pembentukan persamaan Manning dan penyelesaian secara numerik menggunakan metode Bisection, diperoleh persamaan nonlinear yang menghubungkan debit dan kedalaman aliran pada saluran irigasi trapesium pasangan beton.

Kedalaman normal meningkat dari 0,242840 m pada debit 0,15 m³/s menjadi 0,696329 m pada debit 1,00 m³/s.

Seluruh hasil perhitungan memenuhi kriteria kecepatan maksimum, bilangan Froude, dan tinggi jagaan berdasarkan parameter perencanaan KP-03.

Data kalibrasi selanjutnya digunakan untuk membangun model interpolasi, sedangkan data pengujian digunakan untuk mengevaluasi tingkat ketelitian model tersebut.
