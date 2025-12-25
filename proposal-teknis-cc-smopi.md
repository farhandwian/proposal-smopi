# Proposal Teknis
## Integrasi Command Center BBWS Citanduy dengan SMOPI serta Remake Aplikasi Web SMOPI

PT Keen Optima Solution

Tanggal: 25 Desember 2025

---

## 1. Ringkasan Eksekutif
BBWS Citanduy telah memiliki Command Center dengan Bigboard dan Dashboard, namun saat ini belum terintegrasi dengan sistem SMOPI sehingga terjadi perbedaan data pada beberapa aspek (contoh utama: **debit kebutuhan air pada petak tersier**). Selain itu, aplikasi SMOPI yang berjalan memiliki kendala usability (UI/UX), navigasi, performa, keamanan, serta keterbatasan fitur (mis. export Excel) dan beberapa bug.

PT Keen Optima Solution mengusulkan:
- **Remake aplikasi web SMOPI** (perbaikan UI/UX, navigasi, performa, security, serta perbaikan bug).
- **Integrasi parsial** antara SMOPI dan Command Center untuk dataset tertentu, dengan prioritas sinkronisasi **debit kebutuhan air pada petak tersier** agar angka pada Command Center konsisten dengan SMOPI.
- **Integrasi telemetri via API Command Center** untuk mengurangi input manual pada blangko yang membutuhkan data debit (telemetri petak tersier dan telemetri bendung), dengan tetap menyediakan mekanisme penyesuaian manual jika telemetri bermasalah.

Aplikasi akan dibangun sebagai website menggunakan **Next.js**. Untuk peta, digunakan paket yang setara dengan aplikasi “siger” (mis. `@vis.gl/react-google-maps` dan `@turf/turf`). Target durasi pekerjaan: **1 bulan**.

---

## 2. Latar Belakang dan Permasalahan
### 2.1 Kondisi Saat Ini
- SMOPI belum terintegrasi dengan Command Center sehingga terdapat perbedaan data (khususnya debit kebutuhan air).
- Akses telemetri belum tersedia pada SMOPI sehingga data debit perlu diinput manual (default kosong/0).
- UI/UX kurang baik, navigasi membingungkan, beberapa tabel terpotong dan menyulitkan pengisian.
- Performa website lambat.
- Keamanan website kurang baik.
- Terdapat bug pada beberapa menu (contoh: detail daftar TMT bangunan, data tidak muncul pada menu tertentu, duplikasi navbar).
- Tidak ada fitur export Excel (menambah beban kerja operasional).

### 2.2 Tujuan
- Mewujudkan **konsistensi data** antara Command Center dan SMOPI untuk dataset prioritas (debit kebutuhan air pada petak tersier).
- Meningkatkan **efektivitas operasional** melalui integrasi telemetri dan perbaikan UI/UX.
- Meningkatkan **kualitas aplikasi** dari sisi performa, keamanan, dan stabilitas.

---

## 3. Ruang Lingkup
### 3.1 In-Scope
- Remake aplikasi web SMOPI menggunakan Next.js.
- Implementasi modul dan blangko sesuai requirement fungsional (Modul 1–14).
- Integrasi parsial SMOPI → Command Center untuk dataset prioritas: **debit kebutuhan air pada petak tersier**.
- Integrasi telemetri Command Center → SMOPI melalui API untuk:
  - Blangko 06-O (telemetri petak tersier, sebagai default/pre-fill realisasi debit).
  - Blangko 08-O (telemetri bendung, debit sungai).
  - Default nilai pada tabel kondisi air/kerusakan Blangko 04-O (jika tersedia pada telemetri yang relevan).
- Perbaikan UI/UX (navigasi, layout tabel, aksesibilitas), performa, security hardening, dan perbaikan bug.
- Export Excel **difokuskan pada Blangko 04-O** (sesuai kesepakatan fase 1). Untuk blangko lain, fitur keluaran pada fase 1 mengikuti kebutuhan minimal berupa **cetak PDF** sesuai requirement.

### 3.2 Out-of-Scope (Fase Berikutnya)
- Soil Analyzer (Modul 13) sebagai pengembangan selanjutnya.
- Export Excel untuk blangko lainnya (selain 04-O) jika diperlukan di fase lanjutan.
- Perubahan proses bisnis di Command Center di luar integrasi dataset prioritas.

---

## 4. Asumsi dan Ketergantungan
- Command Center menyediakan **telemetri melalui API** (credential, endpoint, dokumentasi, serta mapping ID lokasi) dan dapat diakses dari lingkungan SMOPI baru.
- Data master dan referensi yang diperlukan untuk pemetaan petak tersier/bendung (kode DI, id petak, id bangunan, id bendung) tersedia dan dapat disinkronkan/dipetakan.
- Tidak ada modul khusus “sidang komisi”/workflow komisi terpisah di dalam aplikasi; nilai “Keputusan Komisi Irigasi” dikelola sebagai data input yang diisikan oleh pihak berwenang (diasumsikan role **pengamat**) sesuai hasil sidang/keputusan yang berlaku.

---

## 5. Gambaran Solusi Teknis
### 5.1 Arsitektur Sistem (Ringkas)
SMOPI baru dibangun sebagai aplikasi web Next.js dengan API backend (Route Handlers) dan database terpusat. Integrasi dilakukan ke dua arah secara terpisah:
- **SMOPI → Command Center**: publikasi dataset hasil SMOPI (khususnya debit kebutuhan air petak tersier) untuk konsumsi Bigboard/Dashboard.
- **Command Center → SMOPI**: konsumsi data telemetri via API untuk pre-fill dan efisiensi input.

### 5.2 Diagram Arsitektur Sederhana
```mermaid
flowchart LR
  U[Pengguna Lapangan\n(Pengamat/Juru/POB)] -->|HTTPS| W[Web SMOPI Baru\nNext.js]
  W -->|API Route Handlers| A[Backend API\nAuth + RBAC + Blangko]
  A --> D[(Database\nPostgreSQL + PostGIS*)]

  subgraph CommandCenter[Command Center BBWS Citanduy]
    CCBB[Bigboard/Dashboard]
    CCT[Telemetri API]
  end

  A -->|Fetch Telemetri (API)| CCT
  A -->|Publish kebutuhan air petak tersier (API/Webhook/Job)| CCBB

  A -->|Generate| PDF[PDF Blangko]
  A -->|Generate (khusus 04-O)| XLS[Excel]

  note1[* PostGIS opsional\n(dipakai jika layer GIS memerlukan query spasial)]
```

### 5.3 Teknologi dan Komponen Utama
- Framework: Next.js.
- UI: komponen modern + tabel/grid yang mendukung input massal.
- Peta GIS:
  - `@vis.gl/react-google-maps` untuk rendering peta.
  - `@turf/turf` untuk operasi geospasial (buffer, intersect, dsb bila diperlukan).
- Data & integrasi:
  - Database: PostgreSQL; PostGIS jika diperlukan untuk layer GIS.
  - Integrasi telemetri: konsumsi API Command Center.
  - Integrasi dataset kebutuhan air: endpoint/kontrak data untuk Bigboard/Dashboard.
- Export:
  - Excel khusus Blangko 04-O menggunakan `exceljs`.
  - PDF untuk blangko yang mensyaratkan cetak.
- Keamanan:
  - Auth + RBAC 4 role (pengamat, juru, POB utama, POB suplesi).
  - Hardening dan proteksi API.

---

## 6. Integrasi Data SMOPI–Command Center (Parsial)
### 6.1 Prinsip Integrasi
- Integrasi bersifat **parsial** (tidak semua dataset disinkronkan).
- Dataset prioritas yang disamakan antara SMOPI dan Command Center:
  - **Debit kebutuhan air pada petak tersier** (untuk kebutuhan Bigboard/Dashboard).

### 6.2 Kontrak Data Minimal (Usulan)
Agar integrasi tidak melebar, dataset yang dipublikasikan dari SMOPI minimal memuat:
- Identitas:
  - Kode DI / Daerah Irigasi.
  - ID Petak Tersier (atau key mapping yang disepakati).
  - Periode (tanggal/pekan/periode pemberian air) sesuai kebutuhan Bigboard.
- Nilai:
  - Debit kebutuhan air (angka) + satuan.
  - Timestamp publish.
  - Sumber data (SMOPI) dan versi/skema.

### 6.3 Model Konsistensi dan Audit
- Menggunakan model **eventual consistency**: data di CC akan mengikuti update SMOPI setelah sinkronisasi berjalan.
- Disarankan mekanisme:
  - Idempotency key (menghindari duplikasi update).
  - Retry bila CC tidak dapat menerima update.
  - Pencatatan log sinkronisasi (last sync per periode/DI/petak) untuk audit.

---

## 7. Integrasi Telemetri (Command Center API → SMOPI)
### 7.1 Tujuan
- Mengurangi input manual dan menghindari default 0 untuk:
  - Blangko 06-O (telemetri petak tersier).
  - Blangko 08-O (telemetri bendung).
  - Default nilai pada input kondisi air/kerusakan Blangko 04-O (jika telemetri relevan tersedia).

### 7.2 Mekanisme Fallback
- Jika telemetri tidak tersedia/rusak/berubah, user tetap dapat mengubah nilai (adjustment) dan sistem menyimpan:
  - Nilai awal dari telemetri.
  - Nilai hasil koreksi manual.
  - Metadata (user, waktu, alasan—opsional) untuk audit.

---

## 8. Kebutuhan Fungsional (Lengkap)
Bagian ini memuat seluruh requirement fungsional berdasarkan dokumen kebutuhan.

### 8.1 Modul 1 — Authentication dan RBAC
**Pekerjaan: Login**
- Sistem harus menyediakan fitur login.

**Pekerjaan: Tipe user**
- Sistem harus menyediakan 4 tipe user: pengamat, juru, POB utama, dan POB suplesi.

### 8.2 Modul 2 — Penugasan User / RBAC
**Pekerjaan: Master data (tampilan tabel)**
- Sistem harus menampilkan:
  - Id Wilayah Pengamat
  - Wilayah Kerja Pengamat
  - Pengamat
  - Keterangan
  - Luas (Ha)

**Pekerjaan: List user management**
- Sistem harus menyediakan fitur CRUD untuk pembagian penugasan user yang bisa write oleh pengamat untuk juru, POB utama, dan POB suplesi.

**Pekerjaan: List bendung utama**
- Sistem menyediakan fitur CRUD untuk bendung utama.

**Pekerjaan: List saluran dan bangunan**
- Sistem menyediakan fitur CRUD untuk saluran dan bangunan.

### 8.3 Modul 3 — Pengaturan
**Pekerjaan: List bendung utama**
- Sistem menyediakan fitur CRUD untuk bendung utama.

**Pekerjaan: List saluran dan bangunan**
- Sistem menyediakan fitur CRUD untuk saluran dan bangunan.

**Pekerjaan: List kewenangan bangunan**
- Sistem menyediakan fitur untuk menetapkan kewenangan user terhadap data bangunan yang sudah ada.
- Header Informasi Wilayah:
  - Sistem harus menampilkan ringkasan di bagian atas halaman yang memuat Total Luas (Ha) keseluruhan dan nama Pengamat yang bertugas.
- Tabel Hierarki Data (Tree Table):
  - Sistem menampilkan tabel dengan struktur hierarki (Induk-Anak), di mana:
    - Baris Induk (Parent): menampilkan nama Bangunan dan nama Juru yang bertanggung jawab.
    - Baris Anak (Child): menampilkan detail Petak Tersier di bawah bangunan terkait.
- Visualisasi & Agregasi Luas:
  - Sistem harus membedakan visual kolom Luas (Ha) pada baris Induk (mis. diberi warna latar) yang merupakan total penjumlahan luas petak tersier di bawahnya.
  - Baris anak menampilkan luas area spesifik per petak tersier.
- Tombol Aksi & Navigasi:
  - Sistem menyediakan kolom Action yang berisi tombol pintasan pada setiap baris petak tersier, seperti tombol TMT dan Ref Blangko 5 untuk akses cepat.

### 8.4 Modul 4 — Blangko 01-O
**Pekerjaan: Form**
- Sistem harus menyediakan fitur untuk memilih daerah irigasi dan periode masa tanam.

**Pekerjaan: Tabel**
- Sistem menampilkan tabel dengan baris Jenis Komoditas dan kolom Masa Tanam (MT1, MT2, MT3).
- Pada setiap Masa Tanam, kolom dibagi menjadi dua sub-kolom berdampingan: Usulan dan Keputusan Komisi Irigasi.
- Sistem menyediakan field input untuk mengisi Luas Tanah Usulan pada setiap Masa Tanam.
- Sistem menampilkan data pada kolom Keputusan Komisi Irigasi.

### 8.5 Modul 5 — Blangko 02-O
**Pekerjaan: List blangko**
- Sistem harus menyediakan tabel daftar blangko beserta fitur terkait.

**Pekerjaan: Master data**
- Sistem harus bisa menyimpan dan menampilkan data berikut:
  - Daerah Irigasi
  - No. Kode Irigasi
  - Total Luas Sawah Irigasi
  - Bagian Pelaksana Kegiatan (isian)
  - Perioda Masa Tanam
  - Luas sawah Wil. Ranting/Pengamat
  - Kabupaten

**Pekerjaan: Tabel Rencana Tanam per Wilayah Mantri/Juru per Masa Tanam**
- Tabel Perbandingan:
  - Sistem menampilkan tabel matriks dengan baris Wilayah Kerja Mantri yang membandingkan dua kelompok data utama secara berdampingan:
    - Usulan IP3A/GP3A.
    - Keputusan Komisi Irigasi.
- Detail Komoditas:
  - Pada kedua kelompok (Usulan & Keputusan), sistem memecah kolom berdasarkan jenis tanaman: Padi, Tebu (Muda/Tua), Palawija, Lain-lain, dan Bero.
- Input Keputusan & Jadwal:
  - Sistem menyediakan kolom input (editable) pada bagian Keputusan Komisi Irigasi.
  - Sistem menyediakan kolom input untuk menentukan Golongan air dan Jadwal Pemberian Air (Tanggal Mulai & Akhir) untuk setiap wilayah.
- Kalkulasi & Validasi:
  - Total Baris: sistem otomatis menghitung kolom Jumlah untuk memastikan sesuai Luas Sawah Irigasi.
  - Total Wilayah: sistem menjumlahkan seluruh data angka dari semua Mantri pada baris Jumlah Areal Kerja Ranting di bagian paling bawah.

### 8.6 Modul 6 — Blangko 04A-O dan 04-O
**Pekerjaan: Master data**
- Sistem harus bisa menyimpan dan menampilkan data berikut:
  - Daerah Irigasi
  - No. Kode Irigasi
  - Total Luas Wilayah Irigasi
  - Kabupaten
  - Jumlah Petak Tersier
  - Luas Sawah Mantri
  - Perioda Pemberian Air
  - Keputusan Target Areal Tanam per tanaman (Ha)

**Pekerjaan: Tabel list blangko 04A-O dan 04-O**
- Sistem harus menyediakan tabel daftar blangko beserta fitur terkait.

**Pekerjaan: Tabel Keadaan Air dan Tanaman (Usulan / 04A-O)**
- Sistem menampilkan tabel matriks dengan Petak Tersier sebagai kolom dan Jenis Tanaman/Keadaan Air sebagai baris.
- Sistem menyediakan editable grid agar pengguna bisa menginput data banyak petak tersier sekaligus dalam satu layar.
- Sistem menyediakan filter untuk memilih Tanggal/Periode Laporan.
- Sistem menyediakan form isian untuk Nama Mantri/Juru yang bertanggung jawab.

**Pekerjaan: Tabel Usulan dan Realisasi Luas Tanam (Laporan/Realisasi / 04-O)**
- Sistem menampilkan tabel perbandingan antara Luas Usulan dan Luas Realisasi untuk setiap jenis tanaman.
- Pengguna dapat mengisi angka luas lahan yang sudah ditanam pada kolom Realisasi.
- Sistem menyediakan input form keadaan Air irigasi di Petak Tersier dan kerusakan tanaman dalam tabel matriks sederhana:
  - Baris: Padi, Tebu, Palawija.
  - Kolom: Kekeringan; Genangan/Kebanjiran.
  - Input luas kerusakan: input angka (number stepper) per sel.
  - Nilai default: sistem otomatis menampilkan nilai dari telemetri pada semua kolom input untuk mempercepat pengisian, namun tetap dapat diubah manual.
- Sistem menyediakan input form penanggung jawab laporan dan tanggal laporan.
- Sistem menyediakan fitur cetak PDF dan Excel.

### 8.7 Modul 7 — Blangko 05-O
**Pekerjaan: Master Data**
- Sistem harus bisa menyimpan dan menampilkan data berikut:
  - Daerah Irigasi
  - Nomor Kode DI
  - Total Luas Sawah Irigasi (Ha)
  - Kabupaten
  - Bagian Pelaksana Kegiatan (isian)
  - Kemantren: Jumlah Petak Tersier; Luas Sawah Kemantren
  - Periode Pemberian Air (Tanggal)
  - Daftar Informasi Petak Tersier

**Pekerjaan: Tabel Rencana Kebutuhan di Pintu Pengambilan**
- Sistem menampilkan tabel besar dengan pengelompokan kolom utama berdasarkan Nama Mantri/Juru.
- Pada setiap kolom Mantri, sistem membagi menjadi dua sub-kolom:
  - Usulan Luas Tanam (Ha)
  - Kebutuhan Air di Sawah (l/det)
- Seluruh sel data tidak dapat diedit (disable input) karena nilai dihasilkan dari kalkulasi backend.
- Sistem menampilkan baris data berdasarkan Jenis Tanaman dan Fase Pertumbuhan untuk Padi, Tebu, Palawija.
- Baris Total & Kesimpulan di bagian bawah memuat:
  - Jumlah di Sawah
  - Kebutuhan Air di Pintu Tersier
  - Kerusakan Tanaman
- Sistem menyediakan form isian tanggal dan informasi penanggung jawab.
- Sistem menyediakan fitur cetak PDF.

### 8.8 Modul 8 — Blangko 06-O
**Pekerjaan: Master data**
- Sistem harus bisa menyimpan dan menampilkan:
  - Daerah Irigasi
  - No. Kode Irigasi
  - Total Luas Wilayah Irigasi
  - Kabupaten
  - Bagian Pelaksanaan Kegiatan (input)
  - Perioda Masa Tanam
  - Daerah Ranting
  - Daerah Mantri
  - Luas Sawah Mantri

**Pekerjaan: Tabel Pencatatan Debit**
- Sistem menampilkan tabel dengan hierarki baris berdasarkan Nama Bangunan Kontrol (Bagi/Sadap) dan informasi Petak Tersier terkait.
- Sistem menampilkan kolom debit harian yang pre-filled dari database, namun tetap editable.
- Sistem menghitung ulang Jumlah Debit dan Debit Rata-rata otomatis ketika nilai berubah.
- Sistem menyediakan opsi Cara Pengukuran (radio) default dari database, namun editable.
- Sistem menyediakan opsi Kondisi Alat Ukur (radio) yang bisa diisi user.
- Sistem menyediakan form isian tanggal dan informasi penanggung jawab.
- Sistem menyediakan fitur cetak PDF.

### 8.9 Modul 9 — Blangko 07-O
**Pekerjaan: Master Data**
- Sistem harus bisa menyimpan dan menampilkan:
  - Daerah Irigasi
  - Nomor Kode DI
  - Jumlah Petak Tersier
  - Total Luas Sawah Irigasi
  - Dinas
  - UPTD
  - Periode Pemberian Air (Tanggal)
  - Daftar Informasi Petak Tersier

**Pekerjaan: Tabel List Blangko**
- Sistem harus menyediakan tabel daftar blangko.

**Pekerjaan: Tabel Rencana Kebutuhan Air di Jaringan Utama dan Penetapan Pemberian Air**
- Sistem menampilkan tabel berjenjang (tree view): Mantri/Juru → Bangunan Kontrol → Petak Tersier.
- Sistem menampilkan data referensi (read-only):
  - Luas Sawah Tersier (Ha)
  - Realisasi Debit Periode Lalu (historis rata-rata dan akhir periode)
  - Usulan Luas Tanam (Ha) dari Rencana Tata Tanam (Blangko 01/04)
- Sistem menghitung otomatis Qt pada level petak dan agregasi ke Bangunan/Mantri (Luas Tanam × Faktor Kebutuhan Air/NFR).
- Sistem menyediakan input editable khusus baris rekap Mantri/Juru untuk:
  - Ql (Kebutuhan lain-lain)
  - Qh (Kehilangan air)
  - Qs (Debit suplesi)
- Sistem menghitung otomatis Qb: (Total Qt + Ql + Qh) – Qs.
- Sistem menyediakan kolom Debit Diberikan sebagai hasil akhir alokasi.
- Sistem menyediakan isian tanggal, wilayah, serta informasi terkait juru/pengamat.
- Sistem menyediakan fitur cetak PDF.

### 8.10 Modul 10 — Blangko 08-O
**Pekerjaan: Master Data**
- Sistem harus bisa menyimpan dan menampilkan:
  - Nama Sungai
  - Nama Bendung
  - Daerah Irigasi
  - Total Luas Sawah Irigasi
  - Kabupaten
  - Daerah Ranting/Pengamat
  - Bagian Pelaksanaan Kegiatan
  - Periode Pemberian Air

**Pekerjaan: Tabel list**
- Sistem menampilkan tabel list Blangko 08-O per bulan.

**Pekerjaan: Detail Blangko 08**
- Sistem menampilkan detail tabel pengambilan/pencatatan debit sungai dari telemetri bendung.
- Sistem dapat mencetak Blangko 08.
- Sistem menyediakan fitur verifikasi untuk user pengamat.

### 8.11 Modul 11 — Blangko 09-O
**Pekerjaan: Master Data**
- Sistem harus bisa menyimpan dan menampilkan:
  - Daerah Irigasi
  - No Kode Irigasi
  - Total Luas Sawah Irigasi
  - Kabupaten
  - Periode Pemberian Air

**Pekerjaan: Tabel List**
- Sistem menampilkan tabel list Blangko 09-O per periode tiap tahun.
- Sistem menampilkan debit diperlukan (data dari Blangko 07-O) dan telah dikalkulasi.
- Sistem menampilkan debit tersedia (data dari Blangko 08-O) dan telah dikalkulasi.
- Sistem menampilkan debit dialirkan.
- Sistem menampilkan perhitungan faktor K dan telah dikalkulasi.
- Sistem dapat cetak PDF untuk Blangko 09.

### 8.12 Modul 12 — Blangko 10-O
**Pekerjaan: Tabel List Blangko**
- Sistem menampilkan pesan peringatan bahwa blangko pendahulu (04A s/d 09) wajib selesai sebelum memproses halaman ini.
- Sistem menampilkan list tabel data untuk blangko.

**Pekerjaan: Master data**
- Sistem harus bisa menyimpan dan menampilkan:
  - Daerah Irigasi
  - No. Kode Irigasi
  - Total Luas Wilayah Irigasi
  - Kabupaten
  - Jumlah Petak Tersier
  - Luas Areal Kerja Ranting/Pengamat
  - Jumlah Mantri/Juru
  - Bagian Pelaks. Kegiatan (isian)

**Pekerjaan: Tabel Realisasi Tanam dan Keadaan Air**
- Sistem menampilkan tabel baris waktu Oktober s/d September dibagi Periode 1 dan 2.
- Kolom dikelompokkan: Padi (MT1–3), Palawija (MT1–3), Tebu, Lain-lain.
- Sistem menampilkan data luas tanam (Ha) hasil rekap input periode sebelumnya (read-only).
- Sistem menampilkan kolom Bero dihitung: total luas baku – total luas tanam.
- Sistem menampilkan kolom data hidrologi untuk setiap periode:
  - Debit Tersedia: total debit, debit pengambilan, Q limpas bendung.
  - Faktor Koreksi: kehilangan air, Q suplesi.
  - Kebutuhan Air: kebutuhan di tersier, kebutuhan lain-lain.
  - Analisa: faktor K rata-rata, debit rencana, neraca air.

**Pekerjaan: Tabel Statistik, Kerusakan, Rencana Tanam**
- Sistem menghitung dan menampilkan puncak luas tanam dan intensitas tanam (%) otomatis.
- Sistem menampilkan rekap data kerusakan (kekeringan/banjir) per jenis tanaman (data dari laporan sebelumnya/Blangko 07).
- Sistem menyediakan input editable untuk Rencana YAD.
- Sistem menampilkan data Rencana Tanam Tahun Ini sebagai referensi (read-only).

**Pekerjaan: Tabel Produksi Tanaman**
- Sistem mengambil puncak luas tanam dari tabel statistik sebagai basis.
- Sistem menyediakan input editable Data Ubinan/Rata-rata Produksi (Ton/Ha).
- Sistem menghitung otomatis produksi per tanaman: puncak luas tanam × data ubinan.
- Sistem menjumlahkan seluruh produksi menjadi total jumlah produksi (Ton) di baris bawah.

**Pekerjaan: Laporan**
- Sistem mendukung fitur cetak PDF.
- Sistem menyediakan form isian tanggal dan informasi terkait pengamat/ranting.

### 8.13 Modul 13 — Soil Analyzer (Pengembangan Selanjutnya)
- Sistem bisa otomatis mendeteksi genangan/kebanjiran atau kekeringan (merujuk Blangko 04-O).

### 8.14 Modul 14 — Peta Visualisasi Petak Tersier dan Pintu Air
- Sistem menampilkan peta untuk memvisualisasikan petak tersier dan pintu air menggunakan data GIS yang ada.

---

## 9. Kebutuhan Non-Fungsional (Mengacu Tantangan)
### 9.1 UI/UX dan Usability
- Navigasi sederhana dan konsisten.
- Tabel input tidak terpotong; mendukung layar lapangan.
- User role juru dapat menjalankan workflow utama tanpa kebingungan.

### 9.2 Performa
- Optimasi load data untuk tabel besar (pagination/virtualization).
- Respons cepat pada input grid (khusus 04A/04-O).

### 9.3 Keamanan
- RBAC konsisten di UI dan API.
- Proteksi terhadap akses tanpa kewenangan.
- Logging aktivitas penting (login, perubahan data kritikal).

### 9.4 Stabilitas dan Bugfix
- Perbaikan bug yang sudah teridentifikasi (detail TMT bangunan tidak muncul, duplikasi navbar, halaman list/detail tertentu).

---

## 10. Rencana Pengerjaan (1 Bulan)
### Minggu 1 — Fondasi & Desain
- Finalisasi scope, mapping data petak tersier/bendung, dan kontrak integrasi dataset kebutuhan air.
- Setup arsitektur Next.js, struktur modul, dan RBAC.
- Desain UI/UX untuk alur input utama blangko.

### Minggu 2 — Implementasi Modul Inti & Blangko Prioritas
- Implement modul authentication + RBAC (4 role).
- Implement modul penugasan + pengaturan (kewenangan bangunan/tree table).
- Implement Blangko 04A-O & 04-O (editable grid, filter periode).

### Minggu 3 — Integrasi Telemetri + Export Excel (04-O)
- Integrasi telemetri API untuk Blangko 06-O dan 08-O (serta default nilai 04-O jika tersedia).
- Implement export Excel khusus Blangko 04-O.
- Implement cetak PDF sesuai kebutuhan blangko terkait.

### Minggu 4 — Integrasi SMOPI→Command Center, Hardening, UAT, Handover
- Implement publikasi dataset debit kebutuhan air petak tersier untuk Bigboard/Dashboard.
- Hardening security dan optimasi performa.
- UAT dengan stakeholder, perbaikan bug, finalisasi dokumentasi.

---

## 11. Deliverables
- Aplikasi web SMOPI (remake) dengan modul dan blangko sesuai scope.
- Integrasi telemetri (Command Center API → SMOPI) untuk blangko terkait.
- Integrasi dataset kebutuhan air petak tersier (SMOPI → Command Center).
- Fitur cetak PDF untuk blangko yang mensyaratkan.
- Export Excel untuk Blangko 04-O.
- Dokumen:
  - Diagram arsitektur & data flow.
  - Matriks role & akses.
  - Kontrak integrasi dataset kebutuhan air.
  - Panduan penggunaan singkat.

---

## 12. Risiko dan Mitigasi
- Risiko: Pemetaan ID petak tersier/bendung tidak konsisten antar sistem.
  - Mitigasi: definisikan mapping table dan lakukan validasi awal (sampling) sebelum UAT.
- Risiko: Telemetri API tidak stabil atau data tidak lengkap.
  - Mitigasi: fallback manual adjustment + pencatatan sumber data.
- Risiko: Scope blangko sangat luas untuk 1 bulan.
  - Mitigasi: prioritisasi workflow inti (04A/04-O, 06-O, 08-O, integrasi kebutuhan air), dan fasekan fitur non-kritis.

---

## 13. Penutup
Proposal ini dirancang untuk menyelesaikan dua kebutuhan utama BBWS Citanduy: (1) konsistensi data prioritas antara SMOPI dan Command Center (debit kebutuhan air petak tersier), serta (2) peningkatan kualitas SMOPI melalui remake web yang lebih mudah digunakan, lebih cepat, dan lebih aman.
