Berikut struktur menyeluruh setelah semua aturan digabung:

siswa bisa berpindah kelas antar tahun

kelas hidup di dalam tahun ajaran

daftar pelajaran berbeda tiap kelas

nilai melekat ke raport

raport punya status draft/final

keputusan kenaikan wajib sebelum final

ERD digambarkan dari master → operasional → hasil akhir supaya mudah ditelusuri.

🧱 ERD Lengkap (High Level View)
students
   ↓
student_enrollments
   ↓
report_cards
   ↓
grades
   ↑
class_subjects
   ↑
class_academic_years
   ↑
classes
   ↑
academic_years

teachers → (wali kelas & finalisasi)
subjects → (master nama mapel)
personality_traits → (master aspek kepribadian)
attendance_types → (master jenis kehadiran)


Berikut penjelasan tabel satu per satu beserta relasi dan cardinality.

🎓 1. students

PK: id

Relasi:

1 siswa → banyak student_enrollments

1 siswa → banyak report_cards (via enrollment)

🏫 2. classes

Template kelas (1A, 1B, 2A, dll).

PK: id

Relasi:

1 class → banyak class_academic_years

📅 3. academic_years

PK: id

Relasi:

1 tahun → banyak class_academic_years

👩‍🏫 4. teachers

Dipakai untuk:

wali kelas

siapa yang finalisasi

🏷️ 5. subjects

Master nama pelajaran.

🔥 6. class_academic_years

(Kelas nyata yang berjalan)

PK: id
FK: class_id → classes
FK: academic_year_id → academic_years
FK: homeroom_teacher_id → teachers

Relasi:

1 → banyak student_enrollments

1 → banyak class_subjects

🔥 7. student_enrollments

Siswa berada di kelas mana pada tahun tersebut.

PK: id
FK: student_id → students
FK: class_academic_year_id → class_academic_years

Relasi:

1 → punya report_cards per semester

🔥 8. class_subjects

Daft mapel resmi kelas itu.

PK: id
FK: class_academic_year_id
FK: subject_id

extra:

order_number

kkm (default 60)

Relasi:

1 → muncul di banyak grades

🔥 9. report_cards

Induk nilai.

PK: id
FK: student_enrollment_id

Field penting:

semester

is_finalized

finalized_at

finalized_by → teachers

keputusan naik

is_promoted (nullable sebelum final)

promotion_note (nullable sebelum final)

Relasi:

1 → banyak grades

1 → banyak personality_grades

1 → banyak attendance_records

🔥 10. grades

Nilai per mapel.

PK: id
FK: report_card_id
FK: class_subject_id

Field:

score (integer nullable)

unique:

(report_card_id, class_subject_id)

💎 11. personality_traits

Master aspek kepribadian (nilai akhlaq).

PK: id

Field:

name (Disiplin, Tanggung Jawab, dll)

is_active (boolean)

💎 12. personality_grades

Nilai kepribadian per aspek.

PK: id
FK: report_card_id → report_cards
FK: personality_trait_id → personality_traits

Field:

score (enum A, B, C, D, E nullable)

description (varchar nullable)

unique:

(report_card_id, personality_trait_id)

📋 13. attendance_types

Master jenis kehadiran (absensi).

PK: id

Field:

name (Izin, Alfa, Sakit, dll)

is_active (boolean)

📋 14. attendance_records

Nilai kehadiran per jenis.

PK: id
FK: report_card_id → report_cards
FK: attendance_type_id → attendance_types

Field:

value (integer - jumlah hari)

Relasi:

1 → banyak report_cards

🧠 ERD Relasi Detail (Cardinality)
students (1) ────< (N) student_enrollments

class_academic_years (1) ────< (N) student_enrollments
class_academic_years (1) ────< (N) class_subjects

student_enrollments (1) ────< (N) report_cards

report_cards (1) ────< (N) grades
report_cards (1) ────< (N) personality_grades
report_cards (1) ────< (N) attendance_records

class_subjects (1) ────< (N) grades

subjects (1) ────< (N) class_subjects

teachers (1) ────< (N) class_academic_years
teachers (1) ────< (N) report_cards

personality_traits (1) ────< (N) personality_grades

attendance_types (1) ────< (N) attendance_records
