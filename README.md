# ADS_5_RB
# 📊 Analisis Efektivitas Tes terhadap Pemahaman Next.js

Tugas Besar **ADS**: analisis statistik untuk mengukur apakah skor pemahaman responden terhadap **Next.js** meningkat secara signifikan setelah mengikuti tes, menggunakan **uji-t dua populasi berpasangan (paired t-test)** dengan bahasa **R**.

![R](https://img.shields.io/badge/R-4.x-276DC3?logo=r&logoColor=white)
![RMarkdown](https://img.shields.io/badge/R%20Markdown-analysis-blue)
![Sampel](https://img.shields.io/badge/Sampel-52%20responden-2ECC71)
![p-value](https://img.shields.io/badge/p--value-0.00022-brightgreen)

---

## 📌 Latar Belakang

Responden mengisi survei pemahaman mengenai Next.js sebanyak dua kali:

1. **Sebelum tes**
2. **Setelah tes**

Pertanyaan penelitian: **apakah terdapat perbedaan rata-rata skor pemahaman yang signifikan antara sebelum dan setelah tes?**

## 🎯 Tujuan

- Menggambarkan distribusi skor sebelum dan setelah tes (statistik deskriptif dan visualisasi).
- Memeriksa asumsi normalitas pada selisih skor.
- Menguji secara inferensial apakah ada peningkatan skor yang signifikan.

---

## 🗂️ Dataset

Dua file CSV hasil survei (Google Form) dengan **52 responden** pada masing-masing file (data berpasangan).

| File | Keterangan |
|------|------------|
| `Dataset Tugas Besar ADS - Survei Kepuasan Sebelum Test.csv` | Respons survei sebelum tes |
| `Dataset Tugas Besar ADS - Survei Kepuasan Setelah Test.csv` | Respons survei setelah tes |

**Struktur kolom** (11 kolom):

- `Timestamp`: waktu pengisian
- 10 kolom pernyataan dengan skala Likert **1–5**

| No | Pernyataan |
|----|------------|
| 1 | Tahu apa itu Next.js dan fungsinya sebagai framework website |
| 2 | Tahu cara membuat project baru dengan `npx create-next-app` |
| 3 | Tahu cara menjalankan project di komputer lokal dengan `npm run dev` |
| 4 | Memahami struktur folder (`pages`, `public`, `components`) |
| 5 | Tahu cara membuat halaman baru dengan menambah file di folder `pages` |
| 6 | Tahu cara membuat navigasi antar halaman dengan komponen `<Link>` |
| 7 | Tahu cara menampilkan gambar dengan komponen `<Image>` dari `next/image` |
| 8 | Memahami cara mengatur tampilan global lewat `_app.js` |
| 9 | Tahu cara membuat website siap publish dengan `npm run build` |
| 10 | Merasa percaya diri menggunakan Next.js untuk membuat website sederhana |

**Skor total** per responden = jumlah 10 butir, dengan rentang **10–50**.
**Selisih skor** = skor setelah − skor sebelum.

---

## 🔬 Metodologi

1. **Skoring**: menjumlahkan 10 butir Likert per responden (`rowSums`).   


$$
X_i^{\text{sebelum}} = \sum_{j=1}^{10} x_{ij}^{\text{sebelum}}, \qquad
X_i^{\text{setelah}} = \sum_{j=1}^{10} x_{ij}^{\text{setelah}}
$$


2. **Statistik deskriptif**: n, mean, median, SD, varians, min, Q1, Q3, maks, IQR, skewness, dan batas outlier (aturan 1,5 × IQR).



3. **Visualisasi**: boxplot perbandingan, histogram + kurva densitas selisih, dan Q-Q plot.



4. **Uji normalitas**: Shapiro-Wilk pada selisih skor.



5. **Uji hipotesis**: paired t-test dua sisi, tingkat kepercayaan 95%.

**Hipotesis:**

- H₀ : μ_d = 0 (tidak ada perbedaan rata-rata skor)
- H₁ : μ_d ≠ 0 (ada perbedaan rata-rata skor)

---

## 📈 Hasil Utama

| Statistik | Sebelum Tes | Setelah Tes | Selisih (Setelah − Sebelum) |
|-----------|:-----------:|:-----------:|:---------------------------:|
| n | 52 | 52 | 52 |
| Mean | 28,33 | 33,67 | **5,35** |
| Median | 30,0 | 34,5 | 6,0 |
| Std. Deviasi | 5,81 | 7,25 | 9,69 |
| Min – Maks | 14 – 40 | 10 – 50 | −20 – 29 |

**Uji normalitas (Shapiro-Wilk) pada selisih:** W = 0,985; p-value = 0,752. Karena p > 0,05, selisih skor dapat dianggap berdistribusi normal sehingga syarat uji-t terpenuhi.

**Paired t-test:**

| Parameter | Nilai |
|-----------|-------|
| t-hitung | 3,979 |
| df | 51 |
| p-value | 0,00022 |
| 95% CI selisih rata-rata | [2,65 ; 8,04] |
| Rata-rata selisih | 5,35 |

### ✅ Kesimpulan

Karena p-value (0,00022) < α (0,05), **H₀ ditolak**. Ada perbedaan yang signifikan secara statistik antara skor pemahaman Next.js sebelum dan setelah tes, dengan rata-rata peningkatan sekitar **5,35 poin** (skala 10–50).

> **Catatan:** angka di atas dihitung ulang dari dataset yang disertakan. Jalankan ulang file `.Rmd` untuk memverifikasi pada lingkungan R kamu.

---

## 📁 Struktur Repositori

```
.
├── README.md
├── codeR_5_RB.Rmd
├── Dataset Tugas Besar ADS - Survei Kepuasan Sebelum Test.csv
└── Dataset Tugas Besar ADS - Survei Kepuasan Setelah Test.csv
```

> Sesuaikan dengan susunan folder repo kamu. Jika file CSV dipindah ke folder `data/`, ubah path pada `read.csv()` di dalam `.Rmd`.

---

## 🚀 Cara Menjalankan

### Prasyarat

- [R](https://cran.r-project.org/) ≥ 4.0
- [RStudio](https://posit.co/download/rstudio-desktop/) (disarankan)
- Paket R:

```r
install.packages(c("e1071", "readxl", "rmarkdown"))
```

### Langkah

```bash
git clone https://github.com/<username>/<nama-repo>.git
cd <nama-repo>
```

1. Buka `codeR_5_RB.Rmd` di RStudio.
2. Pastikan kedua file CSV berada di *working directory* (atau sesuaikan path-nya).
3. Klik **Knit**, atau jalankan dari R:

```r
rmarkdown::render("codeR_5_RB.Rmd")
```

---

## 🧰 Teknologi

- **R** dan **R Markdown**
- **e1071** (perhitungan skewness)
- **readxl** (dimuat pada skrip)
- Base R graphics (`boxplot`, `hist`, `qqnorm`)

---

## 👥 Anggota Kelompok

<!-- Isi dengan nama dan NIM anggota kelompok -->

| Nama | NIM |
|------|-----|
| _Nama Anggota 1_ | _NIM_ |
| _Nama Anggota 2_ | _NIM_ |
| _Nama Anggota 3_ | _NIM_ |

**Mata Kuliah:** Analisis Data Statistika (ADS)





# 📊 Analisis Efektivitas Tes terhadap Pemahaman Next.js

Tugas Besar **ADS**: analisis statistik untuk mengukur apakah skor pemahaman responden terhadap **Next.js** meningkat secara signifikan setelah mengikuti tes, menggunakan **uji-t dua populasi berpasangan (paired t-test)** dengan bahasa **R**.

![R](https://img.shields.io/badge/R-4.x-276DC3?logo=r&logoColor=white)
![RMarkdown](https://img.shields.io/badge/R%20Markdown-analysis-blue)
![Sampel](https://img.shields.io/badge/Sampel-52%20responden-2ECC71)
![p-value](https://img.shields.io/badge/p--value-0.00022-brightgreen)

---

## 📌 Latar Belakang

Responden mengisi survei pemahaman mengenai Next.js sebanyak dua kali:

1. **Sebelum tes**
2. **Setelah tes**

Pertanyaan penelitian: **apakah terdapat perbedaan rata-rata skor pemahaman yang signifikan antara sebelum dan setelah tes?**

## 🎯 Tujuan

- Menggambarkan distribusi skor sebelum dan setelah tes (statistik deskriptif dan visualisasi).
- Memeriksa asumsi normalitas pada selisih skor.
- Menguji secara inferensial apakah ada peningkatan skor yang signifikan.

---

## 🗂️ Dataset

Dua file CSV hasil survei (Google Form) dengan **52 responden** pada masing-masing file (data berpasangan).

| File | Keterangan |
|------|------------|
| `Dataset Tugas Besar ADS - Survei Kepuasan Sebelum Test.csv` | Respons survei sebelum tes |
| `Dataset Tugas Besar ADS - Survei Kepuasan Setelah Test.csv` | Respons survei setelah tes |

**Struktur kolom** (11 kolom):

- `Timestamp`: waktu pengisian
- 10 kolom pernyataan dengan skala Likert **1–5**

| No | Pernyataan |
|----|------------|
| 1 | Tahu apa itu Next.js dan fungsinya sebagai framework website |
| 2 | Tahu cara membuat project baru dengan `npx create-next-app` |
| 3 | Tahu cara menjalankan project di komputer lokal dengan `npm run dev` |
| 4 | Memahami struktur folder (`pages`, `public`, `components`) |
| 5 | Tahu cara membuat halaman baru dengan menambah file di folder `pages` |
| 6 | Tahu cara membuat navigasi antar halaman dengan komponen `<Link>` |
| 7 | Tahu cara menampilkan gambar dengan komponen `<Image>` dari `next/image` |
| 8 | Memahami cara mengatur tampilan global lewat `_app.js` |
| 9 | Tahu cara membuat website siap publish dengan `npm run build` |
| 10 | Merasa percaya diri menggunakan Next.js untuk membuat website sederhana |

**Skor total** per responden = jumlah 10 butir, dengan rentang **10–50**.
**Selisih skor** = skor setelah − skor sebelum.

---

## 🔬 Metodologi

1. **Skoring**: menjumlahkan 10 butir Likert per responden (`rowSums`).
2. **Statistik deskriptif**: n, mean, median, SD, varians, min, Q1, Q3, maks, IQR, skewness, dan batas outlier (aturan 1,5 × IQR).
3. **Visualisasi**: boxplot perbandingan, histogram + kurva densitas selisih, dan Q-Q plot.
4. **Uji normalitas**: Shapiro-Wilk pada selisih skor.
5. **Uji hipotesis**: paired t-test dua sisi, tingkat kepercayaan 95%.

**Hipotesis:**

- H₀ : μ_d = 0 (tidak ada perbedaan rata-rata skor)
- H₁ : μ_d ≠ 0 (ada perbedaan rata-rata skor)

---

## 📐 Rumus yang Digunakan

> Rumus ditulis dengan LaTeX dan otomatis dirender oleh GitHub.

### 1. Skor Total dan Selisih

Untuk responden ke-$i$ dengan jawaban butir ke-$j$ sebesar $x_{ij}$ ($j = 1, 2, \dots, 10$):

$$
X_i^{\text{sebelum}} = \sum_{j=1}^{10} x_{ij}^{\text{sebelum}}, \qquad
X_i^{\text{setelah}} = \sum_{j=1}^{10} x_{ij}^{\text{setelah}}
$$

$$
d_i = X_i^{\text{setelah}} - X_i^{\text{sebelum}}
$$

### 2. Statistik Deskriptif

**Rata-rata (mean)**

$$
\bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i
$$

**Varians sampel dan standar deviasi**

$$
s^2 = \frac{1}{n-1}\sum_{i=1}^{n}\left(x_i - \bar{x}\right)^2, \qquad s = \sqrt{s^2}
$$

**Median** (data terurut $x_{(1)} \le \dots \le x_{(n)}$)

$$
\text{Median} =
\begin{cases}
x_{\left(\frac{n+1}{2}\right)}, & n \text{ ganjil} \\[6pt]
\dfrac{x_{\left(\frac{n}{2}\right)} + x_{\left(\frac{n}{2}+1\right)}}{2}, & n \text{ genap}
\end{cases}
$$

**Kuartil** (default `quantile()` di R, tipe 7). Posisi kuantil ke-$p$:

$$
h = (n-1)p + 1, \qquad Q_p = x_{(\lfloor h \rfloor)} + (h - \lfloor h \rfloor)\left(x_{(\lfloor h \rfloor + 1)} - x_{(\lfloor h \rfloor)}\right)
$$

dengan $Q_1$ untuk $p = 0{,}25$ dan $Q_3$ untuk $p = 0{,}75$.

**Rentang antar kuartil (IQR)**

$$
\text{IQR} = Q_3 - Q_1
$$

**Batas pencilan (outlier)**

$$
\text{Batas bawah} = Q_1 - 1{,}5 \times \text{IQR}, \qquad
\text{Batas atas} = Q_3 + 1{,}5 \times \text{IQR}
$$

Data di luar interval tersebut dianggap pencilan (ditandai titik pada boxplot).

**Skewness** (fungsi `e1071::skewness()`, default tipe 3)

$$
b_1 = \frac{m_3}{s^3}, \qquad m_3 = \frac{1}{n}\sum_{i=1}^{n}\left(x_i - \bar{x}\right)^3
$$

Nilai $b_1 \approx 0$ berarti distribusi simetris, $b_1 < 0$ miring ke kiri, $b_1 > 0$ miring ke kanan.

### 3. Uji Normalitas Shapiro-Wilk

Hipotesis: $H_0$ data berdistribusi normal vs $H_1$ data tidak berdistribusi normal.

$$
W = \frac{\left(\sum_{i=1}^{n} a_i\, x_{(i)}\right)^2}{\sum_{i=1}^{n}\left(x_i - \bar{x}\right)^2}
$$

dengan $x_{(i)}$ data terurut dan $a_i$ koefisien yang bergantung pada nilai harapan statistik terurut distribusi normal. **Keputusan:** jika $p\text{-value} > \alpha$, $H_0$ tidak ditolak (data dianggap normal).

### 4. Uji-t Berpasangan (Paired t-test)

**Hipotesis**

$$
H_0 : \mu_d = 0 \qquad \text{vs} \qquad H_1 : \mu_d \neq 0
$$

**Statistik uji**

$$
t = \frac{\bar{d}}{s_d / \sqrt{n}}, \qquad
\bar{d} = \frac{1}{n}\sum_{i=1}^{n} d_i, \qquad
s_d = \sqrt{\frac{1}{n-1}\sum_{i=1}^{n}\left(d_i - \bar{d}\right)^2}
$$

**Derajat bebas**

$$
df = n - 1
$$

**Selang kepercayaan $(1-\alpha)\times 100\%$ untuk $\mu_d$**

$$
\bar{d} \;\pm\; t_{\alpha/2,\,n-1}\cdot\frac{s_d}{\sqrt{n}}
$$

**Kriteria keputusan** (uji dua sisi, $\alpha = 0{,}05$):

$$
\text{Tolak } H_0 \text{ jika } |t| > t_{\alpha/2,\,n-1} \quad \text{atau} \quad p\text{-value} < \alpha
$$

### 5. Penerapan pada Data

Dengan $n = 52$, $\bar{d} = 5{,}346$, dan $s_d = 9{,}689$:

$$
t = \frac{5{,}346}{9{,}689 / \sqrt{52}} = \frac{5{,}346}{1{,}343} \approx 3{,}979, \qquad df = 51
$$

$$
\text{CI}_{95\%} = 5{,}346 \pm 2{,}008 \times 1{,}343 = [\,2{,}65\;;\;8{,}04\,]
$$

Nilai $t_{0{,}025;\,51} \approx 2{,}008$. Karena $|t| = 3{,}979 > 2{,}008$ (atau $p = 0{,}00022 < 0{,}05$), $H_0$ ditolak.

---

## 📈 Hasil Utama

| Statistik | Sebelum Tes | Setelah Tes | Selisih (Setelah − Sebelum) |
|-----------|:-----------:|:-----------:|:---------------------------:|
| n | 52 | 52 | 52 |
| Mean | 28,33 | 33,67 | **5,35** |
| Median | 30,0 | 34,5 | 6,0 |
| Std. Deviasi | 5,81 | 7,25 | 9,69 |
| Min – Maks | 14 – 40 | 10 – 50 | −20 – 29 |

**Uji normalitas (Shapiro-Wilk) pada selisih:** W = 0,985; p-value = 0,752. Karena p > 0,05, selisih skor dapat dianggap berdistribusi normal sehingga syarat uji-t terpenuhi.

**Paired t-test:**

| Parameter | Nilai |
|-----------|-------|
| t-hitung | 3,979 |
| df | 51 |
| p-value | 0,00022 |
| 95% CI selisih rata-rata | [2,65 ; 8,04] |
| Rata-rata selisih | 5,35 |

### ✅ Kesimpulan

Karena p-value (0,00022) < α (0,05), **H₀ ditolak**. Ada perbedaan yang signifikan secara statistik antara skor pemahaman Next.js sebelum dan setelah tes, dengan rata-rata peningkatan sekitar **5,35 poin** (skala 10–50).

> **Catatan:** angka di atas dihitung ulang dari dataset yang disertakan. Jalankan ulang file `.Rmd` untuk memverifikasi pada lingkungan R kamu.

---

## 📁 Struktur Repositori

```
.
├── README.md
├── codeR_5_RB.Rmd
└── data/
    ├── Dataset Tugas Besar ADS - Survei Kepuasan Sebelum Test.csv
    └── Dataset Tugas Besar ADS - Survei Kepuasan Setelah Test.csv
```

> Sesuaikan dengan susunan folder repo kamu. Jika file CSV dipindah ke folder `data/`, ubah path pada `read.csv()` di dalam `.Rmd`.

---

## 🚀 Cara Menjalankan

### Prasyarat

- [R](https://cran.r-project.org/) ≥ 4.0
- [RStudio](https://posit.co/download/rstudio-desktop/) (disarankan)
- Paket R:

```r
install.packages(c("e1071", "readxl", "rmarkdown"))
```

### Langkah

```bash
git clone https://github.com/<username>/<nama-repo>.git
cd <nama-repo>
```

1. Buka `codeR_5_RB.Rmd` di RStudio.
2. Pastikan kedua file CSV berada di *working directory* (atau sesuaikan path-nya).
3. Klik **Knit**, atau jalankan dari R:

```r
rmarkdown::render("codeR_5_RB.Rmd")
```

---

## 🧰 Teknologi

- **R** dan **R Markdown**
- **e1071** (perhitungan skewness)
- **readxl** (dimuat pada skrip)
- Base R graphics (`boxplot`, `hist`, `qqnorm`)

---

## 👥 Anggota Kelompok

<!-- Isi dengan nama dan NIM anggota kelompok -->

| Nama | NIM |
|------|-----|
| _Nama Anggota 1_ | _NIM_ |
| _Nama Anggota 2_ | _NIM_ |
| _Nama Anggota 3_ | _NIM_ |

**Mata Kuliah:** ADS

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan akademik. Tambahkan lisensi (mis. MIT) bila ingin dipublikasikan secara terbuka.
