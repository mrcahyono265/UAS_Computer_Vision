# Tugas Besar 1: Scale-Invariant Feature Transform (SIFT) & Panorama

**Mata Kuliah:** Visi Komputer (T1646746)  
**Nama:** Mohammad Ridho Cahyono  
**Universitas:** Universitas Darussalam Gontor

---

## 📌 Deskripsi Proyek
Proyek ini merupakan implementasi algoritma **Scale-Invariant Feature Transform (SIFT)** untuk mendeteksi fitur lokal pada citra, melakukan pencocokan fitur (*feature matching*), dan menggabungkan dua citra menjadi satu panorama (*image stitching*).

Eksperimen dilakukan menggunakan dataset citra lingkungan kampus UNIDA Gontor, dengan fokus pada penggabungan perspektif gedung dan area parkir yang memiliki area tumpang tindih (*overlap*) sekitar 40%.

## 🎯 Tujuan Pembelajaran
1. Memahami konsep dasar SIFT (Keypoint & Descriptor).
2. Menganalisis peran *Difference of Gaussian* (DoG) dalam *Scale-space*.
3. Melakukan *Feature Matching* menggunakan BFMatcher dan Lowe's Ratio Test.
4. Membangun panorama sederhana menggunakan estimasi matriks Homografi.

## 🚀 Fitur Utama
* **Class-Based Architecture:** Kode ditulis dalam bentuk Class `SIFTPanoStitcher` agar modular dan mudah dikembangkan.
* **Auto Visualization:** Program secara otomatis menghasilkan satu gambar komprehensif yang memuat 3 tahap visualisasi (Keypoints, Matching, Result).
* **Robust Matching:** Menggunakan *Lowe's Ratio Test* untuk menyaring *false matches*.

## 📂 Struktur Direktori
Sesuai dengan instruksi pengumpulan, struktur folder proyek ini adalah sebagai berikut:

```
./
├── code/
│   ├── main.ipynb              # Kode utama 
├── data/
│   ├── 1.jpeg                  # Citra Input 1 (Kiri/Gedung)
│   ├── 2.jpeg                  # Citra Input 2 (Kanan/Lapangan)
├── results/
│   ├── final results.png       # Hasil Akhir
├── laporan.pdf                 # Laporan analisis
└── README.md                   
```

## 🛠️ Instalasi & Dependensi
1.  **Clone repository ini:**
    ```bash
    git clone [https://github.com/mrcahyono265/UAS_Computer_Vision.git](https://github.com/mrcahyono265/UAS_Computer_Vision.git)
    cd repo-ini
    ```

Proyek ini dibangun menggunakan Python 3.11.13
2.  **Buat Virtual Environment (Disarankan):**
    ```bash
    python -m venv venv
    # Windows
    venv\Scripts\activate
    # Mac/Linux
    source venv/bin/activate
    ```

3.  **Install Library:**
    ```bash
    pip install opencv-python numpy matplotlib
    ```

## 🚀 Cara Menjalankan
- Pastikan citra input (`1.jpeg` dan `2.jpeg`) sudah berada di dalam folder `data/`.

- Buka file `main.ipynb` menggunakan Jupyter Notebook atau VS Code.

- Jalankan setiap sel secara berurutan (Run All).

- Hasil visualisasi akan muncul di notebook dan tersimpan otomatis di folder `result/`.

## 📊 Metodologi & Hasil
1. Deteksi KeypointMenggunakan SIFT untuk mendeteksi ribuan titik fitur yang invarian terhadap skala dan rotasi.Jumlah Keypoint Terdeteksi: 5.973 titik.
2. Difference of Gaussian (DoG)Menerapkan Gaussian Blur dengan $\sigma$ berbeda untuk mendekati Laplacian of Gaussian, memungkinkan deteksi fitur pada berbagai skala jarak.
3. Feature Matching (Lowe's Ratio Test)Menggunakan Brute-Force Matcher (k-NN) yang divalidasi dengan Lowe's Ratio Test (threshold = 0.75).Matches Awal: 5.973 pasang.Good Matches (Valid): 668 pasang.
4. Panorama StitchingMatriks Homografi dihitung menggunakan algoritma RANSAC berdasarkan good matches untuk melakukan warping citra kedua ke perspektif citra pertama. Hasilnya adalah panorama mulus yang menyambungkan gedung dan mobil kuning tanpa distorsi signifikan.

## 📝 Catatan Analisis
- Stabilitas: Algoritma berhasil menangani fitur berulang (tiang gedung) berkat tekstur unik dari objek sekitar (mobil kuning, genteng).
- Artefak: Terlihat sedikit garis batas (seam) pada langit akibat perbedaan auto-exposure kamera, namun geometri bangunan tersambung sempurna.