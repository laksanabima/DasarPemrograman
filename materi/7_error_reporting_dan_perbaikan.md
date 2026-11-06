## Universitas Harkat Negeri
### SIF3002 — Dasar Pemrograman

Bima Laksana Putra, S.ST., M.M.

# SYNTAX ERROR, ERROR REPORTING, KLASIFIKASI, DAN PERBAIKAN ERROR

# Capaian Pembelajaran

Setelah mempelajari materi ini, mahasiswa diharapkan mampu:

1. Membedakan syntax error, runtime error, dan logic error.
2. Membaca dan memahami pesan error (traceback) dari interpreter Python.
3. Menentukan letak error berdasarkan pesan error.
4. Mengklasifikasikan jenis error berdasarkan gejalanya.
5. Memperbaiki error umum dalam program sederhana.
6. Menelusuri logic error menggunakan pengujian dan trace.

## Review Materi Sebelumnya

Kita sudah mampu menulis program dengan array (list), string, input-output, dan format output. Saat menjalankan program, kadang muncul **error**. Pertemuan ini kita belajar **membaca, mengklasifikasi, dan memperbaiki** error tersebut.

> Error bukan musuh. Pesan error memberitahu kita apa yang salah dan di mana letaknya.

# 1. Tiga Jenis Error

| Jenis | Kapan terjadi | Ciri | Contoh |
| ---- | ---- | ---- | ---- |
| Syntax error | Sebelum program dijalankan | Program tidak mau jalan | Kurang tanda titik dua `:` |
| Runtime error | Saat program dijalankan | Program berhenti di tengah | Membagi dengan nol |
| Logic error | Program selesai, hasil salah | Tidak ada pesan error | Operator `>` tertulis `<` |

## 1.1 Syntax Error

Kesalahan **penulisan** yang melanggar aturan bahasa. Interpreter tidak dapat memahami program.

```python
nilai = 75
if nilai >= 60
    print("Lulus")
```

Kurang tanda titik dua setelah kondisi. Pesan error:

```
SyntaxError: expected ':'
```

## 1.2 Runtime Error

Kesalahan yang terjadi **saat program berjalan**. Program berhenti di tengah karena melakukan operasi yang tidak valid.

```python
nilai = 75
print(nilai / 0)
```

Pesan error:

```
ZeroDivisionError: division by zero
```

## 1.3 Logic Error

Program berjalan tanpa error, tetapi **hasilnya salah**. Kesalahan ada pada logika, bukan penulisan.

```python
nilai = 75

if nilai > 60:
    print("Lulus")
else:
    print("Belum lulus")
```

> Program berjalan normal, tetapi mahasiswa dengan nilai tepat `60` akan dianggap "Belum lulus". Seharusnya `>=` bukan `>`.

# 2. Membaca Pesan Error (Traceback)

Saat runtime error terjadi, Python menampilkan **traceback**.

```python
def bagi(a, b):
    return a / b

print(bagi(10, 0))
```

Pesan error:

```
Traceback (most recent call last):
  File "program.py", line 4, in <module>
    print(bagi(10, 0))
  File "program.py", line 2, in bagi
    return a / b
ZeroDivisionError: division by zero
```

Cara membaca:

| Bagian | Arti |
| ---- | ---- |
| `ZeroDivisionError` | Jenis error |
| `division by zero` | Penyebab singkat |
| `File "program.py", line 2` | Lokasi file dan nomor baris |
| `return a / b` | Baris yang bermasalah |

> Baca **dari baris paling bawah** — di situlah jenis error dan penyebabnya ditampilkan.

# 3. Klasifikasi dan Perbaikan Error Umum

| Jenis error | Penyebab umum | Contoh | Perbaikan |
| ---- | ---- | ---- | ---- |
| `SyntaxError` | Penulisan salah | Kurang `:` | Tambahkan `:` |
| `IndentationError` | Indentasi tidak konsisten | Spasi campur tab | Rapikan indentasi |
| `NameError` | Variabel belum didefinisikan | `print(nama)` | Definisikan variabel dulu |
| `TypeError` | Operasi antar tipe tidak cocok | `"Umur: " + 20` | Gunakan `str(20)` atau f-string |
| `ValueError` | Konversi tipe gagal | `int("abc")` | Pastikan input berupa angka |
| `IndexError` | Indeks di luar jangkauan | `list[5]` pada list 5 elemen | Cek panjang list |
| `ZeroDivisionError` | Membagi dengan nol | `x / 0` | Periksa pembagi ≠ 0 |

# 4. Strategi Memperbaiki Error

1. **Baca pesan error** sampai tuntas.
2. **Kenali jenis error** dan penyebabnya.
3. **Buka lokasi** (file dan nomor baris) yang disebut.
4. **Periksa baris tersebut** dan baris di sekitarnya.
5. **Perbaiki**, jalankan ulang, lalu uji kembali.

> Perbaiki error **yang muncul paling awal**. Satu error sering memicu error berikutnya.

# 5. Tips Menelusuri Logic Error

Logic error tidak menampilkan pesan. Gunakan cara berikut:

1. **Trace table** — catat nilai variabel langkah demi langkah.
2. **`print()` sementara** — tampilkan nilai variabel di titik penting.

```python
total = 0

for angka in [10, 20, 30]:
    total = total + angka
    print(f"angka={angka}, total={total}")
```

3. **Uji kasus batas** — gunakan nilai di ambang syarat (misalnya `60` pada kelulusan).

# Kuis Cepat

Tentukan **jenis error** untuk setiap program berikut.

**1.**

```python
print(nama)
```

**2.**

```python
print("Umur: " + 20)
```

**3.**

```python
daftar = [1, 2, 3]
print(daftar[5])
```

**4.**

```python
nilai = 75
if nilai >= 60
    print("Lulus")
```

**5.**

```python
print(10 / 0)
```

**6.**

```python
umur = int("dua puluh")
```

**7.** Program kelulusan berjalan tanpa error, tetapi nilai `60` dianggap tidak lulus. Termasuk jenis error apa?

# Tugas

## Latihan 1: Klasifikasi Error

Untuk setiap program berikut, tentukan jenis errornya dan tuliskan perbaikannya.

```python
# Program A
nama = "Supardi Toyib"
print(nama + umur)
```

```python
# Program B
for i in range(3)
    print(i)
```

```python
# Program C
daftar = [10, 20, 30]
print(daftar[3])
```

## Latihan 2: Perbaiki Program

Perbaiki program berikut agar berjalan benar.

```python
nilai = int(input("Masukkan nilai: ")

if nilai >= 60:
print("Lulus")
else:
    print("Belum lulus")
```

## Latihan 3: Temukan Logic Error

Program berikut bertujuan menghitung rata-rata. Program berjalan tanpa error, tetapi hasilnya salah. Temukan dan perbaiki logic error-nya.

```python
nilai = [80, 90, 75]
total = sum(nilai)
rata_rata = total / 4
print(rata_rata)
```

## Ketentuan

1. Dikerjakan secara individu.
2. Tuliskan jenis error, penyebab, dan perbaikan untuk setiap kasus.
3. Perbaikan harus berupa kode yang benar dan dapat dijalankan.
4. Kumpulkan hasil (screenshot program yang sudah berjalan benar) beserta file kodenya.
