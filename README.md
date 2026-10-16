# 📊 Analisis Turnover Rate Suatu Perusahaan

## 📌 Overview Project
Project ini bertujuan untuk menganalisis tren turnover karyawan pada suatu perusahaan, serta mengidentifikasi departemen dan profil karyawan yang paling banyak keluar.

Analisis dilakukan menggunakan **Employee Data** yang berisi informasi karyawan seperti tanggal mulai dan keluar kerja, jabatan, departemen, tipe pemutusan hubungan kerja, tanggal lahir, jenis kelamin, dan skor kinerja.

Melalui analisis ini diharapkan dapat diperoleh insight yang membantu tim HR memahami pola pengunduran diri sehingga strategi retensi karyawan dapat dirancang dengan lebih tepat.

## ❗ Problem Statement
Menurut riset yang dikutip dari Forbes, sekitar 46% karyawan Gen Z berencana resign dalam waktu dekat. Alasannya bukan karena mudah bosan, melainkan karena mereka merasa lelah dan memiliki alasan yang kuat untuk pergi.

> Sumber: [Parapuan – Karyawan Gen Z Mudah Resign, Bagaimana Cara Perusahaan Mencegahnya?](https://www.parapuan.co/read/534329009/karyawan-gen-z-mudah-resign-bagaimana-cara-perusahaan-mencegahnya) (9 Desember 2025)

Dengan menganalisis data karyawan, kita dapat mengetahui siapa yang paling banyak keluar dan pada titik waktu kapan. Insight dari analisis ini dapat membantu:

- Tim HR dalam merancang program retensi yang tepat sasaran
- Manajemen dalam memahami departemen dan posisi yang paling rentan kehilangan karyawan
- Perusahaan dalam menjaga karyawan berkinerja baik agar tidak berpindah ke kompetitor

## ❓ Business Question
Beberapa pertanyaan yang ingin dijawab dalam analisis ini antara lain:

1. Bagaimana tren pergerakan turnover perusahaan saat ini?
2. Apakah tingginya angka pengunduran diri didominasi oleh karyawan berkinerja buruk?
3. Departemen manakah yang menjadi penyumbang turnover terbesar, dan demografi karyawan seperti apa yang paling membutuhkan intervensi retensi?

## 📊 Dataset
- **Nama:** Employee Data
- **Sumber:** [Kaggle](https://www.kaggle.com/datasets/ravindrasinghrana/employeedataset)
- **Format:** CSV
- **Jumlah baris:** 3.000
- **Jumlah kolom:** 26

Kolom utama pada dataset:

| Kelompok | Kolom |
|---|---|
| Identitas dan posisi | Employee ID, Title, Supervisor, Business Unit, Department Type, Division Description, Job Function |
| Status kepegawaian | Start Date, Exit Date, Employee Status, Employee Type, Employee Classification Type, Pay Zone |
| Pemutusan hubungan kerja | Termination Type, Termination Description |
| Demografi | DOB, Gender, State, Location, Race (or) Ethnicity, Marital Status |
| Kinerja | Performance Score, Current Employee Rating |

> Kolom yang berisi data pribadi (nama dan email) tidak dibahas dalam analisis ini.

## 🧹 Data Preparation
1. **Tipe data:** diperiksa menggunakan Power Query. Kolom tanggal (StartDate, ExitDate, DOB) bertipe `Date`, kolom angka (EmpID) bertipe `Whole Number`, dan kolom teks bertipe `Text`.
2. **Duplicate value:** tidak ditemukan.
3. **Outlier:** pemeriksaan dengan metode IQR menemukan outlier sebesar 9% pada kolom Current Employee Rating. Penanganan berupa validasi ulang dengan pemberi data, dan apabila valid maka tidak dilakukan penanganan.
4. **Missing value:** ditemukan pada kolom Exit Date dan Termination Description sebesar 49%. Hal ini wajar karena karyawan yang masih aktif belum memiliki tanggal keluar, sehingga tidak ada penanganan.
5. **Inkonsistensi:** pada kolom Title terdapat dua entri "Data Analyst" akibat spasi berlebih, diperbaiki dengan fungsi `TRIM`.
6. **Feature Engineering:**
   - `EmployeeStatus` dibuat ulang berdasarkan ada atau tidaknya Exit Date, karena sebagian karyawan memiliki Exit Date namun statusnya masih "Active"
   - Kolom durasi bekerja (bulan) sampai karyawan menjadi tidak aktif
   - Kolom usia saat keluar beserta kategori usia (remaja, dewasa, lansia)
   - `EmployeeType` dipakai karena nilainya lebih jelas (Full-Time, Part-Time, Contract) dibandingkan `EmployeeClassificationType`
   - Kolom Termination Type baru yang lebih spesifik (Mengundurkan Diri, Pensiun, PHK)

## 📈 KPI Utama

| Total Karyawan | Total Turnover | Turnover Rate | Rata-rata Durasi Bekerja |
|:---:|:---:|:---:|:---:|
| 3.000 | 1.533 | 51,1% | 16 bulan |

## 🔍 Insight dari Data

Perusahaan mencatat **turnover rate 51,1%** (1.533 dari 3.000 karyawan) dengan **tren kenaikan setiap tahun**, dari 4 karyawan pada 2018 menjadi 596 pada 2023, dan **rata-rata karyawan keluar setelah 16 bulan** bekerja. Penyumbang terbesar adalah departemen **Production (1.014 karyawan)** dengan perbedaan yang sangat signifikan dibanding departemen lain, dan **507 di antaranya mengundurkan diri**. Pengunduran diri dari Production **didominasi perempuan (69%) berusia dewasa** dengan **performa baik (Fully Meets)**, terutama pada posisi **Production Technician I dan II**, sehingga yang keluar justru karyawan yang berkinerja baik dan bukan yang berkinerja rendah.

## 💡 Recommendation

Karena rata-rata karyawan mengundurkan diri pada bulan ke-16, disarankan untuk **menjadwalkan stay interview dan diskusi proyeksi karir pada bulan ke-12**, khususnya bagi Production Technician, agar ketidakpuasan dapat dideteksi sebelum karyawan mencapai titik jenuh. Selain itu, dapat dipertimbangkan **program retensi dan reward bagi karyawan berkinerja baik (Fully Meets)**, misalnya penyesuaian gaji, bonus retensi akhir tahun, atau prioritas pelatihan upskilling, agar mereka tidak berpindah ke kompetitor. Terakhir, disarankan untuk **meninjau fasilitas dan ergonomi kerja lapangan bagi perempuan**, mencakup evaluasi shift yang lebih seimbang, penyediaan fasilitas khusus di area pabrik, serta perbaikan ergonomi untuk mencegah kelelahan fisik yang memicu pengunduran diri.

## 📊 Dashboard
Dashboard interaktif dibuat di Excel dengan slicer **ExitDate (timeline)**, **Employee Status**, **Department**, **Gender**, **Kelompok Usia**, **Tipe Terminasi**, dan **Performance Score**, terdiri dari:

- 4 KPI (Total Karyawan, Total Turnover, Turnover Rate, Rata-rata Durasi Karyawan)
- Jumlah karyawan berdasarkan status
- Timeline jumlah turnover tahunan
- Turnover per departemen
- Turnover berdasarkan tipe terminasi
- Turnover berdasarkan klasifikasi usia dan gender
- Turnover berdasarkan performance score dan title

> 📷 Tambahkan screenshot dashboard di sini:
> 📊 [Dashboard]([images/dashboard.png](https://github.com/ahmad2129/Analisis-Turnover-Rate-Suatu-Perusahaan/blob/main/dashboard/Dashboard%20Excel.png))

## 📊 Presentasi Project
Untuk melihat penjelasan lengkap dari project ini, silakan lihat slide presentasi berikut:

🔗 [Slide Presentasi](https://github.com/ahmad2129/Analisis-Turnover-Rate-Suatu-Perusahaan/blob/main/report/Presentasi%20Mini%20Project%20Excel%20Ahmad%20Malik%20Ibrahim.pdf)

## 🛠 Tools yang Digunakan
- **Microsoft Excel** (Pivot Table, Slicer, dan Dashboard)
- **Power Query** (Pemeriksaan dan pengaturan tipe data)

## 👤 Author
**Ahmad Malik Ibrahim**
Lulusan kedokteran dengan minat pada statistik, analisis, dan matematika, yang sedang menargetkan karir sebagai data analis.
