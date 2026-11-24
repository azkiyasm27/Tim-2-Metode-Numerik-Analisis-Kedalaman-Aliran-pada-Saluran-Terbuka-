# Parameter Saluran dan Acuan Referensi

## 1. Gambaran Saluran

Saluran irigasi pasangan beton berpenampang trapesium pada skala saluran kecil (debit 0,15 sampai 1,0 m^3/s).
Aliran dianggap seragam permanen (kedalaman normal), saluran trapesium, dan kekasaran dinding konstan
terhadap kedalaman. Perancangan mengikuti kriteria pasangan beton pada Standar Perencanaan Irigasi KP-03.

## 2. Parameter dan Sumbernya

| Parameter | Simbol | Nilai | Dasar Penentuan | Sumber |
|---|---|---|---|---|
| Bentuk penampang | - | Trapesium | Bentuk penampang saluran irigasi pada KP-03 | KP-03 Bab IV |
| Koefisien kekasaran | k | 70 m^(1/3)/s | Pasangan beton, nilai yang dianjurkan | KP-03 subbab 4.3.2, hlm. 54 |
| Manning | n = 1/k | 0,0143 | Konversi dari Strickler; masuk rentang beton finishing troweled 0,011 sampai 0,015 (nilai normal 0,013) | KP-03 hlm. 54; Chow (1959) Tabel 5-6 |
| Kemiringan Talud | m | 1,0 (1:1) | Saluran pasangan dengan h < 0,75 m: talud 1,00 pada Tabel 4-3 | KP-03 Tabel 4-3, hlm. 55 |
| Lebar dasar | b | 1,0 m | Pilihan tim; b/h = 1,44 pada Q maks, sejalan dengan rentang b/h 1,3 sampai 1,5 untuk Q 0,75 sampai 1,00 m^3/s | KP-03 Tabel A.2.1, hlm. 116 |
| Kemiringan dasar | S | 0,0005 | Pilihan tim; sejalan dengan orde kemiringan 0,00046 sampai 0,00056 pada profil saluran Q 0,30 sampai 0,75 m^3/s; menjaga Froude < 0,55 | KP-03 Tabel A.2.2, hlm. 117 |
| Tinggi jagaan minimum | F1 | 0,20 m | Pasangan, Q 0,5 sampai 1,5 m^3/s | KP-03 Tabel 4-4, hlm. 56 |
| Tinggi saluran | H | 0,9 m | y pada Q = 1,0 (0,696 m) ditambah jagaan 0,20 m, dibulatkan | turunan dari parameter di atas |
| Percepatan gravitasi | g | 9,81 m/s^2 | Konstanta fisika | standar |

Catatan: KP-03 memakai koefisien Strickler k, sedangkan model Manning memakai n. Keduanya berkebalikan, n = 1/k.

## 3. Daftar Simbol dan Keterangan

### Data masukan

| Simbol | Nama | Satuan | Keterangan |
|---|---|---|---|
| Q | Debit aliran | m^3/s | Volume air yang lewat di saluran setiap detik. Ini data yang diketahui dari skenario |
| b | Lebar dasar saluran | m | Lebar bagian bawah saluran yang datar |
| m | Kemiringan talud | - | Dinding saluran miring. Nilai m = 1 berarti setiap naik 1 m ke atas, dinding bergeser 1 m ke samping |
| S | Kemiringan dasar saluran | m/m | Turunnya dasar saluran untuk setiap 1 m panjang. Di KP-03 simbol ini ditulis I |
| k | Koefisien Strickler | m^(1/3)/s | Ukuran kehalusan dinding menurut KP-03. Makin besar k, makin halus dinding |
| n | Koefisien Manning | s/m^(1/3) | Ukuran kekasaran dinding. Makin besar n, makin kasar dinding. Hubungannya dengan Strickler adalah n = 1/k |
| H | Tinggi saluran | m | Jarak dari dasar sampai tepi atas saluran. Air yang melewati tinggi ini berarti meluap |
| g | Percepatan gravitasi | m/s^2 | Konstanta sebesar 9,81 |

### Besaran yang dicari atau dihitung

| Simbol | Nama | Satuan | Keterangan |
|---|---|---|---|
| y | Kedalaman aliran | m | Tinggi air di dalam saluran. Ini yang dicari dengan metode numerik. Di catatan Istiarto ditulis h |
| A | Luas penampang basah | m^2 | Luas bagian penampang yang terisi air, dihitung dari A = (b + m*y)*y |
| P | Keliling basah | m | Panjang dinding dan dasar yang bersentuhan dengan air, dihitung dari P = b + 2*y*sqrt(1 + m^2) |
| R | Jari jari hidrolis | m | Perbandingan luas dan keliling basah, R = A/P. Nilai ini menggambarkan seberapa efisien bentuk penampang |
| T | Lebar permukaan air | m | Lebar muka air bagian atas, T = b + 2*m*y |
| V | Kecepatan rata rata aliran | m/s | Kecepatan air, dihitung dari V = Q/A |
| Fr | Bilangan Froude | tanpa satuan | Ukuran ketenangan aliran. Nilai di bawah 1 berarti aliran tenang (subkritis). KP-03 menganjurkan di bawah 0,55 agar stabil |
| F1 | Tinggi jagaan | m | Sisa tinggi saluran di atas muka air. Dibutuhkan agar air tidak meluap saat debit naik sedikit |

## 4. Skenario Debit

Rentang 0,15 sampai 1,0 m^3/s mengikuti awal rentang debit pada Tabel A.2.1 KP-03 (mulai 0,15 m^3/s).
Kapasitas saluran pada y = H sekitar 1,65 m^3/s.

| Kelompok | Debit Q (m^3/s) | Fungsi |
|---|---|---|
| Kalibrasi | 0,15; 0,2; 0,3; 0,4; 0,5; 0,6; 0,8; 1,0 | Membangun kurva Q dan y |
| Uji | 0,175; 0,25; 0,35; 0,45; 0,55; 0,7; 0,9 | Tidak dipakai membangun kurva, untuk menguji galat interpolasi |

## 5. Pengecekan Terhadap Kriteria KP-03

| Kriteria | Batas KP-03 | Hasil desain | Status |
|---|---|---|---|
| Kecepatan maksimum pasangan beton | 3 m/s (subbab 4.3.1, hlm. 53) | 0,50 sampai 0,85 m/s | Terpenuhi |
| Bilangan Froude aliran subkritis stabil | kurang dari 0,55 (hlm. 53 sampai 54) | 0,35 sampai 0,38 | Terpenuhi |
| Talud pasangan, h < 0,75 m | 1,00 (Tabel 4-3) | m = 1,0, y maks = 0,70 m | Terpenuhi |
| Tinggi jagaan pasangan Q 0,5 sampai 1,5 | 0,20 m (Tabel 4-4) | H - y maks = 0,204 m | Terpenuhi |
| Tidak meluap | y < H | y maks = 0,696 m < 0,9 m | Terpenuhi |

## 6. Rujukan Hasil Perkiraan

| Q (m^3/s) | y (m) | V (m/s) | Froude |
|---|---|---|---|
| 0,15 | 0,243 | 0,50 | 0,35 |
| 0,3 | 0,361 | 0,63 | 0,36 |
| 0,5 | 0,480 | 0,74 | 0,37 |
| 0,8 | 0,619 | 0,82 | 0,38 |
| 1,0 | 0,696 | 0,85 | 0,38 |

## 7. Persamaan yang dipakai

```
Q = (1/n) * A * R^(2/3) * S^(1/2)
A = (b + m*y) * y
P = b + 2*y*sqrt(1 + m^2)
R = A / P
T = b + 2*m*y
V = Q / A
Fr = V / sqrt(g*A/T)
n = 1/k
```

## 8. Batasan Model

- Hanya aliran seragam permanen.
- n dianggap konstan terhadap kedalaman.
- Panjang saluran tidak dipakai karena Manning hanya bergantung pada penampang.
- b dan S adalah pilihan tim yang konsisten dengan KP-03, bukan data lapangan.

## 9. Referensi

1. Kementerian Pekerjaan Umum, Ditjen Sumber Daya Air (2013). Standar Perencanaan Irigasi, KP-03 Saluran.
2. Chow, V.T. (1959). Open-Channel Hydraulics. McGraw-Hill. Tabel 5-6.
3. Chapra, S.C. Applied Numerical Methods with MATLAB for Engineers and Scientists, 4th ed.
