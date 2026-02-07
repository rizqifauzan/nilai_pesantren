# Data Dictionary

Definisi dan arti setiap field dalam sistem nilai pesantren.

---

## 🧱 MASTER DATA

### users

User admin untuk sistem authentication.

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik user admin |
| username | varchar unique | Username untuk login |
| password | varchar | Password terenkripsi (bcrypt) |
| role | enum | Role user: `admin` = admin sistem |
| status | enum | Status akun: `active` = aktif, `inactive` = tidak aktif |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### students

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik siswa |
| nis | varchar unique | Nomor Induk Siswa - wajib unik |
| nisn | varchar nullable | Nomor Induk Siswa Nasional - opsional |
| full_name | varchar | Nama lengkap siswa |
| gender | enum nullable | Jenis kelamin: `L` = Laki-laki, `P` = Perempuan |
| birth_date | date nullable | Tanggal lahir siswa |
| status | enum | Status siswa: `active` = aktif bersekolah, `graduated` = sudah lulus, `moved` = pindah/keluar |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### teachers

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik guru |
| name | varchar | Nama lengkap guru |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### classes

Template kelas (contoh: 1A, 2A, 3A).

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik template kelas |
| name | varchar | Nama kelas: `1A`, `1B`, `2A`, dll |
| grade_level | int | Tingkat kelas: `1` = kelas 1, `2` = kelas 2, `3` = kelas 3 |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### academic_years

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik tahun ajaran |
| label | varchar | Label tahun ajaran: `2024/2025`, `2025/2026` |
| start_date | date | Tanggal mulai tahun ajaran |
| end_date | date | Tanggal berakhir tahun ajaran |
| is_active | boolean | Apakah tahun ajaran ini sedang aktif: `TRUE` = aktif, `FALSE` = tidak aktif |

---

### subjects

Master nama pelajaran.

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik mata pelajaran |
| name | varchar | Nama mata pelajaran |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### personality_traits

Master aspek kepribadian (nilai akhlaq).

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik aspek kepribadian |
| name | varchar | Nama aspek: `Disiplin`, `Tanggung Jawab`, `Berani`, dll |
| is_active | boolean | Apakah aspek ini aktif: `TRUE` = aktif, `FALSE` = tidak aktif |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### attendance_types

Master jenis kehadiran (absensi).

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik jenis kehadiran |
| name | varchar | Nama jenis: `Izin`, `Alfa`, `Sakit`, dll |
| is_active | boolean | Apakah jenis ini aktif: `TRUE` = aktif, `FALSE` = tidak aktif |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

## 🔄 DATA OPERASIONAL

### class_academic_years

Kelas nyata yang berjalan di tahun tertentu (contoh: "Kelas 1A tahun 2024/2025").

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik kelas berjalan |
| class_id | FK → classes.id | Referensi template kelas |
| academic_year_id | FK → academic_years.id | Referensi tahun ajaran |
| homeroom_teacher_id | FK → teachers.id | Wali kelas yang menangani |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### student_enrollments

Siswa terdaftar di kelas mana pada tahun tersebut.

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik pendaftaran |
| student_id | FK → students.id | Referensi siswa |
| class_academic_year_id | FK → class_academic_years.id | Referensi kelas berjalan |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### class_subjects

Daftar mata pelajaran resmi untuk kelas tersebut.

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik mapel kelas |
| class_academic_year_id | FK → class_academic_years.id | Referensi kelas berjalan |
| subject_id | FK → subjects.id | Referensi mata pelajaran |
| order_number | int | Urutan tampil di raport |
| kkm | integer default 60 | Kriteria Ketuntasan Minimal - default 60 |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

## 📘 DATA RAPOR

### report_cards

Induk nilai raport per semester.

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik raport |
| student_enrollment_id | FK → student_enrollments.id | Referensi pendaftaran siswa |
| semester | int | Semester: `1` = semester 1 (ganjil), `2` = semester 2 (genap) |
| is_finalized | boolean default FALSE | Status finalisasi raport: `TRUE` = sudah final, `FALSE` = masih draft |
| finalized_at | timestamp nullable | Waktu finalisasi (NULL jika belum final) |
| finalized_by | FK → teachers.id nullable | Guru yang melakukan finalisasi (NULL jika belum final) |
| is_promoted | boolean nullable | Keputusan naik kelas: `TRUE` = naik kelas, `FALSE` = tinggal kelas, `NULL` = belum/dipilih tidak ditentukan |
| promotion_note | varchar nullable | Catatan keputusan kenaikan kelas |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### grades

Nilai per mata pelajaran.

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik nilai |
| report_card_id | FK → report_cards.id | Referensi raport |
| class_subject_id | FK → class_subjects.id | Referensi mapel kelas |
| score | integer nullable | Nilai angka (0-100), boleh NULL saat draft |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

---

### personality_grades

Nilai kepribadian per aspek.

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik nilai kepribadian |
| report_card_id | FK → report_cards.id | Referensi raport |
| personality_trait_id | FK → personality_traits.id | Referensi aspek kepribadian (hanya yang `is_active = TRUE`) |
| score | enum nullable | Nilai huruf: `A`, `B`, `C`, `D`, `E` - boleh NULL |
| description | varchar nullable | Deskripsi qualitative |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

**Nilai score (A-E):**
| Nilai | Arti |
|-------|------|
| A | Sangat Baik |
| B | Baik |
| C | Cukup |
| D | Kurang |
| E | Sangat Kurang |
| NULL | Belum dinilai |

**Aturan:**
- Hanya aspek dengan `is_active = TRUE` yang boleh ditambahkan ke raport
- Nilai `score` boleh NULL (siswa belum dinilai untuk aspek tersebut)
- Setelah raport `is_finalized = TRUE`: tidak bisa menambah/menghapus aspek kepribadian

---

### attendance_records

Nilai kehadiran per jenis (jumlah hari).

| Field | Tipe | Definisi |
|-------|------|----------|
| id | bigint PK | Identifikasi unik kehadiran |
| report_card_id | FK → report_cards.id | Referensi raport |
| attendance_type_id | FK → attendance_types.id | Referensi jenis kehadiran (hanya yang `is_active = TRUE`) |
| value | integer | Jumlah hari (misal: 2 hari izin) |
| created_at | timestamp | Waktu pembuatan record |
| updated_at | timestamp | Waktu terakhir perubahan |

**Aturan:**
- Hanya jenis dengan `is_active = TRUE` yang boleh ditambahkan ke raport
- Setelah raport `is_finalized = TRUE`: tidak bisa menambah/menghapus record kehadiran

---

## 📋 RINGKASAN KEPUTUSAN

### is_promoted (Keputusan Kenaikan Kelas)

| Nilai | Arti |
|-------|------|
| TRUE | Naik kelas |
| FALSE | Tinggal kelas |
| NULL | Belum/dipilih tidak ditentukan |

---

### is_finalized (Status Raport)

| Nilai | Arti |
|-------|------|
| TRUE | Raport sudah final dan tidak bisa diubah |
| FALSE | Raport masih draft dan bisa diubah |

---

### status (Status Siswa)

| Nilai | Arti |
|-------|------|
| active | Siswa masih aktif bersekolah |
| graduated | Siswa sudah lulus |
| moved | Siswa sudah pindah atau keluar |

---

### gender (Jenis Kelamin)

| Nilai | Arti |
|-------|------|
| L | Laki-laki |
| P | Perempuan |
| NULL | Belum diisi |

---

### semester

| Nilai | Arti |
|-------|------|
| 1 | Semester 1 (Ganjil) |
| 2 | Semester 2 (Genap) |

---

### kkm (Kriteria Ketuntasan Minimal)

| Nilai | Arti |
|-------|------|
| >= 60 | Tuntas - siswa dianggap memahami materi |
| < 60 | Belum Tuntas - siswa perlu remidi |

Default adalah 60, bisa berbeda per mata pelajaran.

---

### is_active (di personality_traits)

| Nilai | Arti |
|-------|------|
| TRUE | Aspek kepribadian aktif dan tampil di raport |
| FALSE | Aspek tidak aktif, tidak tampil di raport baru |

---

### is_active (di attendance_types)

| Nilai | Arti |
|-------|------|
| TRUE | Jenis kehadiran aktif dan tampil di raport |
| FALSE | Jenis kehadiran tidak aktif, tidak tampil di raport baru |
