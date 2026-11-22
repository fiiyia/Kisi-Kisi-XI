# Product Requirements Document (PRD)
## Web Kisi-Kisi & Latihan UAS Matematika Tingkat Lanjut — SMA Kelas XI

**Versi:** 1.0  
**Target Pengguna:** Peserta Didik SMA Kelas XI & Guru Matematika Tingkat Lanjut  
**Cakupan Materi:** Polinomial (30%), Operasi Matriks (50%), Transformasi Geometri: Translasi (20%)  

---

## 1. Ringkasan Produk (Product Overview)
Aplikasi web ini dirancang sebagai media belajar mandiri dan persiapan Ujian Akhir Semester (UAS) bagi siswa SMA Kelas XI pada mata pelajaran Matematika Tingkat Lanjut. Web ini menggabungkan dua komponen utama:
1. **Kisi-Kisi UAS Interaktif:** Memaparkan peta materi, indikator kompetensi, sebaran tipe soal, bobot skor, dan estimasi waktu pengerjaan ($120$ menit) secara transparan agar siswa dapat menyusun strategi belajar.
2. **Latihan Soal Paralel (Isomorfik):** Menyediakan paket latihan berformat identik dengan naskah UAS (10 Isian Singkat model LKPD, 5 Menjodohkan opsi A–G, dan 5 Uraian HOTS), tetapi menggunakan **konteks cerita, angka, dan variasi langkah yang berbeda** sehingga siswa berlatih konsep secara autentik tanpa menghafal jawaban UAS.

---

## 2. Tujuan Produk (Goals & Objectives)
* Membantu siswa memahami struktur dan tingkat kesulitan UAS (L1–L3) sebelum hari ujian.
* Melatih ketelitian berhitung siswa pada materi Polinomial, Operasi Matriks (termasuk ordo $2 \times 2$ dan $3 \times 3$), serta Translasi (titik, bangun datar, dan garis).
* Memudahkan guru memverifikasi partisipasi belajar siswa melalui **kolom identitas (Nama & Kelas)** dan ringkasan hasil latihan yang dapat diunduh atau dicetak.

---

## 3. Alur Pengguna (User Flow)
1. **Halaman Awal & Identitas Siswa:** Siswa membuka web, melihat ringkasan ujian, lalu wajib mengisi **Nama Lengkap** dan **Kelas** sebelum membuka sesi latihan.
2. **Halaman Kisi-Kisi (Opsional/Tab Navigasi):** Siswa dapat mempelajari tabel kisi-kisi, proporsi materi, dan pembobotan nilai kapan saja sebelum atau sesudah latihan.
3. **Pemilihan Mode Latihan:**
   * *Mode Belajar:* Tanpa batas waktu, dilengkapi tombol petunjuk (*hint*) per nomor.
   * *Mode Simulasi UAS:* Dilengkapi penghitung waktu mundur ($120$ menit) sesuai durasi ujian sesungguhnya.
4. **Pengerjaan Soal Bertahap:**
   * **Bagian I:** Isian Singkat Model Narasi/LKPD (10 rumpang).
   * **Bagian II:** Menjodohkan (5 soal dengan 7 pilihan A–G).
   * **Bagian III:** Uraian HOTS (5 soal dengan kolom jawaban/catatan kerja dan panduan cek mandiri).
5. **Halaman Hasil & Pembahasan:** Menampilkan identitas siswa, skor otomatis (Bagian I & II), cek rubrik mandiri (Bagian III), analisis penguasaan per topik, pembahasan lengkap langkah demi langkah, serta tombol **Cetak / Simpan Bukti Latihan (PDF)**.

---

## 4. Spesifikasi Fitur Utama (Functional Requirements)

### 4.1. Formulir Identitas Siswa (Wajib)
* **Input Nama Lengkap:** Kolom teks wajib diisi (*required*, minimal 3 karakter).
* **Input / Pilihan Kelas:** Dapat berupa *dropdown* (misal: `XI-1` sampai `XI-10` atau `XI MIPA/F` yang dapat dikonfigurasi) atau kolom teks singkat wajib diisi.
* **Persistensi Data:** Nama, kelas, dan progres jawaban tersimpan sementara di `localStorage` browser agar data siswa tidak hilang jika halaman tidak sengaja dimuat ulang (*refresh*).
* **Tampilan Identitas:** Nama dan kelas siswa ditampilkan secara jelas pada *header* selama mengerjakan dan tercetak pada halaman ringkasan hasil akhir.

### 4.2. Modul Kisi-Kisi UAS Interaktif
Menampilkan informasi kisi-kisi final yang terstruktur dalam tabel dan ringkasan visual:
* **Proporsi Materi (Total 20 Butir):**
  * Polinomial: 6 butir ($30\%$) — No. 1–3 (Isian), No. 11–12 (Menjodohkan), No. 16 (Uraian).
  * Operasi Matriks: 10 butir ($50\%$) — No. 4–8 (Isian), No. 13–14 (Menjodohkan), No. 17, 18, 20 (Uraian).
  * Translasi: 4 butir ($20\%$) — No. 9–10 (Isian), No. 15 (Menjodohkan), No. 19 (Uraian).
* **Estimasi Waktu & Bobot Skor:**
  * Bagian I (Isian Singkat LKPD): $25$ menit | $10 \times 2 = 20$ poin.
  * Bagian II (Menjodohkan): $20$ menit | $5 \times 3 = 15$ poin.
  * Bagian III (Uraian HOTS): $75$ menit | $65$ poin (No. 16: $10$, No. 17: $14$, No. 18: $11$, No. 19: $12$, No. 20: $18$).
* **Filter Kisi-Kisi:** Siswa dapat memfilter tabel kisi-kisi berdasarkan topik (Polinomial, Matriks, Translasi) atau tipe soal.

### 4.3. Modul Latihan Soal Paralel
Seluruh notasi matematika wajib dirender dengan rapi menggunakan **LaTeX** (misalnya KaTeX), termasuk pangkat, subskrip, pecahan, dan kurung siku matriks ordo $2 \times 2$ maupun $3 \times 3$.

* **Bagian I — Isian Singkat Interaktif (No. 1–10):**
  * Disajikan dalam 3 kartu narasi bergaya LKPD dengan kotak input (*inline input*) langsung di dalam kalimat rumpang.
  * Sistem penilaian otomatis (*auto-grading*) dengan normalisasi teks (mengabaikan spasi berlebih, titik pemisah ribuan seperti `650000` atau `650.000`, dan toleransi tanda minus).
* **Bagian II — Menjodohkan Interaktif (No. 11–15):**
  * Menampilkan 5 soal di sisi kiri dan 7 pilihan jawaban (`A` sampai `G`, termasuk 2 pengecoh) di sisi kanan.
  * Siswa memilih pasangan huruf melalui *dropdown* atau tombol klik pasang (*click-to-match*).
  * Validasi otomatis jika siswa memilih huruf yang sama untuk dua nomor berbeda (memberi peringatan ringan).
* **Bagian III — Uraian HOTS & Cek Rubrik Mandiri (No. 16–20):**
  * Menyediakan area teks (*textarea*) bagi siswa untuk menuliskan langkah ringkas dan jawaban akhir tiap sub-soal (`a`, `b`, `c`).
  * Setelah menekan **Selesai & Kumpulkan**, sistem menampilkan kunci jawaban, pembahasan langkah demi langkah, serta **daftar centang rubrik (Self-Assessment)** sesuai pembobotan parsial (total $65$ poin) agar siswa dapat menilai kesesuaian langkah kerjanya sendiri.

### 4.4. Halaman Evaluasi & Laporan Hasil
* Menampilkan **Nama**, **Kelas**, **Waktu Selesai**, dan **Total Skor** (Skor Otomatis Bagian I–II + Skor Rubrik Mandiri Bagian III).
* **Analisis Per Topik:** Menampilkan persentase ketepatan siswa pada masing-masing materi (Polinomial, Matriks, Translasi) untuk menunjukkan materi mana yang perlu dipelajari ulang.
* **Ekspor Bukti Latihan:** Tombol **Cetak / Simpan PDF** (`window.print()` dengan *CSS print layout* rapi) yang merangkum identitas siswa, skor, dan status pengerjaan agar dapat dikumpulkan ke guru (misal lewat Google Classroom atau WhatsApp).

---

## 5. Panduan Desain Soal Latihan (Mirip Kisi-Kisi, Tidak Identik UAS)
Agar soal latihan efektif tanpa membocorkan naskah UAS, pengembang konten harus menerapkan aturan variasi berikut:

| Bagian & No. | Kompetensi Kisi-Kisi UAS | Konteks di Naskah UAS Asli | Variasi Konteks & Soal di Web Latihan |
| :--- | :--- | :--- | :--- |
| **I (1–3)** | Perkalian & nilai polinomial (volume balok) | Kotak kemasan UMKM | **Kolam ikan / akuarium kaca** dengan dimensi $p(x), l(x), t(x)$ dan nilai $x$ berbeda. |
| **I (4–8)** | Penjumlahan, pengurangan, skalar, ordo, & perkalian matriks $2 \times 2$ | Penjualan Kopi Susu & Matcha (2 cabang) | **Penjualan Roti Cokelat & Keju** di 2 gerai selama akhir pekan (Sabtu–Minggu) dengan harga satuan baru. |
| **I (9–10)** | Translasi titik bertahap ($T_1$ lalu $T_2$) | Pergerakan drone pemetaan | **Pergerakan robot gudang / kapal nelayan** di koordinat Kartesius dengan titik awal & vektor translasi baru. |
| **II (11–12)** | Teorema Sisa & Teorema Faktor | $P(x)$ dibagi $(x-2)$ dan faktor $(x+1)$ | Polinomial berderajat 3 berbeda dengan pembagi $(x+2)$ dan pencarian koefisien $m$ dari faktor $(x-1)$. |
| **II (13–14)** | Determinan matriks $2 \times 2$ & kesamaan matriks | Matriks $A, P, Q$ dengan variabel $a, b$ | Elemen dan variabel baru ($p, q$), tetap menyertakan pengecoh dari kesalahan tanda determinan. |
| **II (15)** | Translasi persamaan garis | $2x - y + 3 = 0$ oleh $T=(1, -2)$ | Garis $3x + y - 4 = 0$ oleh $T=(-2, 3)$ dengan pengecoh salah tanda substitusi. |
| **III (16)** | Pembagian Horner/bersusun & pemfaktoran akar | $P(x) = x^3 - 2x^2 - 5x + 6$ dibagi $(x-1)$ | Polinomial kubik baru yang habis dibagi $(x+1)$ atau $(x-2)$ dengan 3 akar bulat berbeda. |
| **III (17)** | Soal cerita SPLDV diselesaikan dengan invers/Cramer | Penjualan tiket Reguler & VIP pentas seni | **Paket katering (Paket Hemat & Spesial)** atau **sewa lapangan futsal/badminton** dengan determinan kecil & harga bulat. |
| **III (18)** | Persamaan matriks $A \cdot X = B$ & sifat non-komutatif | Matriks $A$ ($\det = 1$) dan $B$ | Pasangan matriks $2 \times 2$ baru dengan $\det(A) = 1$ atau $-1$ agar invers tetap bulat. |
| **III (19)** | Komposisi translasi segitiga, analisis luas, & garis | Taman bermain segitiga $ABC$ & garis $g$ | **Lahan parkir berbentuk segitiga $PQR$** dan jalur pedestrian garis $h$ dengan dua vektor translasi baru. |
| **III (20)** | Determinan, kofaktor, adjoin, invers matriks $3 \times 3$ & sandi | Matriks kunci $M$ ($\det = -1$) dan sandi $C$ | Matriks kunci $3 \times 3$ baru dengan $\det = 1$ atau $-1$ (sehingga invers berupa bilangan bulat) dan vektor sandi baru. |

---

## 6. Persyaratan Non-Fungsional (Non-Functional Requirements)
* **Responsif (Mobile-First):** Tampilan nyaman diakses di ponsel pintar (mayoritas siswa berlatih lewat HP) maupun laptop. Tabel matriks dan kisi-kisi harus mendukung *horizontal scroll* bila layar sempit.
* **Performa & Kemudahan Akses:** Berjalan sepenuhnya di sisi klien (*client-side*) tanpa memerlukan pembuatan akun/password yang rumit, sehingga siswa dapat langsung mengakses lewat tautan (*link*).
* **Kejelasan Notasi Matematika:** Wajib menggunakan pustaka *math rendering* (**KaTeX**) agar seluruh ekspresi aljabar, matriks, dan vektor translasi tampil tajam dan sesuai standar buku teks.

---

## 7. Rekomendasi Arsitektur & Tech Stack
* **Format Implementasi (MVP):** Aplikasi web *Single-File* (HTML5 + Tailwind CSS + Vanilla JS/React + KaTeX CDN) agar mudah di-*host* secara gratis (GitHub Pages, Netlify, atau Vercel) atau dibuka langsung secara lokal.
* **Penyimpanan Data:** `localStorage` untuk menyimpan Nama, Kelas, dan progres jawaban di perangkat siswa.
* **Pengembangan Lanjutan (Opsional Fase 2):**
  * Integrasi *webhook* ke **Google Forms / Google Sheets** agar Nama, Kelas, dan skor siswa otomatis terekap di spreadsheet guru.
  * Generator angka acak (*dynamic problem generator*) agar siswa bisa mengulang latihan dengan angka yang selalu baru.