🧱 MASTER DATA
students
field	type
id	bigint PK
nis	varchar unique
nisn	varchar nullable
full_name	varchar
gender	enum nullable
birth_date	date nullable
status	enum (active, graduated, moved)
created_at	timestamp
updated_at	timestamp
teachers
field	type
id	bigint PK
name	varchar
created_at	timestamp
updated_at	timestamp
classes

Template kelas.

field	type
id	bigint PK
name	varchar
grade_level	int
created_at	timestamp
updated_at	timestamp
academic_years
field	type
id	bigint PK
label	varchar
start_date	date
end_date	date
is_active	boolean
subjects

Master nama mapel.

field	type
id	bigint PK
name	varchar
created_at	timestamp
updated_at	timestamp
🔄 DATA OPERASIONAL
class_academic_years

Kelas yang berjalan di tahun tertentu.

field	type
id	bigint PK
class_id	FK → classes.id
academic_year_id	FK → academic_years.id
homeroom_teacher_id	FK → teachers.id
created_at	timestamp
updated_at	timestamp
student_enrollments

Siswa terdaftar di kelas mana.

field	type
id	bigint PK
student_id	FK → students.id
class_academic_year_id	FK → class_academic_years.id
created_at	timestamp
updated_at	timestamp
class_subjects

Daftar mapel khusus kelas itu.

field	type
id	bigint PK
class_academic_year_id	FK → class_academic_years.id
subject_id	FK → subjects.id
order_number	int
kkm	integer default 60
created_at	timestamp
updated_at	timestamp
unique
(class_academic_year_id, subject_id)

📘 DATA RAPOR
report_cards
field	type	note
id	bigint PK	
student_enrollment_id	FK	
semester	int	
is_finalized	boolean default false	
finalized_at	timestamp nullable	
finalized_by	FK → teachers.id nullable	
is_promoted	boolean nullable	
promotion_note	varchar nullable	
created_at	timestamp	
updated_at	timestamp	
grades
field	type
id	bigint PK
report_card_id	FK → report_cards.id
class_subject_id	FK → class_subjects.id
score	integer nullable
created_at	timestamp
updated_at	timestamp
unique
(report_card_id, class_subject_id)

📊 DATA NILAI KEPRIBADIAN
personality_traits

Master aspek kepribadian (nilai akhlaq).

field	type
id	bigint PK
name	varchar
is_active	boolean default true
created_at	timestamp
updated_at	timestamp

personality_grades

Nilai kepribadian per aspek.

field	type
id	bigint PK
report_card_id	FK → report_cards.id
personality_trait_id	FK → personality_traits.id
score	enum (A, B, C, D, E) nullable
description	varchar nullable
created_at	timestamp
updated_at	timestamp
unique	(report_card_id, personality_trait_id)

📊 DATA KEHADIRAN
attendance_types

Master jenis kehadiran (absensi).

field	type
id	bigint PK
name	varchar
is_active	boolean default true
created_at	timestamp
updated_at	timestamp

attendance_records

Nilai kehadiran per jenis.

field	type
id	bigint PK
report_card_id	FK → report_cards.id
attendance_type_id	FK → attendance_types.id
value	integer
created_at	timestamp
updated_at	timestamp

🔒 DATA AUTENTIKASI
users

User admin untuk sistem.

| field | type |
|------|------|
| id | BIGINT PK |
| username | VARCHAR(50) UNIQUE |
| password | VARCHAR(255) |
| role | ENUM('admin') DEFAULT 'admin' |
| status | ENUM('active', 'inactive') DEFAULT 'active' |
| created_at | TIMESTAMP |
| updated_at | TIMESTAMP |

---

🔒 VALIDATION RULES WAJIB (BACKEND)

Saat finalize:

Semua class_subjects harus punya baris nilai

Jika kosong → set 0

is_promoted wajib tidak null

promotion_note wajib terisi

Jika tidak → gagal final