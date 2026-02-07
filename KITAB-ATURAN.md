# KITAB ATURAN SISTEM RAPORT AKADEMIK
## Business Rule Book - Dokumen Resmi Penetapan Aturan Bisnis

---

**Nomor:** 001/KITAB-ATURAN/2026
**Tanggal Ditetapkan:** 7 Februari 2026
**Status:** WAJIB DITAATI

---

## PENDAHULUAN

### Pasal 1 - Kedudukan dan Tujuan

(1) Kitab Aturan ini selanjutnya disebut "Dokumen Ini" merupakan dokumen resmi yang menetapkan seluruh aturan bisnis sistem raport akademik.

(2) Dokumen Ini disusun dengan gaya penulisan peraturan perundang-undangan untuk memastikan tidak ada multitafsir dalam implementasi sistem.

(3) Setiap baris dalam Dokumen Ini bersifat MANDATORY dan WAJIB dilaksanakan oleh seluruh pihak yang terlibat dalam pengembangan, pengujian, dan pengoperasian sistem.

(4) Jika terdapat pertentangan antara Dokumen Ini dengan dokumen lain yang bukan merupakan amandemen terhadap Dokumen Ini, maka ketentuan dalam Dokumen Ini yang berlaku.

### Pasal 2 - Ruang Lingkup

(1) Dokumen Ini mengatur hal-hal sebagai berikut:
- a. Aturan master data;
- b. Aturan data operasional;
- c. Aturan pencatatan nilai;
- d. Aturan perhitungan;
- e. Aturan status kenaikan kelas;
- f. Aturan keputusan finalisasi;
- g. Aturan pencetakan raport;
- h. Larangan dan sanksi.

(2) Dokumen Ini TIDAK mengatur hal-hal sebagai berikut:
- a. Multi peran pengguna (multi role user);
- b. Remedial atau ujian perbaikan;
- c. Komponen nilai (praktik, teori, atau lisan);
- d. Persetujuan bertingkat (multi-level approval);
- e. Analitik lanjutan;
- f. Perpindahan otomatis siswa ke kelas baru.

---

## BAB I - ATURAN UMUM

### Pasal 3 - Definisi

Dalam Dokumen Ini, istilah-istilah berikut memiliki arti:

(1) **Admin** adalah satu-satunya pengguna sistem yang memiliki akses penuh untuk mengelola seluruh data dan fungsi sistem.

(2) **Siswa** adalah individu yang terdaftar dalam sistem untuk menerima layanan pendidikan dan pencatatan nilai.

(3) **Kelas** adalah unit pembelajaran yang terdiri dari sekelompok siswa dalam satu tingkat dan tahun ajaran tertentu.

(4) **Mapel** adalah singkatan dari mata pelajaran, yaitu bidang kajian yang diajarkan di kelas.

(5) **Nilai** adalah angka bulat antara 0 (nol) hingga 100 (seratus) yang diberikan untuk menilai pencapaian siswa dalam satu mapel.

(6) **KKM** adalah kriteria ketuntasan minimum, yaitu nilai ambang batas yang menentukan apakah siswa dianggap lulus dalam suatu mapel.

(7) **Raport** adalah dokumen resmi yang memuat seluruh nilai siswa dalam satu semester.

(8) **Finalisasi** adalah tindakan mengunci data raport secara permanen sehingga tidak dapat diubah lagi.

(9) **Draft** adalah status raport yang belum difinalisasi dan masih dapat diubah.

(10) **Ranking** adalah urutan siswa berdasarkan pencapaian akademik tertinggi.

(11) **Enrollment** adalah pencatatan keanggotaan siswa dalam kelas pada tahun ajaran tertentu.

(12) **Semester** adalah pembagian waktu akademik dalam satu tahun ajaran:
- a. Semester 1 (Ganjil): Periode pertama;
- b. Semester 2 (Genap): Periode kedua.

(13) **Jenis Kelamin** adalah penanda gender siswa:
- a. L = Laki-laki;
- b. P = Perempuan.

### Pasal 4 - Prinsip Dasar

(1) **Prinsip Tunggal:** Satu mapel menghasilkan SATU nilai untuk setiap siswa dalam setiap raport.

(2) **Prinsip Integritas:** Setelah finalisasi, data menjadi read-only permanen dan TIDAK boleh diubah dengan cara apapun.

(3) **Prinsip Kelengkapan:** Keputusan kenaikan kelas WAJIB ada sebelum proses finalisasi dapat diselesaikan.

(4) **Prinsip Konsistensi:** Data historis TIDAK boleh berubah akibat perubahan atau pembaruan sistem di masa depan.

---

## BAB II - ATURAN MASTER DATA

### Pasal 5 - Aturan Data Siswa

(1) Setiap siswa yang dimasukkan ke sistem WAJIB memiliki:
- a. Nomor Induk Siswa (NIS) yang bersifat unik dan TIDAK boleh sama dengan siswa lain;
- b. Nama lengkap;
- c. Status keanggotaan.

(2) Data siswa berikut adalah opsional dan dapat diisi kapan saja:
- a. Nomor Induk Siswa Nasional (NISN);
- b. Jenis kelamin;
- c. Tanggal lahir.

(3) Perubahan nama siswa HANYA dapat dilakukan oleh Admin.

(4) Status siswa dapat berupa:
- a. Aktif, untuk siswa yang masih terdaftar;
- b. Lulus, untuk siswa yang telah menyelesaikan pendidikan;
- c. Pindah, untuk siswa yang meninggalkan institusi.

(5) SATU siswa BOLEH memiliki banyak enrollment pada waktu yang berbeda.

### Pasal 6 - Aturan Data Guru

(1) Setiap guru yang dimasukkan ke sistem WAJIB memiliki nama.

(2) Satu guru DAPAT menjadi wali kelas untuk beberapa kelas pada tahun ajaran yang sama.

(3) Satu guru DAPAT menjadi wali kelas dan juga sebagai pelaksana finalisasi raport.

### Pasal 7 - Aturan Data Kelas

(1) Kelas adalah template yang memiliki:
- a. Nama kelas;
- b. Tingkat kelas (grade level), berupa angka 1 (satu) sampai dengan 6 (enam).

(2) Nama kelas TIDAK boleh kosong.

(3) Tingkat kelas WAJIB berupa angka bulat positif.

### Pasal 8 - Aturan Data Tahun Ajaran

(1) Setiap tahun ajaran WAJIB memiliki:
- a. Label tahun ajaran (contoh: "2025/2026");
- b. Tanggal mulai;
- c. Tanggal selesai;
- d. Status aktif atau tidak aktif.

(2) HANYA SATU tahun ajaran yang BOLEH berstatus aktif pada satu waktu.

(3) Label tahun ajaran TIDAK boleh kosong.

(4) Tanggal mulai WAJIB lebih awal dari tanggal selesai.

### Pasal 9 - Aturan Data Mapel

(1) Setiap mapel WAJIB memiliki nama.

(2) Nama mapel TIDAK boleh kosong.

(3) SATU mapel DAPAT diajarkan di banyak kelas.

---

## BAB III - ATURAN DATA OPERASIONAL

### Pasal 10 - Aturan Kelas Tahun Ajaran (Class Academic Year)

(1) Kelas tahun ajaran adalah kelas nyata yang berjalan pada tahun ajaran tertentu.

(2) Pembentukan kelas tahun ajaran WAJIB mengacu pada:
- a. Template kelas yang sudah ada;
- b. Tahun ajaran yang aktif;
- c. Wali kelas yang ditunjuk.

(3) Satu template kelas DAPAT memiliki banyak kelas tahun ajaran pada tahun ajaran berbeda.

(4) Wali kelas WAJIB diisi dengan data guru yang sudah terdaftar dalam sistem.

### Pasal 11 - Aturan Enrollment Siswa

(1) Enrollment adalah pencatatan bahwa siswa terdaftar dalam kelas tahun ajaran tertentu.

(2) Pembuatan enrollment WAJIB mengacu pada:
- a. Data siswa yang sudah terdaftar;
- b. Kelas tahun ajaran yang sudah dibuat.

(3) SATU siswa DAPAT memiliki banyak enrollment pada waktu yang berbeda (misalnya: kelas 1 tahun 2024, kelas 2 tahun 2025).

(4) Jika siswa pindah kelas, enrollment baru WAJIB dibuat dan enrollment lama TIDAK dihapus.

(5) Penghapusan enrollment TIDAK diperkenankan jika sudah memiliki raport.

### Pasal 12 - Aturan Mapel dalam Kelas

(1) Mapel dalam kelas adalah pencatatan mapel yang diajarkan di kelas tahun ajaran tertentu.

(2) Penentuan mapel dalam kelas WAJIB memiliki:
- a. Mapel dari master data;
- b. KKM (kriteria ketuntasan minimum);
- c. Nomor urut tampil di raport.

(3) Nilai default KKM adalah 60 (enam puluh).

(4) KKM DAPAT diubah oleh Admin sebelum finalisasi raport.

(5) Nomor urut tampil di raport WAJIB berupa angka bulat dan menentukan urutan penampilan mapel di raport.

(6) SATU mapel HANYA DAPAT terdaftar sekali dalam satu kelas tahun ajaran.

---

## BAB IV - ATURAN PENCATATAN NILAI

### Pasal 13 - Aturan Umum Nilai

(1) Nilai adalah angka bulat yang menyatakan pencapaian siswa dalam satu mapel.

(2) Nilai WAJIB berada dalam rentang 0 (nol) hingga 100 (seratus).

(3) SATU raport HANYA boleh memiliki SATU nilai untuk SATU mapel.

(4) Nilai DAPAT kosong (NULL) selama status raport masih draft.

(5) Nilai TIDAK boleh berupa desimal.

(6) Nilai TIDAK boleh negatif.

### Pasal 14 - Input dan Perubahan Nilai

(1) Admin DAPAT melakukan hal berikut selama status raport masih draft:
- a. Memasukkan nilai baru untuk mapel yang belum memiliki nilai;
- b. Mengubah nilai yang sudah ada;
- c. Mengosongkan (menghapus) nilai.

(2) Admin TIDAK DAPAT melakukan hal-hal sebagaimana dimaksud pada ayat (1) setelah status raport menjadi final.

(3) Setiap perubahan nilai WAJIB dicatat timestamp pembaruan (updated_at).

(4) Nilai 0 (nol) berbeda dengan nilai kosong (NULL).

### Pasal 15 - Validasi Nilai

(1) Sistem WAJIB melakukan validasi terhadap setiap input atau perubahan nilai.

(2) Validasi meliputi:
- a. Nilai WAJIB berupa angka bulat;
- b. Nilai minimum adalah 0 (nol);
- c. Nilai maksimum adalah 100 (seratus);
- d. Nilai TIDAK boleh mengandung karakter selain angka.

(3) Sistem WAJIB menolak input nilai yang tidak memenuhi validasi sebagaimana dimaksud pada ayat (2).

### Pasal 15A - Aturan Semester dan Jenis Kelamin

(1) Semester dalam sistem WAJIB bernilai:
- a. 1 (satu) untuk Semester 1 (Ganjil);
- b. 2 (dua) untuk Semester 2 (Genap).

(2) Sistem WAJIB menolak input semester di luar rentang 1-2.

(3) Jenis Kelamin dalam sistem WAJIB bernilai:
- a. L untuk Laki-laki;
- b. P untuk Perempuan.

(4) Jenis Kelamin BOLEH dikosongkan (NULL) jika belum diketahui.

---

## BAB V - ATURAN PERHITUNGAN

### Pasal 16 - Perhitungan Rata-rata

(1) Rata-rata adalah nilai tengah yang dihitung dari seluruh nilai siswa dalam satu raport.

(2) Perhitungan rata-rata menggunakan rumus berikut:
```
Rata-rata = (Jumlah Seluruh Nilai) ÷ (Jumlah Mapel)
```

(3) Jika terdapat nilai kosong (NULL), nilai tersebut TIDAK termasuk dalam perhitungan jumlah mapel.

(4) Nilai kosong (NULL) akan otomatis diubah menjadi 0 (nol) pada saat finalisasi.

(5) Hasil perhitungan rata-rata DAPAT berupa desimal dan dibulatkan hingga 2 (dua) angka di belakang koma.

### Pasal 17 - Perhitungan Ranking

(1) Ranking adalah urutan siswa berdasarkan pencapaian akademik tertinggi.

(2) Ranking WAJIB dihitung per kelas.

(3) Ranking per kelas WAJIB didasarkan pada rata-rata seluruh nilai dalam raport.

(4) Urutan ranking adalah sebagai berikut:
- a. Nilai rata-rata tertinggi menduduki ranking 1 (satu);
- b. Nilai rata-rata terendah menduduki ranking terakhir;
- c. Jika rata-rata sama, ranking ditentukan berdasarkan urutan abjad nama (A-Z).

(5) Ranking HANYA menghitung siswa dengan status aktif.

(6) Ranking DAPAT berubah setiap kali ada perubahan nilai.

---

## BAB VI - ATURAN STATUS KELULUSAN MAPEL

### Pasal 18 - Penentuan Kelulusan per Mapel

(1) Kelulusan siswa dalam satu mapel ditentukan oleh perbandingan antara nilai dengan KKM mapel tersebut.

(2) Aturan kelulusan adalah sebagai berikut:
- a. Jika nilai sama dengan KKM atau lebih tinggi, siswa Dinyatakan LULUS;
- b. Jika nilai lebih rendah dari KKM, siswa Dinyatakan TIDAK LULUS.

(3) Status kelulusan DAPAT berbeda untuk setiap mapel dalam raport yang sama.

(4) Sistem WAJIB menampilkan status kelulusan per mapel di raport.

---

## BAB VII - ATURAN KEPUTUSAN KENAIKAN KELAS

### Pasal 19 - Keputusan Kenaikan Kelas

(1) Keputusan kenaikan kelas adalah pernyataan mengenai status perpindahan siswa ke kelas berikutnya.

(2) Keputusan kenaikan kelas WAJIB disimpan dalam record raport dengan field:
- a. is_promoted (boolean);
- b. promotion_note (catatan tekstual).

(3) is_promoted dapat bernilai:
- a. TRUE, jika siswa naik kelas;
- b. FALSE, jika siswa tinggal kelas.

(4) promotion_note WAJIB diisi dengan salah satu format berikut:
- a. "NAIK Ke Kelas [X]";
- b. "TINGGAL di Kelas [X]";
- c. "NAIK Bersyarat Ke Kelas [X]";
- d. Format lain yang jelas menyatakan keputusan.

(5) Admin DAPAT mengubah keputusan kenaikan kelas selama status raport masih draft.

(6) Admin TIDAK DAPAT mengubah keputusan kenaikan kelas setelah status raport menjadi final.

### Pasal 20 - Kewajiban Keputusan Kenaikan

(1) Selama status raport masih draft, keputusan kenaikan kelas BOLEH kosong (nullable).

(2) SEBELUM proses finalisasi, Admin WAJIB memastikan:
- a. is_promoted TIDAK boleh kosong untuk setiap siswa;
- b. promotion_note TIDAK boleh kosong untuk setiap siswa.

(3) Sistem WAJIB menolak proses finalisasi jika masih terdapat siswa dengan keputusan kenaikan kelas yang kosong.

---

## BAB VIII - ATURAN FINALISASI

### Pasal 21 - Pengertian Finalisasi

(1) Finalisasi adalah tindakan mengunci seluruh data raport secara permanen.

(2) Setelah finalisasi, status raport berubah dari draft menjadi final.

(3) Data yang telah difinalisasi TIDAK DAPAT diubah dengan cara apapun oleh pihak manapun.

(4) Finalisasi dilakukan per kelas per semester.

### Pasal 22 - Syarat Finalisasi

(1) Sebelum melakukan finalisasi, sistem WAJIB memeriksa syarat-syarat berikut:
- a. Semua keputusan kenaikan kelas WAJIB sudah terisi;
- b. Tidak ada siswa dengan keputusan kenaikan kosong;
- c. Nilai untuk setiap mapel WAJIB ada atau NULL.

(2) Jika terdapat nilai NULL pada saat finalisasi, sistem WAJIB mengubah NULL menjadi 0 (nol).

(3) Sistem WAJIB menolak finalisasi jika syarat sebagaimana dimaksud pada ayat (1) tidak terpenuhi.

### Pasal 23 - Proses Finalisasi

(1) Finalisasi dilakukan oleh Admin melalui fungsi "Mark as Final" untuk seluruh siswa di kelas tersebut.

(2) Pada saat finalisasi, sistem WAJIB melakukan hal-hal berikut:
- a. Memeriksa kelengkapan keputusan kenaikan kelas;
- b. Mengubah semua nilai NULL menjadi 0 (nol);
- c. Mengubah status is_finalized menjadi TRUE;
- d. Mencatat finalized_at dengan timestamp saat itu;
- e. Mencatat finalized_by dengan identitas Admin yang melakukan finalisasi.

(3) Setelah finalisasi, sistem WAJIB menolak setiap upaya perubahan:
- a. Nilai;
- b. Keputusan kenaikan kelas;
- c. Enrollment siswa.

(4) Finalisasi bersifat IRREVERSIBLE (tidak dapat dibatalkan).

---

## BAB IX - ATURAN PENCETAKAN RAPORT

### Pasal 24 - Kewajiban Pencetakan

(1) Raport DAPAT dicetak dalam dua kondisi:
- a. Status draft (belum final);
- b. Status final (sudah final).

(2) Pencetakan raport dapat dilakukan kapan saja sesuai kebutuhan Admin.

### Pasal 25 - Tampilan Raport Draft

(1) Raport yang dicetak dalam status draft WAJIB menampilkan watermark "DRAFT".

(2) Watermark HARUS terlihat jelas dan tidak dapat dihapus.

(3) Raport draft TIDAK berlaku sebagai dokumen resmi.

### Pasal 26 - Tampilan Raport Final

(1) Raport yang dicetak dalam status final TIDAK menampilkan watermark "DRAFT".

(2) Raport final WAJIB menampilkan informasi:
- a. Identitas siswa;
- b. Identitas kelas dan tahun ajaran;
- c. Semester;
- d. Seluruh nilai per mapel;
- e. Rata-rata nilai;
- f. Ranking;
- g. Status kelulusan per mapel;
- h. Keputusan kenaikan kelas;
- i. Tanggal dan penanggung jawab finalisasi.

(3) Raport final berlaku sebagai dokumen resmi yang tidak dapat diubah.

---

## BAB X - ATURAN NILAI KEPRIBADIAN DAN KEHADIRAN

### Pasal 26A - Aturan Nilai Kepribadian

(1) Nilai kepribadian adalah penilaian terhadap aspek akhlaq siswa.

(2) Nilai kepribadian WAJIB menggunakan nilai huruf: A, B, C, D, atau E.

(3) Arti nilai huruf:
- a. A = Sangat Baik
- b. B = Baik
- c. C = Cukup
- d. D = Kurang
- e. E = Sangat Kurang

(4) Nilai kepribadian BOLEH kosong (NULL) selama status raport masih draft.

(5) Setelah finalisasi, nilai kepribadian TIDAK dapat diubah.

(6) SATU raport HANYA boleh memiliki SATU nilai untuk SATU aspek kepribadian.

(7) Aspek kepribadian yang ditampilkan di raport HANYA yang berstatus aktif (is_active = TRUE).

### Pasal 26B - Aturan Kehadiran

(1) Kehadiran adalah pencatatan jumlah hari absensi siswa.

(2) Jenis kehadiran meliputi: Izin, Alfa, Sakit, dan lainnya.

(3) Sistem WAJIB menampilkan rekap kehadiran per jenis di raport.

(4) Setelah finalisasi, data kehadiran TIDAK dapat diubah.

(5) SATU raport HANYA boleh memiliki SATU record untuk SATU jenis kehadiran.

---

## BAB XI - LARANGAN DAN SANKSI

### Pasal 27 - Larangan Umum

(1) DILARANG mengubah data raport setelah finalisasi.

(2) DILARANG menghapus enrollment siswa yang sudah memiliki raport.

(3) DILARANG menghapus mapel dari kelas jika sudah memiliki nilai.

(4) DILARANG mengubah KKM mapel setelah ada nilai yang diinput.

(5) DILARANG memiliki dua nilai untuk satu mapel dalam satu raport.

(6) DILARANG mengubah status aktif tahun ajaran jika ada kelas berjalan.

(7) DILARANG finalisasi raport yang memiliki keputusan kenaikan kosong.

### Pasal 28 - Sanksi

(1) Setiap pelanggaran terhadap larangan sebagaimana dimaksud dalam Pasal 27 WAJIB ditolak oleh sistem.

(2) Tidak ada mekanisme bypass untuk pelanggaran larangan.

(3) Administrator sistem TIDAK memiliki hak untuk mengakali larangan melalui manipulasi database langsung.

---

## BAB XI - KETENTUAN PENUTUP

### Pasal 29 - Kedudukan Dokumen

(1) Dokumen Ini merupakan bagian tidak terpisahkan dari pengembangan sistem raport akademik.

(2) Dokumen Ini menjadi rujukan utama dalam:
- a. Pengembangan fitur sistem;
- b. Pengujian sistem (testing);
- c. Pengoperasian sistem;
- d. Pemecahan masalah (troubleshooting).

### Pasal 32 - Prosedur Perubahan

(1) Perubahan terhadap Dokumen Ini HANYA dapat dilakukan melalui:
- a. Amandemen resmi;
- b. Persetujuan tertulis dari pembuat kebijakan.

(2) Setiap perubahan WAJIB didokumentasikan dengan mencantumkan:
- a. Nomor amandemen;
- b. Tanggal perubahan;
- c. Deskripsi perubahan;
- d. Alasan perubahan.

(3) Perubahan tidak berlaku surut untuk data yang sudah final.

### Pasal 31 - Pernyataan Akhir

(1) Dokumen Ini ditetapkan dan berlaku sejak tanggal yang tertulis di awal dokumen.

(2) Segala sesuatu yang tidak diatur dalam Dokumen Ini, diselesaikan dengan mengacu pada prinsip-prinsip yang ditetapkan dalam Dokumen Ini.

(3) Jika terdapat kekosongan regulasi, maka pengembang WAJIB berkonsultasi dengan pembuat kebijakan sebelum mengambil keputusan.

---

## LAMPIRAN

### Lampiran A - Matriks Validasi Nilai

| Input | Hasil |
|-------|-------|
| NULL | Diterima (saat draft) |
| 0 | Diterima |
| 1-59 | Diterima |
| 60-100 | Diterima |
| >100 | Ditolak |
| <0 | Ditolak |
| Desimal | Ditolak |
| Huruf/Karakter | Ditolak |

### Lampiran B - Matriks Kelulusan

| Kondisi | Hasil |
|---------|-------|
| Nilai = KKM | LULUS |
| Nilai > KKM | LULUS |
| Nilai < KKM | TIDAK LULUS |

### Lampiran C - Matriks Finalisasi

| Kondisi | Bisa Final? |
|---------|-------------|
| Semua keputusan naik terisi | YA |
| Ada keputusan naik kosong | TIDAK |
| Semua nilai terisi | YA |
| Ada nilai NULL | YA (NULL diubah jadi 0) |
| Admin belum login | TIDAK |

---

**Dokumen Ini disusun dengan gaya peraturan perundang-undangan untuk memastikan tidak multitafsir.**

**Setiap ketentuan bersifat MANDATORY dan WAJIB dilaksanakan.**

---

*Kitab Aturan Sistem Raport Akademik*
*Versi 1.0*
