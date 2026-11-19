## Universitas Harkat Negeri
### SIF3002 — Dasar Pemrograman

Bima Laksana Putra, S.ST., M.M.

# KUNCI JAWABAN — REFACTORING, OPTIMISASI, NAMING, COMMENT, DAN ORGANISASI KODE

> Dokumen ini berisi kunci jawaban kuis dan latihan pertemuan 9. Gunakan sebagai pembanding setelah mencoba mengerjakan sendiri.

# Kuis Cepat

**1.** Nama variabel yang lebih baik untuk menyimpan jumlah mahasiswa:

- **b) `jumlah_mahasiswa`**

Alasan: jelas menggambarkan isi, berupa kata benda, dan mengikuti `snake_case`. `jm` terlalu singkat, `data` terlalu umum.

**2.** Tujuan refactoring:

Refactoring adalah **memperbaiki struktur kode tanpa mengubah perilakunya**. Tujuannya: kode lebih mudah dibaca, mudah dipelihara, dan bebas duplikasi.

**3.** Penyederhanaan kode:

```python
total = sum(daftar)
```

**4.** Komentar yang lebih baik:

- **b) `# pindah ke mahasiswa berikutnya`**

Alasan: menjelaskan **maksud/alasan**, bukan mengulang apa yang sudah jelas dari kode.

**5.** Fungsi `if __name__ == "__main__":`:

Memastikan blok program utama (biasanya `main()`) **hanya dijalankan saat file dieksekusi langsung**, tidak saat file di-*import* sebagai modul oleh program lain.

**6.** Penulisan konstanta yang benar:

- **b) `BATAS_LULUS = 60`**

Konstanta ditulis dengan huruf besar dan garis bawah (`UPPER_CASE`).

**7.** Mengapa `500000` sebaiknya diganti konstanta:

Karena `500000` adalah *magic number* (angka ajaib). Menggantinya dengan konstanta memberi **nama/makna**, memudahkan dibaca, dan memudahkan perubahan nilai hanya di satu tempat.

# Tugas

## Latihan 1: Refactoring

```python
BATAS_LULUS = 60


def hitung_rata_rata(daftar_nilai):
    """Mengembalikan rata-rata dari daftar nilai."""
    return sum(daftar_nilai) / len(daftar_nilai)


def hitung_jumlah_lulus(daftar_nilai):
    """Mengembalikan jumlah nilai yang lulus."""
    jumlah = 0
    for nilai in daftar_nilai:
        if nilai >= BATAS_LULUS:
            jumlah = jumlah + 1
    return jumlah


def tentukan_grade(nilai):
    """Mengembalikan grade berdasarkan nilai."""
    if nilai >= 90:
        return "A"
    elif nilai >= 80:
        return "B"
    elif nilai >= 70:
        return "C"
    elif nilai >= 60:
        return "D"
    else:
        return "E"


def main():
    daftar_nilai = [80, 90, 75, 85, 92]

    rata_rata = hitung_rata_rata(daftar_nilai)
    jumlah_lulus = hitung_jumlah_lulus(daftar_nilai)

    print(f"Rata-rata: {rata_rata:.2f}")
    print(f"Jumlah lulus: {jumlah_lulus}")

    for nilai in daftar_nilai:
        print(tentukan_grade(nilai))


if __name__ == "__main__":
    main()
```

Perubahan utama:

| Sebelum | Sesudah |
| ---- | ---- |
| `d`, `t`, `r`, `n`, `i` | `daftar_nilai`, `total`, `rata_rata`, `jumlah_lulus`, `nilai` |
| `60`, `90`, `80`, `70` | konstanta `BATAS_LULUS` (dan rentang di `tentukan_grade`) |
| Satu blok panjang | Fungsi `hitung_rata_rata`, `hitung_jumlah_lulus`, `tentukan_grade` |
| Logika kelulusan terduplikasi | Terpusat pada `BATAS_LULUS` |
| Tanpa struktur | `main()` + `if __name__ == "__main__":` |

## Latihan 2: Optimisasi

```python
angka = [12, 45, 7, 23, 89, 34, 5, 67, 90, 18]

total = sum(angka)
rata_rata = total / len(angka)
terbesar = max(angka)
terkecil = min(angka)

print(total)
print(rata_rata)
print(terbesar)
print(terkecil)
```

Penjelasan optimisasi:

| Sebelum | Sesudah |
| ---- | ---- |
| Empat perulangan manual | Fungsi bawaan `sum()`, `max()`, `min()` |
| Total dihitung dua kali | `total` dihitung sekali, dipakai ulang untuk rata-rata |
| `range(len(...))` + indeks | Tidak perlu indeks manual |
| `len(angka)` dipanggil berulang | Dipanggil sekali |

## Latihan 3: Naming dan Comment

```python
PHI = 3.14
BATAS_LULUS = 60


def hitung_luas_lingkaran(jari_jari):
    """Mengembalikan luas lingkaran berdasarkan jari-jari."""
    return PHI * jari_jari * jari_jari


def sudah_lulus(nilai):
    """Mengembalikan True jika nilai memenuhi syarat kelulusan."""
    return nilai >= BATAS_LULUS


jari_jari = 7
nilai = 75

print(hitung_luas_lingkaran(jari_jari))
print(sudah_lulus(nilai))
```

Perubahan utama:

| Sebelum | Sesudah |
| ---- | ---- |
| `f`, `g`, `x`, `n`, `r`, `s` | `hitung_luas_lingkaran`, `sudah_lulus`, `jari_jari`, `nilai` |
| `3.14`, `60` (angka ajaib) | konstanta `PHI`, `BATAS_LULUS` |
| Komentar mengulang kode | Docstring yang menjelaskan fungsi |
| `if-else` untuk boolean | Langsung `return nilai >= BATAS_LULUS` |

## Latihan 4: Organisasi Kode

```python
BATAS_LULUS = 60


def baca_nilai(banyak):
    """Membaca sejumlah nilai dari input dan mengembalikannya sebagai list."""
    data = []
    for i in range(banyak):
        nilai = int(input(f"Nilai ke-{i + 1}: "))
        data.append(nilai)
    return data


def hitung_rata_rata(daftar_nilai):
    """Mengembalikan rata-rata dari daftar nilai."""
    return sum(daftar_nilai) / len(daftar_nilai)


def tentukan_status(nilai):
    """Mengembalikan status kelulusan berdasarkan nilai."""
    if nilai >= BATAS_LULUS:
        return "Lulus"
    return "Tidak lulus"


def main():
    print("=== Pengolahan Nilai ===")
    banyak = int(input("Banyak nilai: "))

    daftar_nilai = baca_nilai(banyak)
    rata_rata = hitung_rata_rata(daftar_nilai)

    print(f"Rata-rata: {rata_rata:.2f}")
    print(f"Status: {tentukan_status(rata_rata)}")


if __name__ == "__main__":
    main()
```

Pembagian tanggung jawab:

| Bagian | Tanggung jawab |
| ---- | ---- |
| `baca_nilai` | Input (membaca data) |
| `hitung_rata_rata`, `tentukan_status` | Logika (tanpa `input()`/`print()`) |
| `main` | Output (menampilkan hasil) |
| `if __name__ == "__main__":` | Menjalankan program utama |
