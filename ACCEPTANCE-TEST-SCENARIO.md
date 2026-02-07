# Acceptance Test Scenario (ATS)
## Senjata QA & AI - Sistem Raport Akademik

---

**Nomor:** 001/ATS/2026  
**Tanggal:** 7 Februari 2026  
**Status:** WAJIB DILAKUKAN  
**Referensi:** [KITAB-ATURAN.md](KITAB-ATURAN.md), [PRD.md](PRD.md)

---

## PENDAHULUAN

### Tujuan Dokumen

Dokumen Acceptance Test Scenario (ATS) ini berfungsi sebagai:
1. **Pedoman QA** - Manual testing untuk memverifikasi setiap fitur
2. **Skenario AI** - Input untuk AI coding assistant dalam memahami aturan bisnis
3. **Validasi Sistem** - Checklist untuk memastikan sistem memenuhi spesifikasi

### Cara Menggunakan

Setiap skenario memiliki format:
- **ID**: Kode unik skenario
- **Kategori**: Bidang yang diuji
- **Pre-condition**: Kondisi sebelum test
- **Steps**: Langkah-langkah test
- **Expected Result**: Hasil yang diharapkan
- **Status**: PASS/FAIL

---

## BAGIAN A: ATURAN NILAI

### A.1 - Validasi Input Nilai

**ATS-NIL-001: Input nilai valid (0-100)**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa enrollment di kelas, mapel ditentukan |
| Steps | 1. Buka halaman input nilai<br>2. Input nilai 0<br>3. Simpan |
| Expected Result | Nilai 0 tersimpan |

**ATS-NIL-002: Input nilai valid (100)**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa enrollment di kelas, mapel ditentukan |
| Steps | 1. Buka halaman input nilai<br>2. Input nilai 100<br>3. Simpan |
| Expected Result | Nilai 100 tersimpan |

**ATS-NIL-003: Input nilai desimal DITOLAK**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa enrollment di kelas, mapel ditentukan |
| Steps | 1. Buka halaman input nilai<br>2. Input nilai 75.5<br>3. Simpan |
| Expected Result | Sistem menolak dengan error "Nilai harus angka bulat" |

**ATS-NIL-004: Input nilai negatif DITOLAK**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa enrollment di kelas, mapel ditentukan |
| Steps | 1. Buka halaman input nilai<br>2. Input nilai -5<br>3. Simpan |
| Expected Result | Sistem menolak dengan error "Nilai minimum 0" |

**ATS-NIL-005: Input nilai >100 DITOLAK**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa enrollment di kelas, mapel ditentukan |
| Steps | 1. Buka halaman input nilai<br>2. Input nilai 101<br>3. Simpan |
| Expected Result | Sistem menolak dengan error "Nilai maksimum 100" |

**ATS-NIL-006: Input nilai huruf DITOLAK**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa enrollment di kelas, mapel ditentukan |
| Steps | 1. Buka halaman input nilai<br>2. Input nilai "delapan puluh"<br>3. Simpan |
| Expected Result | Sistem menolak dengan error "Nilai harus angka" |

---

### A.2 - Nilai NULL vs 0

**ATS-NIL-007: Nilai NULL berbeda dengan 0**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa memiliki nilai NULL dan siswa lain punya nilai 0 |
| Steps | 1. Lihat tampilan nilai<br>2. Bandingkan |
| Expected Result | NULL ditampilkan berbeda dari 0 (misal: "-" vs "0") |

**ATS-NIL-008: Nilai NULL saat draft DITERIMA**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas berstatus draft |
| Steps | 1. Biarkan nilai mapel kosong<br>2. Simpan |
| Expected Result | Nilai NULL tersimpan, tidak error |

**ATS-NIL-009: ⭐ NULL menjadi 0 SAAT FINAL (CONTOH UTAMA)**

| Field | Value |
|-------|-------|
| Pre-condition | 1. Kelas memiliki 10 mapel<br>2. Siswa A punya 10 nilai<br>3. Siswa B punya 9 nilai, 1 NULL<br>4. Semua keputusan kenaikan terisi |
| Steps | 1. Klik "Mark as Final"<br>2. Konfirmasi |
| Expected Result | - Siswa B: nilai NULL otomatis menjadi 0<br>- 10 mapel × 9 nilai + 1 × 0 = 90 (bukan 9)<br>- STATUS: PASS jika NULL→0, FAIL jika tidak |

**Kriteria Koreksi AI/QA:**
```
JIKA sistem tidak mengubah NULL ke 0 SAAT FINAL → 
  STATUS = FAIL
  BUG = Aturan bisnis Pasal 16 ayat 4 dilanggar
```

**ATS-NIL-010: Nilai 0 TIDAK berubah saat final**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa punya nilai 0 di satu mapel |
| Steps | 1. Finalisasi kelas |
| Expected Result | Nilai 0 tetap 0, tidak berubah |

---

## BAGIAN B: PERHITUNGAN RATA-RATA

### B.1 - Rumus Rata-rata

**ATS-RAT-001: Rata-rata tanpa NULL**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa punya nilai: 80, 90, 70 (3 mapel) |
| Steps | 1. Lihat rata-rata |
| Expected Result | (80+90+70)÷3 = 80.00 |

**ATS-RAT-002: Rata-rata dengan NULL (sebelum final)**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa punya nilai: 80, 90, NULL (3 mapel, 1 NULL) |
| Steps | 1. Lihat rata-rata |
| Expected Result | (80+90)÷2 = 85.00 (NULL TIDAK dihitung) |

**ATS-RAT-003: ⭐ Rata-rata setelah final (NULL→0)**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa punya nilai: 80, 90, NULL → menjadi 80,90,0 |
| Steps | 1. Finalisasi<br>2. Lihat rata-rata |
| Expected Result | (80+90+0)÷3 = 56.66 (bukan 85!) |

**ATS-RAT-004: Semua NULL menjadi 0**

| Field | Value |
|-------|-------|
| Pre-condition | 10 mapel, semua NULL |
| Steps | 1. Finalisasi<br>2. Lihat rata-rata |
| Expected Result | (0×10)÷10 = 0.00 |

---

## BAGIAN C: PERINGKAT (RANKING)

### C.1 - Urutan Ranking

**ATS-RNK-001: Ranking berdasarkan rata-rata tertinggi**

| Field | Value |
|-------|-------|
| Pre-condition | 3 siswa:<br>- Siswa A: rata-rata 85<br>- Siswa B: rata-rata 90<br>- Siswa C: rata-rata 78 |
| Steps | 1. Lihat ranking |
| Expected Result | 1. Siswa B, 2. Siswa A, 3. Siswa C |

**ATS-RNK-002: Ranking sama rata-rata urut nama**

| Field | Value |
|-------|-------|
| Pre-condition | 2 siswa sama rata-rata 85:<br>- Siswa Ali<br>- Siswa Budi |
| Steps | 1. Lihat ranking |
| Expected Result | 1. Ali, 2. Budi (A-Z) |

**ATS-RNK-003: Ranking HANYA siswa aktif**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa A (aktif, rata 80), Siswa B (pindah, rata 90) |
| Steps | 1. Lihat ranking |
| Expected Result | Ranking hanya tampil untuk Siswa A |

---

## BAGIAN D: STATUS KELULUSAN MAPEL

### D.1 - KKM (Kriteria Ketuntasan Minimum)

**ATS-KKM-001: Nilai = KKM → LULUS**

| Field | Value |
|-------|-------|
| Pre-condition | KKM = 60, Siswa punya nilai 60 |
| Steps | 1. Lihat status kelulusan |
| Expected Result | Status: LULUS |

**ATS-KKM-002: Nilai > KKM → LULUS**

| Field | Value |
|-------|-------|
| Pre-condition | KKM = 60, Siswa punya nilai 75 |
| Steps | 1. Lihat status kelulusan |
| Expected Result | Status: LULUS |

**ATS-KKM-003: Nilai < KKM → TIDAK LULUS**

| Field | Value |
|-------|-------|
| Pre-condition | KKM = 60, Siswa punya nilai 55 |
| Steps | 1. Lihat status kelulusan |
| Expected Result | Status: TIDAK LULUS |

---

## BAGIAN E: KEPUTUSAN KENAIKAN KELAS

### E.1 - Input Keputusan

**ATS-KNK-001: Keputusan NAIK**

| Field | Value |
|-------|-------|
| Pre-condition | Draft, siswa layak naik |
| Steps | 1. Pilih "NAIK Ke Kelas 3"<br>2. Simpan |
| Expected Result | is_promoted=TRUE, promotion_note="NAIK Ke Kelas 3" |

**ATS-KNK-002: Keputusan TINGGAL**

| Field | Value |
|-------|-------|
| Pre-condition | Draft, siswa tidak layak naik |
| Steps | 1. Pilih "TINGGAL di Kelas 2"<br>2. Simpan |
| Expected Result | is_promoted=FALSE, promotion_note="TINGGAL di Kelas 2" |

**ATS-KNK-003: Keputusan BOLEH kosong saat draft**

| Field | Value |
|-------|-------|
| Pre-condition | Draft |
| Steps | 1. Biarkan keputusan kosong<br>2. Simpan |
| Expected Result | Tersimpan tanpa error |

---

### E.2 - Finalisasi dengan Keputusan

**ATS-KNK-004: ⭐ Finalisasi DITOLAK jika ada keputusan kosong**

| Field | Value |
|-------|-------|
| Pre-condition | 10 siswa, 9 punya keputusan, 1 kosong |
| Steps | 1. Klik "Mark as Final" |
| Expected Result | Sistem menolak dengan error "Semua keputusan kenaikan WAJIB terisi" |

**ATS-KNK-005: Finalisasi DITERIMA jika semua keputusan terisi**

| Field | Value |
|-------|-------|
| Pre-condition | 10 siswa, SEMUA punya keputusan |
| Steps | 1. Klik "Mark as Final"<br>2. Konfirmasi |
| Expected Result | Finalisasi berhasil, status=final |

---

## BAGIAN F: FINALISASI

### F.1 - Proses Finalisasi

**ATS-FIN-001: ⭐ NULL → 0 SAAT FINALISASI (ATURAN KUNCI)**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas draft, ada nilai NULL |
| Steps | 1. Klik "Mark as Final"<br>2. Konfirmasi<br>3. Cek nilai |
| Expected Result | SEMUA nilai NULL berubah menjadi 0 |

**Kriteria Validasi:**
```
CHECKPOINT: Setelah finalisasi, query:
  SELECT nilai FROM scores WHERE nilai IS NULL
  
HASIL YANG BENAR: 0 rows (tidak ada NULL)
HASIL YANG SALAH: Ada rows dengan NULL

JIKA ADA NULL → FAIL, sistem tidak sesuai Pasal 22 ayat 2 KITAB-ATURAN
```

**ATS-FIN-002: Nilai TIDAK NULL tetap sama**

| Field | Value |
|-------|-------|
| Pre-condition | Nilai 80, 90, 75 |
| Steps | 1. Finalisasi<br>2. Cek nilai |
| Expected Result | Nilai tetap 80, 90, 75 |

**ATS-FIN-003: Status final aktif**

| Field | Value |
|-------|-------|
| Pre-condition | Setelah finalisasi |
| Steps | 1. Cek status kelas |
| Expected Result | is_finalized=TRUE, finalized_at=timestamp, finalized_by=admin |

**ATS-FIN-004: Finalisasi IRREVERSIBLE**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas sudah final |
| Steps | 1. Coba klik "Unfinalize" atau ubah nilai |
| Expected Result | Sistem menolak, tidak ada tombol/fitur untuk membatalkan |

---

### F.2 - Perubahan Setelah Final (DITOLAK)

**ATS-FIN-005: Ubah nilai DITOLAK**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas sudah final |
| Steps | 1. Coba ubah nilai |
| Expected Result | Sistem menolak "Data sudah final, tidak dapat diubah" |

**ATS-FIN-006: Hapus enrollment DITOLAK**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas sudah final |
| Steps | 1. Coba hapus enrollment siswa |
| Expected Result | Sistem menolak "Enrollment tidak dapat dihapus" |

**ATS-FIN-007: Ubah keputusan DITOLAK**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas sudah final |
| Steps | 1. Coba ubah keputusan naik/tinggal |
| Expected Result | Sistem menolak "Data sudah final, tidak dapat diubah" |

**ATS-FIN-008: Edit via databaselangsung DITOLAK**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas sudah final |
| Steps | 1. Coba UPDATE langsung di database |
| Expected Result | Database constraint ERROR (foreign key/unchangeable) |

---

## BAGIAN G: PENCETAKAN RAPORT

### G.1 - Raport Draft

**ATS-RPT-001: ⭐ Watermark DRAFT muncul**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas berstatus draft |
| Steps | 1. Cetak raport |
| Expected Result | Ada watermark "DRAFT" yang terlihat jelas |

**ATS-RPT-002: Raport draft TIDAK berlaku resmi**

| Field | Value |
|-------|-------|
| Pre-condition | Cetak raport draft |
| Steps | 1. Baca raport |
| Expected Result | Tidak ada tanda tangan/tanggal finalisasi |

---

### G.2 - Raport Final

**ATS-RPT-003: ⭐ Watermark TIDAK muncul di final**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas sudah final |
| Steps | 1. Cetak raport |
| Expected Result | TIDAK ada watermark "DRAFT" |

**ATS-RPT-004: Raport final menampilkan SEMUA informasi**

| Field | Value |
|-------|-------|
| Pre-condition | Kelas sudah final |
| Steps | 1. Cetak dan baca raport |
| Expected Result | Terdapat:<br>- Identitas siswa<br>- Identitas kelas/tahun ajaran<br>- Semester<br>- Seluruh nilai per mapel<br>- Rata-rata<br>- Ranking<br>- Status kelulusan per mapel<br>- Keputusan kenaikan<br>- Tanggal dan penanggung jawab finalisasi |

**ATS-RPT-005: Nilai final sesuai data (NULL→0)**

| Field | Value |
|-------|-------|
| Pre-condition | Ada nilai NULL yang difinalisasi |
| Steps | 1. Cetak raport<br>2. Cek nilai NULL |
| Expected Result | Nilai NULL tampil sebagai 0 |

---

## BAGIAN H: MASTER DATA

### H.1 - Data Siswa

**ATS-SIS-001: NIS unik**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa A dengan NIS "001" ada |
| Steps | 1. Coba buat siswa B dengan NIS "001" |
| Expected Result | Sistem menolak "NIS sudah digunakan" |

**ATS-SIS-002: Satu siswa banyak enrollment**

| Field | Value |
|-------|-------|
| Pre-condition | Siswa A di Kelas 1 (2024) |
| Steps | 1. Daftarkan siswa A ke Kelas 2 (2025) |
| Expected Result | Enrollment baru dibuat, enrollment lama tetap ada |

---

### H.2 - Data Kelas

**ATS-KLS-001: Satu tahun ajaran aktif**

| Field | Value |
|-------|-------|
| Pre-condition | Tahun Ajaran 2024/2025 aktif |
| Steps | 1. Coba buat tahun ajaran baru 2024/2025 aktif |
| Expected Result | Sistem menolak "Hanya satu tahun ajaran boleh aktif" |

---

### H.3 - Data Mapel

**ATS-MPL-001: Satu mapel sekali dalam kelas**

| Field | Value |
|-------|-------|
| Pre-condition | Matematika di Kelas 2A sudah ada |
| Steps | 1. Coba tambahkan Matematika lagi di Kelas 2A |
| Expected Result | Sistem menolak "Mapel sudah ada di kelas ini" |

---

## BAGIAN I: NILAI KEPRIBADIAN

### I.1 - Nilai Kepribadian

**ATS-PERS-001: Input nilai huruf A-E**

| Field | Value |
|-------|-------|
| Pre-condition | Raport draft |
| Steps | 1. Input nilai kepribadian "Disiplin" dengan nilai "A" |
| Expected Result | Nilai A tersimpan |

**ATS-PERS-002: Nilai NULL dibolehkan saat draft**

| Field | Value |
|-------|-------|
| Pre-condition | Raport draft |
| Steps | 1. Biarkan nilai kepribadian kosong |
| Expected Result | NULL tersimpan tanpa error |

**ATS-PERS-003: Nilai kepribadian terkunci setelah final**

| Field | Value |
|-------|-------|
| Pre-condition | Raport sudah final |
| Steps | 1. Coba ubah nilai kepribadian |
| Expected Result | Sistem menolak "Data sudah final" |

**ATS-PERS-004: Hanya aspek aktif tampil di raport**

| Field | Value |
|-------|-------|
| Pre-condition | Aspect "Keberanian" inactive |
| Steps | 1. Lihat daftar aspek di raport draft |
| Expected Result | "Keberanian" tidak tampil |

---

## BAGIAN J: KEHADIRAN

### J.1 - Kehadiran

**ATS-ATT-001: Input jumlah hari izin**

| Field | Value |
|-------|-------|
| Pre-condition | Raport draft |
| Steps | 1. Input kehadiran "Izin" dengan nilai 2 |
| Expected Result | 2 hari izin tersimpan |

**ATS-ATT-002: Kehadiran terkunci setelah final**

| Field | Value |
|-------|-------|
| Pre-condition | Raport sudah final |
| Steps | 1. Coba ubah jumlah hari alfa |
| Expected Result | Sistem menolak "Data sudah final" |

**ATS-ATT-003: Satu jenis kehadiran per raport**

| Field | Value |
|-------|-------|
| Pre-condition | Jenis "Sakit" sudah ada dengan 3 hari |
| Steps | 1. Coba tambahkan "Sakit" lagi dengan 5 hari |
| Expected Result | Sistem menolak "Jenis kehadiran sudah ada" |

---

## MATRIKS PRIORITAS TEST

| Prioritas | ID Skenario | Keterangan |
|-----------|-------------|-------------|
| 🔴 KRITIK | ATS-NIL-009 | NULL→0 saat final (contoh utama user) |
| 🔴 KRITIK | ATS-FIN-001 | NULL→0 saat finalisasi |
| 🔴 KRITIK | ATS-KNK-004 | Finalisasi ditolak jika keputusan kosong |
| 🔴 KRITIK | ATS-FIN-005 s/d 008 | Perubahan setelah final ditolak |
| 🟠 TINGGI | ATS-RPT-001, 003 | Watermark DRAFT/FINAL |
| 🟠 TINGGI | ATS-RAT-002, 003 | Perhitungan rata-rata dengan NULL |
| 🟡 SEDANG | ATS-NIL-001 s/d 006 | Validasi input nilai |
| 🟡 SEDANG | ATS-KKM-001 s/d 003 | Status kelulusan |
| 🟡 SEDANG | ATS-PERS-001 s/d 004 | Nilai kepribadian |
| 🟡 SEDANG | ATS-ATT-001 s/d 003 | Kehadiran |
| 🟢 RENDAH | ATS-SIS-001 s/d 002 | Master data siswa |
| 🟢 RENDAH | ATS-KLS-001 | Master data kelas |

---

## CHECKLIST FINAL SEBELUM PRODUKSI

```
┌─────────────────────────────────────────────────────────────────┐
│              ACCEPTANCE TEST CHECKLIST                           │
├─────────────────────────────────────────────────────────────────┤
│ NILAI                                                         │
│ [ ] Nilai 0-100 valid                                         │
│ [ ] Desimal/negatif/huruf ditolak                            │
│ [ ] NULL ≠ 0 saat draft                                       │
│ [ ] NULL → 0 SAAT FINAL                                       │
├─────────────────────────────────────────────────────────────────┤
│ PERHITUNGAN                                                   │
│ [ ] Rata-rata = jumlah ÷ jumlah mapel                        │
│ [ ] NULL tidak dihitung dalam rata-rata (sebelum final)      │
│ [ ] NULL dihitung sebagai 0 (sesudah final)                   │
│ [ ] Ranking berdasarkan rata-rata tertinggi                  │
│ [ ] Ranking sama rata → urut nama (A-Z)                      │
├─────────────────────────────────────────────────────────────────┤
│ KENAIKAN KELAS                                                │
│ [ ] Keputusan boleh kosong saat draft                        │
│ [ ] Finalisasi DITOLAK jika ada keputusan kosong             │
├─────────────────────────────────────────────────────────────────┤
│ FINALISASI                                                    │
│ [ ] Setelah final → nilai tidak bisa diubah                   │
│ [ ] Setelah final → enrollment tidak bisa dihapus           │
│ [ ] Setelah final → keputusan tidak bisa diubah              │
│ [ ] Finalisasi irreversible                                  │
├─────────────────────────────────────────────────────────────────┤
│ RAPORT                                                        │
│ [ ] Draft → ada watermark DRAFT                              │
│ [ ] Final → tidak ada watermark DRAFT                        │
│ [ ] Final → menampilkan semua informasi                      │
│ [ ] Final → NULL tampil sebagai 0                            │
├─────────────────────────────────────────────────────────────────┤
│ NILAI KEPRIBADIAN                                               │
│ [ ] Nilai huruf A-E valid                                       │
│ [ ] NULL dibolehkan saat draft                                  │
│ [ ] Terkunci setelah final                                     │
│ [ ] Hanya aspek aktif tampil                                    │
├─────────────────────────────────────────────────────────────────┤
│ KEHADIRAN                                                      │
│ [ ] Input jumlah hari valid                                     │
│ [ ] Terkunci setelah final                                     │
│ [ ] Satu jenis per raport                                       │
├─────────────────────────────────────────────────────────────────┤
│ STATUS: [ ] SEMUA PASS / [ ] ADA FAIL                         │
└─────────────────────────────────────────────────────────────────┘
```

---

## CONTOH LAPORAN BUG

**Format Laporan:**

```
BUG REPORT
==========
ID: BUG-[YYYYMMDD]-[001]
Skenario: ATS-[ID] - [Judul]
Status: [OPEN/FIXED/VERIFIED]
Severity: [CRITICAL/HIGH/MEDIUM/LOW]

Deskripsi:
[S描述 bug yang ditemukan]

Expected Result:
[Hasil yang benar berdasarkan ATS]

Actual Result:
[Hasil yang salah dari sistem]

Steps to Reproduce:
1. [Langkah 1]
2. [Langkah 2]

Evidence:
[Screenshot/log]

Assigned to: [Developer]
```

---

**Dokumen ini adalah bagian tidak terpisahkan dari pengembangan sistem.**

**Referensi:**
- [PRD.md](PRD.md) - Product Requirements Document
- [KITAB-ATURAN.md](KITAB-ATURAN.md) - Business Rule Book
- [DEFINITION-OF-DONE.md](DEFINITION-OF-DONE.md) - Standar Kelengkapan
