# TUGAS 3 Implementasi Filter dan Pengolahan Histogram

Mata kuliah Analisis Data Citra Biomedis.

Repo ini berisi citra masukan dan satu notebook Jupyter yang memuat implementasi mean filter, median filter, dan perataan histogram.

## Isi repo

```
images/INPUT.png       citra utama, CT kepala axial grayscale 8-bit 512x512
images/REFERENCE.png   citra referensi untuk histogram specification
notebook.ipynb         seluruh kode dan analisis
```

## Cara menjalankan

Butuh Python 3.10 atau lebih baru.

```bash
pip install numpy scipy matplotlib pillow
```

Buka `notebook.ipynb` di Jupyter, lalu pilih Run All. Pastikan folder `images/` berada di direktori yang sama dengan notebook, karena path citra ditulis relatif terhadap folder kerja kernel.

## Struktur notebook

| Bagian | Isi | Status |
| --- | --- | --- |
| C1 | Citra grayscale asli dan histogramnya | selesai |
| C2 | Mean filter 3x3 dan 5x5, lengkap dengan histogram dan analisis | selesai |
| C3 | Median filter 3x3 dan 5x5, lengkap dengan histogram dan analisis | selesai |
| C4 | Perataan histogram, citra asli dan hasil beserta histogramnya | selesai |
| C5 | Spesifikasi histogram dengan `images/REFERENCE.png` | belum dikerjakan |

Fungsi pembantu `show_image_hist` dan `hist_values` dipakai ulang di seluruh bagian. Filter median dan mean diimplementasikan manual dengan NumPy, lalu diverifikasi terhadap `scipy.ndimage` pada cell masing-masing.

## Catatan hasil

Beberapa angka yang dipakai pada bagian analisis:

- Mean filter dan median filter sama-sama ditulis manual dengan NumPy. Padding tepi memakai mode `reflect`, sehingga dimensi citra tidak berubah.
- Pada citra utama, mean filter lebih efektif menekan derau, sedangkan median filter hampir tidak mengubah tepi anatomi. Retensi tepi diukur sebagai rasio rata-rata magnitude gradien pada piksel tepi terhadap citra asli.
- Perataan histogram menaikkan kecerahan rata-rata citra, tetapi kontras antar jaringan di area parenkim justru berkurang. Penyebabnya komposisi histogram citra yang didominasi background bernilai 0 dan tulang yang jenuh di 255.

Seluruh angka pada bagian analisis diambil langsung dari output cell, bukan estimasi manual.

## Pembagian

- C1, C2, dan penyediaan citra: Satria Manggala Putra Pratama
- C3 dan C4: ian