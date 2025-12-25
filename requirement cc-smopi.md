1.Modul authentication dan rbac
Pekerjaan:
a.login
fungsional requirement:
-sistem haru menyediakan fitur login
b.tipe user
fungsional requirement:
-sistem harus menyediakan 4 tipe user pengamat, juru, pob utama, dan pob suplesi
 
2.Modul penugasan user/rbac
Pekerjaan:
a.master data
fungsional requirement:
- sistem harus menampilkan:
Id Wilayah Pengamat
Wilayah Kerja Pengamat
Pengamat
Keterangan
Luas(HA)
b. list user management
fungsional requirement:
- sistem harus menyediakan fitur crud untuk pembagian penugasan user yang bisa write oleh pengamat untuk juru, pob utama, dan pob suplesi
c. list bendung utama
fungsional requirement:
- sistem menyediakan fitur crud untuk bendung utama
d. list saluran dan bangunan
fungsional requirement:
- sistem menyediakan fitur crud untuk saluran dan bangunan
 
3.modul pengaturan
Pekerjaan:
a. list bendung utama
fungsional requirement:
- sistem menyediakan fitur crud untuk bendung utama
b. list saluran dan bangunan
fungsional requirement:
sistem menyediakan fitur crud untuk saluran dan bangunan
c. list kewenangan bangunan
fungsional requirement:
- sistem menyedikan fitur untuk menetapkan kewenangan user terhadap data bangunan yang sudah ada
- Header Informasi Wilayah:
Sistem harus menampilkan informasi ringkasan di bagian atas halaman yang memuat Total Luas (Ha) keseluruhan dan nama Pengamat yang bertugas.
- Tabel Hierarki Data (Tree Table):
Sistem menampilkan tabel dengan struktur hierarki (Induk-Anak) di mana:
Baris Induk (Parent): Menampilkan nama Bangunan (misal: BCk. 8) dan nama Juru yang bertanggung jawab.
Baris Anak (Child): Menampilkan detail Petak Tersier (misal: BCk 8 Ka) di bawah bangunan terkait.
- Visualisasi & Agregasi Luas:
Sistem harus membedakan visual kolom Luas (Ha) pada baris Induk (biasanya diberi warna latar kuning) yang merupakan total penjumlahan dari luas petak-petak tersier di bawahnya.
Baris anak menampilkan luas area spesifik per petak tersier.
- Tombol Aksi & Navigasi:
Sistem menyediakan kolom Action yang berisi tombol pintasan (shortcut buttons) pada setiap baris petak tersier, seperti tombol TMT dan Ref Blangko 5 untuk mengakses detail atau referensi formulir terkait secara cepat.
 
4. modul blangko 01-o
Pekerjaan:
a. form
fungsional requirement:
- sistem harus bisa menyediakan fitur untuk memilih daerah irigasi dan periode masa tanam
b. tabel
fungsional requirement:
- Sistem menampilkan tabel dengan baris Jenis Komoditas dan kolom Masa Tanam (MT 1, MT 2, MT 3).
- Pada setiap Masa Tanam, kolom harus dibagi menjadi dua sub-kolom berdampingan: Usulan dan Keputusan Komisi Irigasi
- Sistem menyediakan field yang dapat diinput untuk mengisi Luas Tanah Usulan pada setiap Masa Tanam.
- Sistem menampilkan data pada kolom Keputusan Komisi Irigasi (data ini bisa bersifat read-only dari hasil sidang komisi atau input khusus admin).
 
5. modul blangko 02-o
Pekerjaan:
a. list blangko
fungsional requirement:
-  sistem harus menyediakan tabel daftar blangko beserta fitur terkait
b. master data
fungsional requirement:
- Sistem Harus bisa menyimpan dan menampilkan data berikut:
Daerah Irigasi
No. Kode Irigasi
Total Luas Sawah Irigasi
Bagian Pelaksana Kegiatan berupa isian
Perioda Masa Tanam
Luas sawah Wil. Ranting/Pengamat
Kabupaten
c. tabel RENCANA TANAM PER WILAYAH MANTRI/JURU PER MASA TANAM
fungsional requirement:
- Tabel Perbandingan: Sistem menampilkan tabel matriks dengan baris Wilayah Kerja Mantri yang membandingkan dua kelompok data utama secara berdampingan:
Usulan IP3A/GP3A: Data rencana yang diajukan petani/perkumpulan.
Keputusan Komisi Irigasi: Data final yang telah disetujui dalam sidang komisi.
- Detail Komoditas: Pada kedua kelompok tersebut (Usulan & Keputusan), sistem harus memecah kolom berdasarkan jenis tanaman: Padi, Tebu (Muda/Tua), Palawija, Lain-lain, dan Bero (Lahan kosong).
- Input Keputusan & Jadwal:
Sistem menyediakan kolom input (editable) pada bagian Keputusan Komisi Irigasi untuk merevisi angka jika ada perubahan dari usulan.
Sistem menyediakan kolom input untuk menentukan Golongan air dan Jadwal Pemberian Air (Tanggal Mulai & Akhir) untuk setiap wilayah.
- Kalkulasi & Validasi:
Total Baris: Sistem otomatis menghitung kolom Jumlah (Total Luas) untuk memastikan angkanya sesuai dengan Luas Sawah Irigasi yang tersedia.
Total Wilayah: Sistem harus menjumlahkan seluruh data angka dari semua Mantri pada baris Jumlah Areal Kerja Ranting di bagian paling bawah.
 
6. modul Blangko 04a-o dan 04-o
Pekerjaan:
a. master data
fungsional requirement:
- Sistem Harus bisa menyimpan dan menampilkan data berikut:
Daerah Irigasi
No. Kode Irigasi
Total Luas Wilayah Irigasi
Kabupaten
Jumlah Petak Tersier
Luas Sawah Mantri
Perioda Pemberian Air
Keputusan Target Areal Tanam per tanaman(ha)
b. tabel list blangko untuk 04a-o dan 04-o
fungsional requirement:
- sistem harus menyediakan tabel daftar blangko fitur terkait
c. tabel Keadaan Air dan Tanaman Pada Wilayah Mantri/Juru(usulan/04a-o)
fungsional requirement:
- Sistem menampilkan tabel matriks dengan Petak Tersier sebagai kolom dan Jenis Tanaman/Keadaan Air sebagai baris.
- Sistem menyediakan tabel yang dapat diisi langsung (editable grid) agar pengguna bisa menginput data untuk banyak Petak Tersier sekaligus dalam satu layar
- Sistem menyediakan filter untuk memilih Tanggal/Periode Laporan.
- Sistem menyediakan form isian untuk Nama Mantri/Juru yang bertanggung jawab atas data tersebut.
d. tabel usulan dan realisasi luas tanam(laporan/realisasi/04-o)
fungsional requirement:
- Sistem menampilkan tabel perbandingan antara Luas Usulan dan Luas Realisasi untuk setiap jenis tanaman
- Pengguna dapat mengisi angka luas lahan yang sudah ditanam pada kolom Realisasi.
- sistem harus menyediakan input form untuk keadaan Air irigasi di Petak Tersier dan kerusakan tanaman dengan menampilkan tabel input sederhana dengan struktur matriks:
Baris: Kategori tanaman utama (Padi, Tebu, Palawija).
Kolom: Jenis penyebab kerusakan (Kekeringan, Genangan/Kebanjiran).
Input Luas Kerusakan: Sistem menyediakan kolom input angka (number stepper) yang dapat diedit pada setiap sel untuk mengisi luas lahan yang rusak (biasanya dalam Ha).
Nilai Default: Sistem secara otomatis menampilkan nilai yang diambil dari telemetri pada semua kolom input untuk mempercepat pengisian jika tidak ada kerusakan, namun nilai ini tetap bisa diubah manual oleh pengguna.
- sistem harus menyediakan input form terkait penanggung jawab laporan dan tanggal laporan.
- sistem harus menyediakan fitur cetak pdf dan excel.
 
7. modul Blangko 05 – O
Pekerjaan:
a. Master Data
fungsional requirement:
- Sistem Harus bisa menyimpan dan menampilkan data berikut:
Daerah Irigasi
Nomor Kode DI
Total Luas Sawah Irigasi (ha)
Kabupaten
Bagian Pelaksana Kegiatan berupa isian
Kemantren:
Jumlah Petak Tersier
Luas Sawah Kemantren
Periode Pemberian Air (Tanggal)
Daftar Informasi Petak Tersier
b. Tabel Rencana Kebutuhan di Pintu Pengambilan
fungsional requirement:
- Sistem menampilkan tabel besar dengan pengelompokan kolom utama berdasarkan Nama Mantri/Juru.
- Pada setiap kolom Mantri, sistem harus membagi lagi menjadi dua sub-kolom:
Usulan Luas Tanam (Ha): Menampilkan luas lahan yang direncanakan.
Kebutuhan Air di Sawah (l/det): Menampilkan debit air yang dibutuhkan.
- Seluruh sel data pada tabel ini harus bersifat tidak dapat diedit (disable input) oleh pengguna, karena nilai dihasilkan dari kalkulasi sistem (Backend).
- Sistem menampilkan baris data yang dikategorikan berdasarkan Jenis Tanaman dan Fase Pertumbuhan (misal: Pengolahan Tanah, Pertumbuhan, Panen) untuk Padi, Tebu, dan Palawija.
- Baris Total & Kesimpulan: Sistem harus menampilkan baris rekapitulasi di bagian paling bawah yang memuat:
Jumlah di Sawah: Total debit air yang dibutuhkan di lahan.
Kebutuhan Air di Pintu Tersier: Total debit akhir yang harus disuplai (termasuk faktor kehilangan air).
Kerusakan Tanaman: Data monitoring kerusakan (jika ada).
- sistem harus menyediakan form isian untuk tanggal dan isian untuk informasi penanggung jawab
- sistem harus menyediakan fitur cetak pdf
 
8. modul Blangko 06-o
Pekerjaan:
a. master data
fungsional requirement:
- Sistem Harus bisa menyimpan dan menampilkan data berikut:
Daerah Irigasi
No. Kode Irigasi
Total Luas Wilayah Irigasi
Kabupaten
Bagian Pelaksanaan kegiatan berupa input
Perioda Masa Tanam
Daerah Ranting
Daerah Mantri
Luas Sawah Mantri
b. Tabel Pencatatan Debit
fungsional requirement:
- Sistem menampilkan tabel dengan hierarki baris berdasarkan Nama Bangunan Kontrol (Bagi/Sadap) dan menampilkan informasi Petak Tersier terkait
- Sistem harus menampilkan kolom debit harian yang sudah terisi otomatis (pre-filled) dengan nilai dari database (Backend), namun kolom tersebut harus tetap dapat diedit/diubah manual oleh pengguna
- Sistem harus menghitung ulang Jumlah Debit dan Debit Rata-rata secara otomatis ketika pengguna mengubah nilai default maupun menginput nilai baru.
-  Sistem menyediakan opsi Cara Pengukuran (Radio Button) yang status awalnya (default selection) diambil dari database, namun tetap dapat diubah oleh pengguna.
- Sistem menyediakan opsi Kondisi Alat Ukur (Radio Button) yang bisa diisi oleh pengguna
- Sistem menyediakan form isian untuk tanggal dan untuk informasi penanggung jawab
- Sistem menyediakan fitur cetak pdf
 
9. modul Blangko 07-o
Pekerjaan:
a. Master Data
fungsional requirement:
- Sistem Harus bisa menyimpan dan menampilkan:
Daerah Irigasi
Nomor Kode DI
Jumlah Petak Tersier
Total Luas Sawah Irigasi
Dinas
UPTD
Periode Pemberian Air (Tanggal)
Daftar Informasi Petak Tersier
b. Tabel List Blangko
fungsional requirement:
- sistem harus menyediakan tabel daftar blangko
c. Tabel Rencana Kebutuhan Air di Jaringan Utama dan Penetapan Pemberian Air
fungsional requirement:
- Sistem menampilkan tabel dengan struktur berjenjang (tree view) yang dimulai dari level Mantri/Juru, turun ke Bangunan Kontrol, hingga detail Petak Tersier.
- Sistem otomatis menampilkan data referensi yang tidak bisa diedit:
Luas Sawah Tersier (Ha): Data statis wilayah.
Realisasi Debit Periode Lalu: Data historis rata-rata dan akhir periode sebelumnya.
Usulan Luas Tanam (Ha): Diambil dari Rencana Tata Tanam (Blangko 01/04).
- Sistem menghitung otomatis Kebutuhan Air di Pintu Tersier (Qt) pada level petak, lalu menjumlahkannya ke level Bangunan dan Mantri (Rumus: Luas Tanam x Faktor Kebutuhan Air/NFR)
- Sistem menyediakan kolom input (editable) khusus pada baris rekapitulasi (Level Mantri/Juru) untuk variabel:
Kebutuhan Lain-lain (Ql)
Kehilangan Air (Qh)
Debit Suplesi (Qs)
- Sistem menghitung otomatis Kebutuhan Air di Bangunan Bagi (Qb) dengan rumus neraca: (Total Qt + Ql + Qh) – Qs
- Sistem harus menyediakan kolom Debit Diberikan sebagai hasil akhir alokasi air.
- Sistem menyediakan isian untuk tanggal, wilayah serta informasi terkait dengan juru/pengamat
- Sistem menyediakan fitur cetak pdf
 
10. modul Blangko 08-o
Pekerjaan:
a. Master Data
fungsional requirement:
- Sistem Harus bisa menyimpan dan menampilkan:
Nama Sungai
Nama Bendung
Daerah Irigasi
Total Luas Sawah Irigasi
Kabupaten
Daerah Ranting/Pengamat
Bagian Pelaksanaan Kegiatan
Periode Pemberian Air
b. Tabel list
fungsional requirement:
- Sistem dapat menampilkan tabel list blangko 08-0 per bulan
c. Detail Blangko 08
fungsional requirement:
- Sistem dapat menampilkan (detail) tabel pengambilan / pencatatan debit sungai dengan data diambil dari telemetri bendung
- Sistem dapat mencetak blangko 08
- Sistem dapat menyediakan fitur verifikasi untuk user pengamant
 
11. modul Blangko 09-o
Pekerjaan:
a. Master Data
fungsional requirement:
- Sistem Harus bisa menyimpan dan menampilkan:
Daerah Irigasi
No Kode Irigasi
Total Luas Sawah Irigasi
Kabupaten
Periode Pemberian Air
b. Tabel List
fungsional requirement:
- Sistem dapat menampilkan tabel list blangko 09-O per periode tiap tahun
- Sistem dapat menampilkan tabel debit diperlukan (data diambil dari blangko 07-0) dan telah dikalkulasi
- Sistem dapat menampilkan tabel debit tersedia (data diambil dari blangko 08-0) dan telah dikalkulasi
- Sistem dapat menampilkan tabel debit dialirkan
- Sistem dapat menampilkan tabel perhitungan faktor K dan telah dikalkulasi
- Sistem dapat cetak PDF untuk blangko-09
 
12. modul Blangko 10-0
Pekerjaan:
a. Tabel List Blangko
fungsional requirement:
- Sistem menampilkan pesan peringatan bahwa Blangko pendahulu (04A s/d 09) wajib selesai sebelum memproses halaman ini.
- Sistem harus menampilkan list tabel data untuk blangko
b. master data
fungsional requirement:
- Sistem Harus bisa menyimpan dan menampilkan data berikut:
Daerah Irigasi
No. Kode Irigasi
Total Luas Wilayah Irigasi
Kabupaten
Jumlah Petak Tersier
Luas Areal Kerja Ranting/Pengamat
Jumlah Mantri/Juru
Bagian Pelaks.Kegiatan berupa isian
c. Tabel Realisasi Tanam dan keadaan air
fungsional requirement:
- Sistem menampilkan tabel dengan baris urutan waktu (Oktober s/d September) yang dibagi menjadi Periode 1 dan 2 (setengah bulanan)
- Kolom tabel harus dikelompokkan berdasarkan jenis tanaman: Padi (MT1, MT2, MT3), Palawija (MT1, MT2, MT3), Tebu, dan Lain-lain
- Sistem menampilkan data luas tanam (Ha) pada setiap sel yang merupakan hasil rekapitulasi dari input laporan periode sebelumnya (Data bersifat Read-Only)
- Sistem menampilkan kolom Bero (lahan kosong) yang dihitung dari total luas baku dikurangi total luas tanam
- Sistem menampilkan kolom-kolom data hidrologi untuk setiap periode tersebut, meliputi:
Debit Tersedia: (Total debit, Debit Pengambilan, Q Limpas Bendung).
Faktor Koreksi: (Kehilangan Air, Q Suplesi).
Kebutuhan Air: (Kebutuhan di Tersier, Kebutuhan Lain-lain).
Analisa: (Faktor K Rata-rata, Debit Rencana, Neraca Air).
d. Tabel Statistik, Kerusakan, Rencana Tanam
fungsional requirement:
- Sistem harus menghitung dan menampilkan Puncak Luas Tanam dan Intensitas Tanam (persentase) secara otomatis untuk setiap musim tanam
- Sistem menampilkan rekapitulasi data kerusakan (Kekeringan/Banjir) berdasarkan jenis tanaman (Data diambil dari laporan kerusakan sebelumnya/Blangko 07)
- Pada bagian "Rencana Tanam", sistem menyediakan kolom input (editable) untuk mengisi Rencana YAD (Yang Akan Datang)
- Sistem menampilkan data "Rencana Tanam Tahun Ini" sebagai referensi perbandingan (Read-Only)
e. Tabel Produksi Tanaman
fungsional requirement:
- Sistem otomatis mengambil data Puncak Luas Tanam (Ha) dari tabel statistik sebelumnya sebagai basis perhitungan.
- Sistem menyediakan kolom input (editable) untuk mengisi Data Ubinan / Rata-rata Produksi (Ton/Ha) untuk setiap jenis tanaman
- Sistem harus menghitung otomatis Produksi per Tanaman (Ton) dengan rumus: (Puncak Luas Tanam x Data Ubinan).
- Sistem menjumlahkan seluruh produksi tanaman menjadi Total Jumlah Produksi (Ton) di baris paling bawah
f. Laporan
fungsional requirement:
- Sistem harus mendukung fitur cetak pdf
- Sistem harus menyediakan form isian tanggal dan informasi terkati pengamat/ranting
 
13. modul Soil Analyzer(untuk pengembangan selanjutnya)
fungsional requirement:
- sistem bisa otomatis mendeteksi genangan/kebanjiran atau kekering(merujuk pada blangko 04-o)
 
14. modul peta visualisai petak tersier dan pintu air
fungsional requirement:
- sistem menampilkan peta yang akan memvisualisasikan petak tersier dan pintu air, menggunakan data gis yang ada