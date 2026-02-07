# Product Requirements Document (PRD) - Sistem Raport Akademik

1.  Latar Belakang

Sekolah membutuhkan sistem pengolahan nilai yang:

mudah digunakan,

tidak menimbulkan konflik interpretasi

menghasilkan raport resmi yang tidak dapat diubah setelah disahkan.

Sistem ini difokuskan untuk kebutuhan operasional nyata, bukan sistem akademik kompleks berskala universitas.

2.  Tujuan Produk

Menyediakan alat bagi admin untuk:

Mengelola data siswa dan kelas.

Memasukkan nilai per mata pelajaran.

Melihat peringkat siswa dalam kelas.

Menentukan status kenaikan kelas.

Mengunci data secara resmi.

Mencetak raport.

3.  Definisi Keberhasilan

Produk dianggap berhasil jika admin dapat menjalankan alur berikut tanpa bantuan teknis tambahan:

Input → Review → Tentukan kenaikan → Finalisasi → Cetak.

4.  Ruang Lingkup (In Scope)

✔ Master data siswa✔ Master kelas✔ Enrollment siswa ke kelas✔ Mapel per kelas✔ Input nilai✔ Ranking per kelas✔ KKM✔ Status naik/tinggal✔ Nilai kepribadian✔ Kehadiran✔ Finalisasi per kelas✔ Cetak raport

5.  Di Luar Ruang Lingkup (Out of Scope)

❌ Multi role user❌ Remedial❌ Komponen nilai (praktik/teori/lisan)❌ Approval bertingkat❌ Analitik lanjutan❌ Otomatis memindahkan siswa ke kelas baru

6.  Tipe PenggunaAdmin

Satu-satunya pengguna sistem.Memiliki akses penuh.

7.  Gambaran Model Datastudents

Identitas siswa.

classes

Template kelas (1A, 2A, dll).

academic_years

Tahun ajaran aktif.

student_enrollments

Hubungan siswa dengan kelas (memiliki histori).

class_subjects

Mapel yang diajarkan di kelas + KKM + urutan raport.

report_cards

Induk nilai per semester, contains is_finalized untuk status draft/final.

grades

Nilai siswa per mapel.

8.  Aturan Bisnis Utama (MANDATORY)

Satu mapel menghasilkan satu nilai.

Nilai harus integer 0–100.

Ranking berdasarkan rata-rata semua mapel.

Nilai boleh kosong saat draft.

Saat final → kosong menjadi 0.

Setelah final → tidak boleh ada perubahan.

Keputusan kenaikan kelas wajib ada sebelum final.

Jika ada konflik pendapat di masa depan → aturan ini menang.

9.  Fitur Detail9.1 Master Data

Admin dapat:

membuat tahun ajaran

membuat kelas

membuat siswa

mendaftarkan siswa ke kelas

membuat mapel

menentukan mapel dalam kelas

menentukan KKM

menentukan urutan tampil di raport

Default KKM = 60.

9.2 Enrollment (student_enrollments)

Satu siswa bisa muncul di beberapa kelas pada waktu berbeda.

Jika pindah kelas:→ buat record baru.Record lama tetap ada.

9.3 Input Nilai

Admin melihat tabel:

Siswa aktif × mapel.

Admin dapat:✔ isi✔ ubah✔ kosongkan

Selama kelas belum final.

9.4 Validasi Nilai

hanya angka bulat

minimum 0

maksimum 100

9.5 PerhitunganRata-rata

Mean dari semua mapel.

Ranking

hanya siswa aktif

urut nilai terbesar

Jika sama → urut nama.

9.6 Status KKM

Per mapel:

= KKM → LULUS< KKM → TIDAK LULUS

9.7 Keputusan Kenaikan Kelas

Disimpan di report_cards (per raport, per siswa).

Field:

is_promoted (boolean)

promotion_note (string)

Contoh note:

NAIK Ke Kelas 3

TINGGAL di Kelas 2

NAIK Bersyarat Ke Kelas 3

Aturan:

Saat draft → boleh kosong.Saat final → tidak boleh ada yang kosong.

9.8 Finalisasi

Dilakukan per kelas per semester. Ketika admin mengklik "Mark as Final", SEMUA siswa di kelas tersebut akan difinalisasi.

Langkah:

Klik Mark as Final.

Sistem cek:

semua promotion terisi untuk seluruh siswa di kelas.

Jika lolos → nilai NULL jadi 0.

Status final aktif.

Setelah Final:

Tidak boleh:

ubah nilai

ubah enrollment

ubah keputusan kenaikan

Harus ditolak oleh backend.

9.9 Cetak Raport

Menampilkan:

nilai

rata-rata

ranking

status kenaikan

Jika belum final:→ ada watermark DRAFT.

10.  Kebutuhan Non-FungsionalKeamanan

Final = read only permanen.

Konsistensi

Data lama tidak boleh berubah karena update masa depan.

Kemudahan pakai

Admin awam harus bisa menjalankan tanpa pelatihan panjang.

11.  Risiko yang Diterima

Karena sistem sederhana:

tidak ada detail komponen nilai

tidak ada histori remedial

Ini disadari & diterima.

12.  Acceptance Criteria

Sistem siap produksi jika:

✔ nilai bisa diinput✔ ranking muncul✔ draft bisa dicetak✔ finalisasi sukses✔ setelah final tidak bisa edit✔ raport final valid

13.  Future Possibility (Bukan bagian versi ini)

multi user

approval pimpinan

detail nilai

auto kenaikan kelas

14.  Pernyataan Penutup

PRD ini adalah referensi resmi pengembangan.Semua keputusan teknis harus mengikuti dokumen ini.

Jika kebutuhan berubah → harus revisi PRD.