# Definition of Done (DoD)
## Standar Kelengkapan Fitur - Sistem Raport Akademik

---

**Nomor:** 001/DoD/2026
**Tanggal:** 7 Februari 2026
**Status:** WAJIB DITAATI

---

## PENDAHULUAN

### Pasal 1 - Tujuan Dokumen

(1) Definition of Done (DoD) ini menetapkan standar kapan suatu fitur dianggap **SELESAI** dan siap untuk dianggap telah memenuhi syarat pengembangan.

(2) Setiap fitur yang dikembangkan dalam Sistem Raport Akademik WAJIB memenuhi seluruh kriteria dalam Dokumen ini sebelum dapat dianggap "Done".

(3) Dokumen ini bersifat **COMPLETE CHECKLIST** - semua kriteria harus terpenuhi, tidak ada pengecualian.

(4) Dokumen ini merupakan bagian tidak terpisahkan dari [KITAB-ATURAN.md](KITAB-ATURAN.md) dan [PRD.md](PRD.md).

---

## BAB I - KRITERIA TEKNIS

### Pasal 2 - Kode Sumber

(1) **Kode WAJIB:**
   - [ ] Mengikuti konvensi penamaan yang konsisten
   - [ ] Tidak memiliki variabel yang tidak digunakan (unused variables)
   - [ ] Tidak memiliki fungsi yang tidak terpanggil (dead code)
   - [ ] Tidak memiliki komentar yang menyesatkan atau sudah tidak relevan
   - [ ] Format kode sesuai dengan style guide bahasa pemrograman yang digunakan

(2) **Struktur Kode WAJIB:**
   - [ ] Fungsi memiliki tanggung jawab tunggal (single responsibility)
   - [ ] Tidak ada duplikasi kode (DRY principle)
   - [ ] Kode mudah dibaca dan dipahami
   - [ ] Kompleksitas siklomatik reasonable (tidak lebih dari 10 per fungsi)

(3) **Git Commit WAJIB:**
   - [ ] Pesan commit deskriptif dan jelas
   - [ ] Satu commit fokus pada satu perubahan
   - [ ] Tidak ada commit dengan pesan seperti "fix", "update", "misc"

### Pasal 3 - Database dan Data Integrity

(1) **Migrasi Database WAJIB:**
   - [ ] Semua perubahan skema disertai migrasi yang dapat di-rollback
   - [ ] Tidak ada data loss saat migrasi
   - [ ] Migrasi sudah diuji di environment staging

(2) **Data Integrity WAJIB:**
   - [ ] Foreign key constraints terdefinisi dengan benar
   - [ ] Unique constraints terdefinisi sesuai KITAB-ATURAN.md
   - [ ] Tidak ada orphan records yang tidak seharusnya terjadi
   - [ ] Timestamp (created_at, updated_at) terisi otomatis

(3) **Validasi Data WAJIB:**
   - [ ] Nis unik per siswa
   - [ ] Satu siswa tidak bisa memiliki dua nilai untuk mapel yang sama dalam satu raport
   - [ ] Nilai dalam rentang 0-100 dan berupa integer
   - [ ] KKM default 60 sesuai Pasal 12 ayat (3) KITAB-ATURAN.md

---

## BAB II - PENGUJIAN

### Pasal 4 - Unit Testing

(1) **Coverage WAJIB:**
   - [ ] Minimum 80% line coverage untuk kode bisnis kritis
   - [ ] 100% coverage untuk fungsi validasi
   - [ ] 100% coverage untuk fungsi perhitungan (rata-rata, ranking)

(2) **Skenario Testing WAJIB:**
   - [ ] Happy path (alur normal)
   - [ ] Edge cases (nilai 0, nilai 100, NULL)
   - [ ] Error conditions (input tidak valid)
   - [ ] Boundary conditions (nilai di luar rentang)

(3) **Test Data WAJIB:**
   - [ ] Tests tidak tergantung pada data spesifik yang bisa berubah
   - [ ] Tests dapat dijalankan secara independent
   - [ ] Tests tidak memiliki side effects

### Pasal 5 - Integration Testing

(1) **API Testing WAJIB:**
   - [ ] Semua endpoint REST/GraphQL memiliki test
   - [ ] Response format sesuai dengan kontrak yang diharapkan
   - [ ] Error responses sesuai dengan standar error handling

(2) **Database Integration WAJIB:**
   - [ ] Transactions di-test dengan rollback scenario
   - [ ] Constraints teruji (unique, foreign key, check)
   - [ ] NULL handling teruji

### Pasal 6 - User Acceptance Testing (UAT)

(1) **Skenario UAT WAJIB:**
   - [ ] Admin dapat login dan mengakses dashboard
   - [ ] Admin dapat membuat tahun ajaran baru
   - [ ] Admin dapat mendaftarkan siswa ke kelas
   - [ ] Admin dapat input nilai per mapel
   - [ ] Admin dapat melihat ranking siswa
   - [ ] Admin dapat menentukan keputusan kenaikan kelas
   - [ ] Admin dapat finalisasi raport
   - [ ] Admin dapat cetak raport (draft dan final)
   - [ ] Setelah finalisasi, data tidak dapat diubah

(2) **Validasi UAT WAJIB:**
   - [ ] Perhitungan rata-rata sesuai Pasal 16 KITAB-ATURAN.md
   - [ ] Ranking sesuai Pasal 17 KITAB-ATURAN.md
   - [ ] Kelulusan sesuai Pasal 18 KITAB-ATURAN.md
   - [ ] Watermark DRAFT muncul pada raport draft
   - [ ] Tidak ada watermark pada raport final

---

## BAB III - DOKUMENTASI

### Pasal 7 - Dokumentasi Teknis

(1) **Kode WAJIB:**
   - [ ] Semua public functions memiliki docstrings
   - [ ] Complex logic memiliki inline comments
   - [ ] business rules yang diimplementasikan dijelaskan

(2) **API Documentation WAJIB:**
   - [ ] OpenAPI/Swagger spec lengkap untuk semua endpoint
   - [ ] Request/response examples
   - [ ] Error codes documentation
   - [ ] Authentication requirements

(3) **Database Documentation WAJIB:**
   - [ ] ERD terbaru sesuai dengan implementasi
   - [ ] Deskripsi setiap tabel dan kolom
   - [ ] Constraints dan relationships dijelaskan

### Pasal 8 - Dokumentasi Pengguna

(1) **User Manual WAJIB:**
   - [ ] Panduan langkah demi langkah untuk setiap fitur
   - [ ] Screenshots untuk setiap halaman
   - [ ] Contoh input dan output yang diharapkan
   - [ ] Penjelasan alur kerja (workflow)

(2) **Quick Start Guide WAJIB:**
   - [ ] Cara setup environment pengembangan
   - [ ] Cara menjalankan aplikasi
   - [ ] Cara menjalankan tests

---

## BAB IV - KEAMANAN

### Pasal 9 - Security Requirements

(1) **Authentication & Authorization WAJIB:**
   - [ ] Tidak ada hardcoded credentials
   - [ ] API keys dan secrets di environment variables
   - [ ] Password hashing dengan algoritma yang aman (bcrypt/argon2)
   - [ ] Session management yang aman

(2) **Input Validation WAJIB:**
   - [ ] Semua input divalidasi di backend
   - [ ] SQL injection prevention
   - [ ] XSS prevention
   - [ ] CSRF protection

(3) **Data Protection WAJIB:**
   - [ ] Finalized data tidak dapat dimodifikasi
   - [ ] Audit trail untuk perubahan data (selama draft)
   - [ ] Backup strategy terdefinisi

(4) **Finalisasi Security WAJIB:**
   - [ ] Tidak ada mekanisme bypass finalisasi
   - [ ] Tidak ada admin_override untuk data final
   - [ ] Database constraints mencegah perubahan data final

---

## BAB V - PERFORMA

### Pasal 10 - Performance Requirements

(1) **Response Time WAJIB:**
   - [ ] Page load < 2 detik
   - [ ] API response < 500ms untuk operasi normal
   - [ ] API response < 3 detik untuk operasi kompleks (ranking, finalisasi)

(2) **Database Performance WAJIB:**
   - [ ] Indexed columns yang tepat (NIS, foreign keys)
   - [ ] Query tidak N+1 problem
   - [ ] Large dataset test dilakukan

(3) **Scalability WAJIB:**
   - [ ] Kode tidak blocking untuk operasi yang lambat
   - [ ] Async processing untuk operasi berat jika diperlukan

---

## BAB VI - UI/UX

### Pasal 11 - User Interface

(1) **Visual Design WAJIB:**
   - [ ] Konsisten dengan design system
   - [ ] Typography konsisten
   - [ ] Spacing konsisten
   - [ ] Color scheme konsisten

(2) **Responsiveness WAJIB:**
   - [ ] Tampilan baik di desktop (minimal 1366px)
   - [ ] Tampilan baik di tablet (768px)
   - [ ] Tampilan baik di mobile (375px) - jika required

(3) **Accessibility WAJIB:**
   - [ ] Alt text untuk gambar
   - [ ] Keyboard navigation berfungsi
   - [ ] Contrast ratio mencukupi WCAG AA

### Pasal 12 - User Experience

(1) **Usability WAJIB:**
   - [ ] Navigasi jelas dan konsisten
   - [ ] Feedback untuk setiap aksi pengguna
   - [ ] Error messages yang jelas dan helpful
   - [ ] Loading states terlihat jelas

(2) **Workflow WAJIB:**
   - [ ] Alur kerja sesuai dengan KITAB-ATURAN.md
   - [ ] Input → Review → Tentukan Kenaikan → Finalisasi → Cetak
   - [ ] Tidak ada langkah yang membingungkan

(3) **Raport Display WAJIB:**
   - [ ] Format raport sesuai template
   - [ ] Ranking terlihat jelas
   - [ ] Status kelulusan per mapel terlihat
   - [ ] Keputusan kenaikan kelas terlihat
   - [ ] Watermark DRAFT untuk draft (Pasal 25 KITAB-ATURAN.md)

---

## BAB VII - DEPLOYMENT

### Pasal 13 - Deployment Checklist

(1) **Pre-Deployment WAJIB:**
   - [ ] Semua tests PASS (unit, integration, UAT)
   - [ ] Code review sudah done
   - [ ] Tidak ada outstanding bugs dengan severity high/critical
   - [ ] Security scan PASS
   - [ ] Performance test PASS

(2) **Deployment WAJIB:**
   - [ ] Database migrations successfully applied
   - [ ] Environment variables configured
   - [ ] Application version recorded
   - [ ] Rollback plan ready

(3) **Post-Deployment WAJIB:**
   - [ ] Smoke test PASS
   - [ ] Health check PASS
   - [ ] Monitoring aktif
   - [ ] Logging aktif

---

## BAB VIII - BUSINESS RULES COMPLIANCE

### Pasal 14 - Mandatory Business Rules

(1) **Value Integrity WAJIB:**
   - [ ] Satu mapel = satu nilai per siswa (Prinsip Tunggal, Pasal 4 ayat 1)
   - [ ] Nilai 0 berbeda dengan NULL (Pasal 14 ayat 4)
   - [ ] Nilai tidak boleh negatif atau desimal (Pasal 13 ayat 5-6)

(2) **Calculation Rules WAJIB:**
   - [ ] Rata-rata = jumlah nilai ÷ jumlah mapel (Pasal 16 ayat 2)
   - [ ] NULL tidak termasuk dalam perhitungan jumlah mapel (Pasal 16 ayat 3)
   - [ ] NULL menjadi 0 saat finalisasi (Pasal 16 ayat 4)
   - [ ] Ranking berdasarkan rata-rata tertinggi (Pasal 17 ayat 3)

(3) **Promotion Rules WAJIB:**
   - [ ] is_promoted tidak boleh NULL saat finalisasi (Pasal 20 ayat 2)
   - [ ] promotion_note tidak boleh NULL saat finalisasi (Pasal 20 ayat 2)
   - [ ] Sistem tolak finalisasi jika keputusan kenaikan kosong (Pasal 20 ayat 3)

(4) **Finalization Rules WAJIB:**
   - [ ] Setelah final, data tidak dapat diubah (Prinsip Integritas)
   - [ ] Finalisasi bersifat irreversible (Pasal 23 ayat 4)
   - [ ] Nilai NULL diubah menjadi 0 saat finalisasi (Pasal 22 ayat 2)

(5) **Prohibition Rules WAJIB:**
   - [ ] Dilarang ubah data setelah final (Pasal 28 ayat 1)
   - [ ] Dilarang hapus enrollment yang sudah punya raport (Pasal 28 ayat 2)
   - [ ] Dilarang finalisasi dengan keputusan kosong (Pasal 28 ayat 7)

---

## BAB IX - VALIDASI FINAL

### Pasal 15 - DoD Checklist Final

Sebelum mengklaim fitur DONE, WAJIB checklist berikut:

```
┌─────────────────────────────────────────────────────────────────┐
│                    DEFINITION OF DONE CHECKLIST                 │
├─────────────────────────────────────────────────────────────────┤
│ KODE & TEKNIS                                                   │
│ [ ] Kode sesuai style guide                                     │
│ [ ] Tidak ada dead code/unused variables                        │
│ [ ] Git commit message规范                                      │
│ [ ] Database migrations ready                                   │
│ [ ] Data integrity constraints ter implementasi                │
├─────────────────────────────────────────────────────────────────┤
│ PENGUJIAN                                                       │
│ [ ] Unit test coverage ≥ 80%                                    │
│ [ ] 100% coverage fungsi validasi & perhitungan                 │
│ [ ] Integration tests PASS                                       │
│ [ ] UAT scenarios PASS                                          │
├─────────────────────────────────────────────────────────────────┤
│ DOKUMENTASI                                                     │
│ [ ] Code comments & docstrings lengkap                          │
│ [ ] API documentation lengkap                                   │
│ [ ] Database documentation terbaru                              │
│ [ ] User manual lengkap                                        │
├─────────────────────────────────────────────────────────────────┤
│ KEAMANAN                                                        │
│ [ ] Tidak ada hardcoded credentials                             │
│ [ ] Input validation lengkap                                     │
│ [ ] Finalisasi security ter implementasi                        │
│ [ ] Security scan PASS                                           │
├─────────────────────────────────────────────────────────────────┤
│ PERFORMA                                                        │
│ [ ] Page load < 2 detik                                         │
│ [ ] API response < 500ms                                         │
│ [ ] Database queries optimized                                  │
├─────────────────────────────────────────────────────────────────┤
│ UI/UX                                                           │
│ [ ] Design konsisten                                            │
│ [ ] Responsif                                                  │
│ [ ] Aksesibilitas                                              │
│ [ ] Workflow jelas                                              │
├─────────────────────────────────────────────────────────────────┤
│ DEPLOYMENT                                                      │
│ [ ] Tests PASS                                                   │
│ [ ] Code review done                                            │
│ [ ] Bugs high/critical resolved                                 │
│ [ ] Smoke test PASS                                             │
├─────────────────────────────────────────────────────────────────┤
│ BUSINESS RULES                                                  │
│ [ ] Prinsip Tunggal: 1 mapel = 1 nilai                          │
│ [ ] Prinsip Integritas: final = read-only                      │
│ [ ] Prinsip Kelengkapan: keputusan naik wajib ada               │
│ [ ] Perhitungan rata-rata sesuai rumus                         │
│ [ ] Ranking berdasarkan rata-rata                              │
│ [ ] NULL → 0 saat finalisasi                                    │
│ [ ] Finalisasi irreversible                                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## BAB X - KETENTUAN PENUTUP

### Pasal 16 - Penegakan DoD

(1) **Wajib Dipenuhi:** Seluruh kriteria dalam Dokumen ini WAJIB dipenuhi. Tidak ada toleransi untuk kriteria yang ditandai sebagai WAJIB.

(2) **Fleksibilitas:** Kriteria yang ditandai sebagai "minimum" atauopsional dapat disesuaikan dengan persetujuan Product Owner, namun TIDAK boleh turun di bawah standar minimum yang ditetapkan.

(3) **Pengecualian:** pengecualian terhadap DoD ini HANYA dapat dilakukan dengan persetujuan tertulis dari pembuat kebijakan dan WAJIB didokumentasikan.

### Pasal 17 - Revisi DoD

(1) Perubahan terhadap DoD ini HANYA dapat dilakukan melalui amandemen resmi.

(2) Setiap amandemen WAJIB mencantumkan:
   - Nomor amandemen
   - Tanggal perubahan
   - Deskripsi perubahan
   - Alasan perubahan

(3) Perubahan berlaku untuk fitur yang belum dimulai. Fitur yang sedang dikembangkan tidak wajib mengikuti amandemen baru.

---

**Ditetapkan pada tanggal 7 Februari 2026**

**Standar ini WAJIB ditaati oleh seluruh tim pengembangan.**
