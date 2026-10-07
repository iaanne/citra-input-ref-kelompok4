# TUGAS 3 Implementasi Filter dan Pengolahan Histogram

Mata kuliah Analisis Data Citra Biomedis.

Repo ini berisi citra masukan dan satu notebook Jupyter yang memuat implementasi mean filter, median filter, perataan histogram, dan spesifikasi histogram.

## Isi repo

```
images/INPUT.png       citra utama, CT kepala axial grayscale 8-bit 512x512
images/REFERENCE.png   citra referensi (kepala dengan urutan MRI T2) untuk histogram specification
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
| C5 | Spesifikasi histogram dengan `images/REFERENCE.png` | selesai |

Fungsi pembantu `show_image_hist` dan `hist_values` dipakai ulang di seluruh bagian. Filter median dan mean diimplementasikan manual dengan NumPy, lalu diverifikasi terhadap `scipy.ndimage` pada cell masing-masing.

## Catatan hasil

Beberapa angka yang dipakai pada bagian analisis:

- Mean filter dan median filter sama-sama ditulis manual dengan NumPy. Padding tepi memakai mode `reflect`, sehingga dimensi citra tidak berubah.
- Pada citra utama, mean filter lebih efektif menekan derau, sedangkan median filter hampir tidak mengubah tepi anatomi. Retensi tepi diukur sebagai rasio rata-rata magnitude gradien pada piksel tepi terhadap citra asli.
- Perataan histogram menaikkan kecerahan rata-rata citra, tetapi kontras antar jaringan di area parenkim justru berkurang. Penyebabnya komposisi histogram citra yang didominasi background bernilai 0 dan tulang yang jenuh di 255.
- Histogram specification memakai `images/INPUT.png` (CT kepala axial) sebagai citra input dan `images/REFERENCE.png` (kepala dengan urutan MRI T2) sebagai referensi. Mean citra input 80.772 menjadi 59.693 dan std 87.044 menjadi 64.570, mendekati referensi (41.591 / 40.481). Selisih rata-rata CDF hasil terhadap referensi 0.0720 dengan maksimum 0.4001, karena 40.42% piksel input menumpuk di level 0 dan harus masuk ke satu level hasil (15) oleh sifat monoton dan banyak-ke-satu pemetaannya, sehingga kecocokan hanya bersifat aproksimasi.

Seluruh angka pada bagian analisis diambil langsung dari output cell, bukan estimasi manual.

## Pembagian

- C1, C2, dan penyediaan citra: Satria Manggala Putra Pratama
- C3 dan C4: ian