# Development Plan - Sistem Raport Akademik

Dokumen ini menjabarkan rencana pengembangan sistem secara bertahap.

---

## 1. Arsitektur Teknis

### 1.1 Tech Stack Rekomendasi

| Layer | Teknologi | Catatan |
|-------|-----------|---------|
| **Frontend** | Next.js 14+ (React) | App Router, Server Components |
| **Database** | Neon DB (PostgreSQL) | Serverless, auto-scaling, gratis tier |
| **Deployment** | Vercel | Auto-deploy dari GitHub |
| **ORM** | Prisma | Type-safe database access |
| **Authentication** | NextAuth.js (v5) | Admin authentication |
| **Styling** | Tailwind CSS + shadcn/ui | Modern UI components |
| **Forms** | React Hook Form + Zod | Form validation |
| **Tables** | TanStack Table | Data table with sorting/filtering |
| **Charts** | Recharts | Untuk statistik (opsional) |

### 1.2 Neon DB Setup

1. **Buat Akun Neon**
   - Buka https://neon.tech
   - Sign up dengan GitHub
   - Buat project baru "nilai-pesantren"

2. **Get Connection String**
   - Di Neon Dashboard → Connection Details
   - Copy "Connection string" (format: `postgres://user:pass@ep-xxx.us-east-1.aws.neon.tech/nilai_pesantanamo?sslmode=require`)

3. **Configure Environment Variables**
   ```bash
   # .env
   DATABASE_URL="postgres://..."
   ```

### 1.3 Vercel Deployment

1. **Connect GitHub ke Vercel**
   - Buka https://vercel.com
   - Import repository

2. **Environment Variables di Vercel**
   - Vercel Dashboard → Project → Settings → Environment Variables
   - Add `DATABASE_URL`
   - Add `NEXTAUTH_SECRET`
   - Add `NEXTAUTH_URL`

3. **Auto Deploy**
   - Setiap push ke branch `main` → auto deploy
   - Preview deployments untuk PRs

### 1.4 Neon DB + Serverless Considerations

1. **Connection Pooling**
   - Neon menyediakan built-in connection pooling
   - Format URL dengan pooling:
   ```
   postgres://user:pass@ep-xxx.us-east-1.aws.neon.tech/nilai_pesantren?sslmode=require&pool_timeout=10
   ```

2. **Prisma Singleton untuk Serverless**
   ```typescript
   // src/lib/prisma.ts
   import { PrismaClient } from '@prisma/client'
   
   const globalForPrisma = globalThis as unknown as {
     prisma: PrismaClient | undefined
   }
   
   export const prisma = globalForPrisma.prisma ?? new PrismaClient()
   
   if (process.env.NODE_ENV !== 'production') globalForPrisma.prisma = prisma
   ```

3. **Error Handling untuk Serverless**
   ```typescript
   try {
     const result = await prisma.student.findMany()
     return Response.json({ success: true, data: result })
   } catch (error) {
     console.error('Database error:', error)
     return Response.json({ error: 'Database error' }, { status: 500 })
   }
   ```

### 1.5 Prisma Setup with Neon

```bash
# Install Prisma
npm install prisma @prisma/client

# Initialize Prisma
npx prisma init

# Generate Prisma Client
npx prisma generate

# Run migrations (atau let Vercel handle via prisma migrate deploy)
npx prisma migrate deploy

# Check database in Neon
npx prisma studio
```

### 1.6 Struktur Project (Next.js + Vercel + Neon DB)

```
nilai_pesantren/
├── prisma/
│   ├── schema.prisma        # Database schema
│   └── migrations/          # DB migrations
├── src/
│   ├── app/                 # Next.js App Router
│   │   ├── (auth)/          # Authentication pages
│   │   ├── dashboard/       # Dashboard pages
│   │   ├── api/             # API Routes (Serverless)
│   │   │   ├── students/
│   │   │   ├── grades/
│   │   │   └── report-cards/
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/
│   │   ├── ui/              # Reusable UI (shadcn/ui)
│   │   ├── forms/           # Form components
│   │   └── tables/          # Data tables
│   ├── lib/
│   │   ├── prisma.ts        # Prisma client singleton
│   │   ├── db.ts            # Database utilities
│   │   └── utils.ts         # Helper functions
│   └── styles/
│       └── globals.css
├── .env.example             # Environment variables template
├── vercel.json              # Vercel configuration
├── tailwind.config.ts       # Tailwind CSS
├── next.config.js           # Next.js configuration
├── package.json
└── README.md
```

---

## 2. Fase Pengembangan

### Fase 1: Foundation (Week 1-2)

#### 2.1.1 Setup Environment
- [ ] Inisialisasi Next.js project: `npx create-next-app@latest nilai_pesantren --typescript --tailwind --eslint`
- [ ] Install dependencies:
  ```bash
  npm install prisma @prisma/client next-auth zod react-hook-form @hookform/resolvers zustand @tanstack/react-table lucide-react class-variance-authority clsx tailwind-merge
  npm install -D prisma
  ```
- [ ] Setup Prisma:
  ```bash
  npx prisma init
  ```
- [ ] Konfigurasi environment variables (.env)
- [ ] Setup Git repository

#### 2.1.2 Database Schema (Prisma)
- [ ] Buat `prisma/schema.prisma` dengan semua models:
  ```prisma
  model Student {
    id        BigInt   @id @default(autoincrement())
    nis       String   @unique
    nisn      String?
    fullName  String
    gender    Gender?
    birthDate DateTime?
    status    StudentStatus @default(ACTIVE)
    createdAt DateTime @default(now())
    updatedAt DateTime @updatedAt
    enrollments Enrollment[]
  }
  ```
- [ ] Jalankan `npx prisma migrate dev --name init`
- [ ] Generate Prisma Client: `npx prisma generate`
- [ ] Setup Prisma singleton di `src/lib/prisma.ts`

#### 2.1.3 Base API (Next.js App Router)
- [ ] Setup Next.js App Router structure (`src/app/api/`)
- [ ] Buat `src/lib/prisma.ts` singleton untuk Prisma Client
- [ ] Setup error handling di `src/app/api/error.ts`
- [ ] Setup response helpers di `src/lib/api-response.ts`

---

### Fase 2: Master Data CRUD (Week 3-4)

#### 2.2.1 Students Management
- [ ] **Endpoint Structure**: `src/app/api/students/`
- [ ] POST `/api/students` - Create student (Zod validation)
- [ ] GET `/api/students` - List students (with pagination)
- [ ] GET `/api/students/[id]` - Get student detail
- [ ] PUT `/api/students/[id]` - Update student
- [ ] DELETE `/api/students/[id]` - Delete student
- [ ] Validasi NIS unik di Prisma schema + Zod

#### 2.2.2 Teachers Management
- [ ] **Endpoint Structure**: `src/app/api/teachers/`
- [ ] CRUD endpoints similar pattern

#### 2.2.3 Classes Management
- [ ] **Endpoint Structure**: `src/app/api/classes/`
- [ ] CRUD endpoints similar pattern

#### 2.2.4 Academic Years Management
- [ ] **Endpoint Structure**: `src/app/api/academic-years/`
- [ ] Validasi hanya 1 tahun ajaran aktif (database constraint)

#### 2.2.5 Subjects Management
- [ ] **Endpoint Structure**: `src/app/api/subjects/`
- [ ] CRUD endpoints similar pattern

---

### Fase 3: Operational Data (Week 5-6)

#### 2.3.1 Class Academic Years
- [ ] **Endpoint Structure**: `src/app/api/class-academic-years/`
- [ ] CRUD endpoints
- [ ] Assign homeroom teacher

#### 2.3.2 Student Enrollments
- [ ] **Endpoint Structure**: `src/app/api/enrollments/`
- [ ] GET with class_id filter
- [ ] DELETE with raport existence check
- [ ] Tracking histori enrollment

#### 2.3.3 Class Subjects
- [ ] **Endpoint Structure**: `src/app/api/class-subjects/`
- [ ] GET with class_id filter
- [ ] PUT for KKM update
- [ ] DELETE with grades existence check
- [ ] Unique constraint: class_id + subject_id

---

### Fase 4: Grades & Calculations (Week 7-8)

#### 2.4.1 Grades CRUD
- [ ] **Endpoint Structure**: `src/app/api/grades/`
- [ ] POST - Create grade (Zod: score 0-100 integer)
- [ ] GET with report_card_id filter
- [ ] PUT - Update grade
- [ ] DELETE - Delete grade
- [ ] Validasi unik: report_card_id + class_subject_id

#### 2.4.2 Average Calculation
- [ ] GET `/api/report-cards/[id]/average`
- [ ] Implementasi: AVG(score) where score IS NOT NULL
- [ ] Return JSON: `{ average: number, totalScore: number, subjectCount: number }`

#### 2.4.3 Ranking
- [ ] GET `/api/rankings?class_id=X&semester=Y`
- [ ] SQL: ORDER BY average DESC, full_name ASC
- [ ] Filter: student.status = 'ACTIVE'

#### 2.4.4 KKM Status
- [ ] GET `/api/grades/[id]/passing-status`
- [ ] Bandingkan: score >= kkm ? 'LULUS' : 'TIDAK LULUS'

---

### Fase 5: Report Cards & Finalization (Week 9-10)

#### 2.5.1 Report Cards
- [ ] **Endpoint Structure**: `src/app/api/report-cards/`
- [ ] POST - Create report card
- [ ] GET with enrollment_id filter
- [ ] GET /[id] - Get full report card with grades

#### 2.5.2 Promotion Decision
- [ ] PUT `/api/report-cards/[id]/promotion`
- [ ] Update: is_promoted, promotion_note
- [ ] Zod validation: promotion_note required if is_promoted set

#### 2.5.3 Finalization Process (CRITICAL)
- [ ] POST `/api/report-cards/[id]/finalize`
- [ ] Transaction:
  1. Check all is_promoted NOT NULL
  2. Check all promotion_note NOT NULL
  3. UPDATE grades SET score = 0 WHERE score IS NULL
  4. UPDATE report_card SET is_finalized = true, finalized_at = NOW(), finalized_by = admin_id
- [ ] Reject if already finalized

#### 2.5.4 Read-Only Protection
- [ ] Prisma middleware: block UPDATE/DELETE if is_finalized = true
- [ ] Database constraint (optional)

---

### Fase 6: Personality & Attendance (Week 11)

#### 2.6.1 Personality Traits & Grades
- [ ] **Endpoint Structure**: `src/app/api/personality-traits/`
- [ ] **Endpoint Structure**: `src/app/api/personality-grades/`
- [ ] GET personality-traits: filter is_active = true
- [ ] Personality grades: score enum A/B/C/D/E

#### 2.6.2 Attendance
- [ ] **Endpoint Structure**: `src/app/api/attendance-types/`
- [ ] **Endpoint Structure**: `src/app/api/attendance-records/`
- [ ] GET attendance-types: filter is_active = true
- [ ] Attendance records: value = integer (jumlah hari)

---

### Fase 7: Frontend Development (Week 12-16)

#### 2.7.1 Dashboard
- [ ] Halaman utama dengan statistik
- [ ] Daftar tahun ajaran aktif
- [ ] Quick actions

#### 2.7.2 Master Data Pages
- [ ] CRUD Students dengan form validasi
- [ ] CRUD Teachers
- [ ] CRUD Classes
- [ ] CRUD Academic Years
- [ ] CRUD Subjects

#### 2.7.3 Enrollment Page
- [ ] Daftar siswa per kelas
- [ ] Form enrollment siswa baru
- [ ] Tracking histori

#### 2.7.4 Grades Input Page
- [ ] Tabel: Siswa × Mapel
- [ ] Input nilai dengan validasi 0-100
- [ ] Auto-save atau manual save
- [ ] Tampilan rata-rata per siswa
- [ ] Ranking display

#### 2.7.5 Report Cards Page
- [ ] View raport per siswa
- [ ] Edit promotion decision
- [ ] Tombol "Mark as Final"
- [ ] Konfirmasi dialog

#### 2.7.6 Print/Raport Template
- [ ] Print preview
- [ ] Watermark "DRAFT" jika belum final
- [ ] Export PDF
- [ ] Raport final tanpa watermark

---

### Fase 8: Testing & Polish (Week 17-18)

#### 2.8.1 Unit Tests (Vitest / Jest)
- [ ] Test validasi nilai (ATS-NIL-001 s/d ATS-NIL-006)
- [ ] Test perhitungan rata-rata (ATS-RAT-001 s/d ATS-RAT-004)
- [ ] Test ranking (ATS-RNK-001 s/d ATS-RNK-003)
- [ ] Test finalisasi (ATS-FIN-001 s/d ATS-FIN-008)

#### 2.8.2 API Tests (Integration)
- [ ] Test API routes dengan test database
- [ ] Test database constraints
- [ ] Test Prisma transactions

#### 2.8.3 UI Tests (Playwright / Cypress)
- [ ] Test semua skenario ATS via browser
- [ ] Responsive design check
- [ ] Print/PDF generation test

#### 2.8.4 Vercel Deployment
- [ ] Push ke GitHub
- [ ] Import project di Vercel
- [ ] Set environment variables di Vercel:
  - `DATABASE_URL` (Neon connection string)
  - `NEXTAUTH_SECRET` (generate with `openssl rand -base64 32`)
  - `NEXTAUTH_URL` (your vercel domain)
- [ ] Trigger deployment
- [ ] Test di production URL

---

## 3. Urutan Implementasi (Topological Sort)

```
Week 1-2: Foundation + Database Schema
    ↓
Week 3-4: Master Data CRUD
    ↓
Week 5-6: Operational Data (Enrollment, Class Subjects)
    ↓
Week 7-8: Grades + Calculations
    ↓
Week 9-10: Report Cards + Finalization (CRITICAL)
    ↓
Week 11: Personality + Attendance
    ↓
Week 12-16: Frontend Development
    ↓
Week 17-18: Testing + Polish
```

---

## 4. Critical Path

1. **Database Schema** → Tanpa ini, tidak ada yang bisa dimulai
2. **Master Data CRUD** → Untuk setup data dasar
3. **Enrollment** → Untuk menghubungkan siswa ke kelas
4. **Class Subjects** → Untuk menentukan mapel per kelas
5. **Grades CRUD** → Core functionality
6. **Average + Ranking Calculations** → Feature utama
7. **Finalization** → Aturan bisnis kritis (NULL→0)
8. **Frontend** → User interface

---

## 5. Risiko & Mitigasi

| Risiko | Dampak | Mitigasi |
|--------|--------|----------|
| Finalisasi bug | Data terkunci salah | Unit test 100% untuk finalisasi |
| NULL→0 salah | Rata-rata salah | ATS-RAT-003 test |
| Ranking salah | Kesalahan perangkingan | ATS-RNK test |
| Enrollment dihapus setelah raport | Orphan data | Database constraint |

---

## 6. Definition of Done per Fase

Sebelum lanjut ke fase berikutnya, WAJIB:

- [ ] Semua API endpoints terdefinisi di OpenAPI/Swagger
- [ ] Unit test coverage ≥ 80%
- [ ] 100% test pass untuk fungsi validasi & perhitungan
- [ ] Code review passed
- [ ] No critical bugs

---

**Revisi: 1.0**
**Tanggal: 7 Februari 2026**
