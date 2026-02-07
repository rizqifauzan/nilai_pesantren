# TODO - Sistem Raport Akademik (Nilai Pesantren)

## 📋 Project Overview

**Project Name:** Sistem Raport Akademik (Nilai Pesantren)  
**Type:** Academic Report Card System for Islamic Boarding Schools  
**Development Timeline:** 18 Weeks  
**Status:** Planning Phase

### Objectives
- [ ] Build a comprehensive academic report card system for pesantren
- [ ] Implement secure admin authentication system
- [ ] Create master data management for students, teachers, classes, and subjects
- [ ] Develop grade calculation and ranking system
- [ ] Build report card generation with finalization workflow
- [ ] Implement personality and attendance tracking
- [ ] Ensure data integrity with read-only finalization
- [ ] Achieve 80%+ test coverage for critical business code
- [ ] Deploy to production with Vercel

---

## 🛠️ Tech Stack & Architecture

### Frontend
- [ ] Next.js 14+ with App Router
- [ ] React Server Components
- [ ] Tailwind CSS for styling
- [ ] shadcn/ui component library
- [ ] React Hook Form + Zod for form validation
- [ ] TanStack Table for data tables

### Backend
- [ ] Next.js API Routes
- [ ] Prisma ORM for database access
- [ ] NextAuth.js v5 for authentication

### Database
- [ ] Neon DB (PostgreSQL) - Serverless
- [ ] Auto-scaling configuration
- [ ] Connection pooling optimization

### Deployment
- [ ] Vercel for hosting
- [ ] GitHub integration for auto-deploy
- [ ] Environment variable management
- [ ] CI/CD pipeline setup

---

## 🗄️ Database Schema Summary

### Core Tables (15 total)
- [ ] **users** - Admin authentication
- [ ] **students** - Student records
- [ ] **teachers** - Teacher records
- [ ] **classes** - Class templates
- [ ] **academic_years** - Academic year records
- [ ] **subjects** - Subject master data
- [ ] **class_academic_years** - Running classes per year
- [ ] **student_enrollments** - Student-class relationships
- [ ] **class_subjects** - Subjects per class with KKM
- [ ] **report_cards** - Parent report records with finalization status
- [ ] **grades** - Subject grades per student
- [ ] **personality_traits** - Character assessment aspects
- [ ] **personality_grades** - Character grades (A-E)
- [ ] **attendance_types** - Attendance type master
- [ ] **attendance_records** - Attendance counts per type

### Database Setup Tasks
- [ ] Create Prisma schema file
- [ ] Define all 15 tables with relationships
- [ ] Set up indexes for performance
- [ ] Create database migrations
- [ ] Seed initial data (admin user, attendance types)
- [ ] Configure connection pooling
- [ ] Set up backup strategy

---

## 📐 Critical Business Rules

### 1. Single Value Principle
- [ ] Implement validation: One subject = one grade per student per report card
- [ ] Prevent duplicate grade entries
- [ ] Add unique constraint on (report_card_id, student_id, subject_id)
- [ ] Create error handling for duplicate attempts

### 2. Integrity Principle
- [ ] Implement finalization flag on report_cards table
- [ ] Create read-only middleware for finalized reports
- [ ] Prevent any data modification after finalization
- [ ] Add audit trail for finalization actions
- [ ] Display warning before finalization

### 3. Completeness Principle
- [ ] Validate promotion decisions exist before finalization
- [ ] Check all grades are entered
- [ ] Verify personality grades are complete
- [ ] Ensure attendance records are present
- [ ] Block finalization if incomplete

### 4. Consistency Principle
- [ ] Implement historical data immutability
- [ ] Create versioning for master data changes
- [ ] Use effective date patterns for updates
- [ ] Prevent retroactive changes to finalized reports
- [ ] Archive old academic years properly

---

## 🚀 Development Phases

### Phase 1: Foundation (Week 1-2)
**Goal:** Set up project infrastructure and core authentication

#### Week 1: Project Setup
- [ ] Initialize Next.js 14+ project with App Router
- [ ] Configure TypeScript and ESLint
- [ ] Set up Tailwind CSS
- [ ] Install and configure shadcn/ui
- [ ] Set up Prisma with Neon DB
- [ ] Create database schema
- [ ] Run initial migrations
- [ ] Set up environment variables (.env.example)
- [ ] Configure GitHub repository
- [ ] Set up Vercel project

#### Week 2: Authentication
- [ ] Install NextAuth.js v5
- [ ] Configure authentication providers
- [ ] Create admin user model
- [ ] Implement login page
- [ ] Create protected route middleware
- [ ] Set up session management
- [ ] Create admin dashboard layout
- [ ] Implement logout functionality
- [ ] Add authentication error handling
- [ ] Test authentication flow

---

### Phase 2: Master Data CRUD (Week 3-4)
**Goal:** Create CRUD operations for all master data

#### Week 3: Basic Master Data
- [ ] Create students CRUD (Create, Read, Update, Delete)
- [ ] Create teachers CRUD
- [ ] Create classes CRUD
- [ ] Create academic_years CRUD
- [ ] Create subjects CRUD
- [ ] Implement form validation with Zod
- [ ] Add data table with sorting/filtering
- [ ] Create confirmation dialogs for delete
- [ ] Add search functionality
- [ ] Test all CRUD operations

#### Week 4: Advanced Master Data
- [ ] Create class_academic_years CRUD
- [ ] Create student_enrollments CRUD
- [ ] Create class_subjects CRUD with KKM
- [ ] Create personality_traits CRUD
- [ ] Create attendance_types CRUD
- [ ] Implement relationship validation
- [ ] Add bulk import functionality
- [ ] Create data export feature
- [ ] Add data validation rules
- [ ] Test all relationships

---

### Phase 3: Operational Data (Week 5-6)
**Goal:** Build operational data management features

#### Week 5: Enrollment Management
- [ ] Create enrollment form
- [ ] Implement student-to-class assignment
- [ ] Create teacher-to-class assignment
- [ ] Build class schedule view
- [ ] Create student list per class
- [ ] Implement enrollment validation
- [ ] Add enrollment history tracking
- [ ] Create bulk enrollment feature
- [ ] Add enrollment reports
- [ ] Test enrollment workflows

#### Week 6: Subject Management
- [ ] Create subject assignment to classes
- [ ] Implement KKM (Minimum Passing Grade) configuration
- [ ] Create teacher-subject assignment
- [ ] Build subject list per class
- [ ] Create subject weight configuration
- [ ] Implement subject validation
- [ ] Add subject reordering
- [ ] Create subject templates
- [ ] Add subject reports
- [ ] Test subject workflows

---

### Phase 4: Grades & Calculations (Week 7-8)
**Goal:** Implement grade entry and calculation system

#### Week 7: Grade Entry
- [ ] Create grade entry form
- [ ] Implement grade validation (0-100)
- [ ] Add grade input per student per subject
- [ ] Create bulk grade entry
- [ ] Implement grade auto-save
- [ ] Add grade history tracking
- [ ] Create grade validation rules
- [ ] Implement grade comments
- [ ] Add grade approval workflow
- [ ] Test grade entry

#### Week 8: Calculations
- [ ] Implement average calculation per subject
- [ ] Implement overall average calculation
- [ ] Create ranking system per class
- [ ] Implement KKM status check
- [ ] Create grade summary reports
- [ ] Implement grade statistics
- [ ] Add grade distribution charts
- [ ] Create class performance reports
- [ ] Implement subject performance analysis
- [ ] Test all calculations

---

### Phase 5: Report Cards & Finalization (Week 9-10) ⚠️ CRITICAL
**Goal:** Build report card generation and finalization workflow

#### Week 9: Report Card Generation
- [ ] Create report card template
- [ ] Implement report card data aggregation
- [ ] Build report card preview
- [ ] Create student report card view
- [ ] Implement class report card view
- [ ] Add report card filters
- [ ] Create report card export (PDF)
- [ ] Implement report card printing
- [ ] Add report card sharing
- [ ] Test report card generation

#### Week 10: Finalization Workflow
- [ ] Implement finalization validation
- [ ] Create finalization confirmation dialog
- [ ] Add finalization warning messages
- [ ] Implement read-only enforcement
- [ ] Create finalization audit log
- [ ] Add finalization status indicators
- [ ] Implement finalization rollback (admin only)
- [ ] Create finalization reports
- [ ] Add finalization notifications
- [ ] Test finalization workflow thoroughly

---

### Phase 6: Personality & Attendance (Week 11)
**Goal:** Implement character assessment and attendance tracking

#### Personality Assessment
- [ ] Create personality trait CRUD
- [ ] Implement personality grade entry (A-E)
- [ ] Create personality assessment form
- [ ] Add personality comments
- [ ] Create personality summary reports
- [ ] Implement personality statistics
- [ ] Add personality trend analysis
- [ ] Create personality certificates
- [ ] Test personality assessment

#### Attendance Tracking
- [ ] Create attendance type CRUD
- [ ] Implement attendance entry form
- [ ] Create bulk attendance entry
- [ ] Add attendance calculation
- [ ] Create attendance summary reports
- [ ] Implement attendance alerts
- [ ] Add attendance trends
- [ ] Create attendance certificates
- [ ] Test attendance tracking

---

### Phase 7: Frontend Development (Week 12-16)
**Goal:** Build complete user interface with theme implementation

#### Week 12: Dashboard & Navigation
- [ ] Create main dashboard layout
- [ ] Implement navigation menu
- [ ] Create dashboard widgets
- [ ] Add quick actions
- [ ] Create notification center
- [ ] Implement user profile
- [ ] Add theme toggle (if needed)
- [ ] Create responsive design
- [ ] Add loading states
- [ ] Test dashboard

#### Week 13: Master Data Pages
- [ ] Create students list page
- [ ] Create teachers list page
- [ ] Create classes list page
- [ ] Create subjects list page
- [ ] Create academic years list page
- [ ] Implement data tables with sorting
- [ ] Add filtering and search
- [ ] Create detail views
- [ ] Add pagination
- [ ] Test all pages

#### Week 14: Grades & Reports Pages
- [ ] Create grade entry page
- [ ] Create report card page
- [ ] Create class performance page
- [ ] Create student performance page
- [ ] Create ranking page
- [ ] Implement charts and graphs
- [ ] Add export functionality
- [ ] Create print views
- [ ] Add responsive design
- [ ] Test all pages

#### Week 15: Personality & Attendance Pages
- [ ] Create personality assessment page
- [ ] Create attendance tracking page
- [ ] Create attendance summary page
- [ ] Create personality summary page
- [ ] Implement visual indicators
- [ ] Add trend charts
- [ ] Create certificates
- [ ] Add export functionality
- [ ] Test all pages

#### Week 16: Polish & UX
- [ ] Implement loading skeletons
- [ ] Add error boundaries
- [ ] Create empty states
- [ ] Add success notifications
- [ ] Implement confirmation dialogs
- [ ] Add tooltips and help text
- [ ] Create onboarding flow
- [ ] Add keyboard shortcuts
- [ ] Optimize performance
- [ ] Final UX testing

---

### Phase 8: Testing & Polish (Week 17-18)
**Goal:** Comprehensive testing and production readiness

#### Week 17: Testing
- [ ] Write unit tests for business logic
- [ ] Write integration tests for API routes
- [ ] Write E2E tests for critical flows
- [ ] Test all acceptance scenarios (50+)
- [ ] Performance testing
- [ ] Security testing
- [ ] Cross-browser testing
- [ ] Mobile responsiveness testing
- [ ] Accessibility testing
- [ ] Load testing

#### Week 18: Polish & Deployment
- [ ] Fix all identified bugs
- [ ] Optimize database queries
- [ ] Implement caching strategies
- [ ] Add monitoring and logging
- [ ] Create deployment documentation
- [ ] Set up production environment
- [ ] Deploy to Vercel
- [ ] Configure domain and SSL
- [ ] Create user documentation
- [ ] Final acceptance testing

---

## ✅ Testing Requirements

### Acceptance Test Scenarios (50+)

#### Value Validation Tests
- [ ] Test grade range validation (0-100)
- [ ] Test duplicate grade prevention
- [ ] Test KKM validation
- [ ] Test personality grade validation (A-E)
- [ ] Test attendance count validation
- [ ] Test required field validation
- [ ] Test data type validation
- [ ] Test relationship validation

#### Average Calculation Tests
- [ ] Test subject average calculation
- [ ] Test overall average calculation
- [ ] Test weighted average calculation
- [ ] Test average with missing grades
- [ ] Test average rounding rules
- [ ] Test average edge cases (all zeros, all perfect)
- [ ] Test average calculation accuracy

#### Ranking Tests
- [ ] Test class ranking calculation
- [ ] Test tie handling in ranking
- [ ] Test ranking with equal averages
- [ ] Test ranking updates after grade changes
- [ ] Test ranking after finalization
- [ ] Test ranking across multiple classes

#### KKM Status Tests
- [ ] Test KKM pass/fail determination
- [ ] Test KKM status per subject
- [ ] Test overall KKM status
- [ ] Test KKM status display
- [ ] Test KKM status in reports
- [ ] Test KKM status after finalization

#### Promotion Decision Tests
- [ ] Test promotion decision logic
- [ ] Test promotion with all passes
- [ ] Test promotion with failures
- [ ] Test promotion with borderline cases
- [ ] Test promotion decision validation
- [ ] Test promotion decision display

#### Finalization Tests
- [ ] Test finalization validation
- [ ] Test finalization with complete data
- [ ] Test finalization with incomplete data
- [ ] Test read-only enforcement after finalization
- [ ] Test finalization audit logging
- [ ] Test finalization rollback (admin)
- [ ] Test finalization status display

#### Report Printing Tests
- [ ] Test individual report card printing
- [ ] Test class report printing
- [ ] Test PDF export
- [ ] Test print layout
- [ ] Test print with Arabic text
- [ ] Test batch printing

#### Master Data Tests
- [ ] Test student CRUD operations
- [ ] Test teacher CRUD operations
- [ ] Test class CRUD operations
- [ [ ] Test subject CRUD operations
- [ ] Test academic year CRUD operations
- [ ] Test enrollment operations
- [ ] Test subject assignment operations
- [ ] Test data relationships

#### Personality & Attendance Tests
- [ ] Test personality grade entry
- [ ] Test personality summary calculation
- [ ] Test attendance entry
- [ ] Test attendance calculation
- [ ] Test attendance summary
- [ ] Test personality and attendance in reports

---

## 🎯 Definition of Done Checklist

### Code Quality
- [ ] Code follows naming conventions
- [ ] Code is properly commented
- [ ] No console.log statements in production code
- [ ] No hardcoded credentials
- [ ] Proper error handling implemented
- [ ] TypeScript strict mode enabled
- [ ] ESLint rules configured and passing
- [ ] Prettier formatting applied

### Testing Coverage
- [ ] Minimum 80% line coverage for critical business code
- [ ] 100% coverage for validation functions
- [ ] 100% coverage for calculation functions
- [ ] All acceptance test scenarios PASS
- [ ] Unit tests written for business logic
- [ ] Integration tests written for API routes
- [ ] E2E tests written for critical flows

### Performance
- [ ] Page load time < 2 seconds
- [ ] API response time < 500ms (normal operations)
- [ ] Database queries optimized
- [ ] Images optimized
- [ ] Code splitting implemented
- [ ] Lazy loading implemented
- [ ] Caching strategy implemented

### Business Rules Compliance
- [ ] Single Value Principle implemented
- [ ] Integrity Principle implemented
- [ ] Completeness Principle implemented
- [ ] Consistency Principle implemented
- [ ] All business rules tested
- [ ] Edge cases handled

### Documentation
- [ ] API documentation complete
- [ ] User documentation complete
- [ ] Deployment documentation complete
- [ ] Code comments adequate
- [ ] README updated
- [ ] CHANGELOG maintained

### Security
- [ ] Authentication implemented
- [ ] Authorization implemented
- [ ] Input validation implemented
- [ ] SQL injection prevention
- [ ] XSS prevention
- [ ] CSRF protection
- [ ] Environment variables secured
- [ ] Secrets management configured

---

## 🎨 Theme Design Specifications

### Color Palette
- **Primary:** Sage Green (#5C8D6E)
  - [ ] Apply to primary buttons
  - [ ] Apply to active states
  - [ ] Apply to success indicators
  - [ ] Apply to headers

- **Secondary:** Sand/Cream (#F5E6D3)
  - [ ] Apply to backgrounds
  - [ ] Apply to cards
  - [ ] Apply to secondary elements

- **Accent:** Dark Navy (#1E3A5F)
  - [ ] Apply to text
  - [ ] Apply to borders
  - [ ] Apply to important elements

- **Background:** Off White (#FAFAFA)
  - [ ] Apply to page backgrounds
  - [ ] Apply to sections

### Typography
- **Headings:** Inter font
  - [ ] Apply to all headings (h1-h6)
  - [ ] Configure font weights
  - [ ] Set line heights

- **Body:** Inter font
  - [ ] Apply to body text
  - [ ] Configure font sizes
  - [ ] Set line heights

- **Arabic:** Amiri font
  - [ ] Apply to Arabic text
  - [ ] Configure RTL support
  - [ ] Set appropriate sizes

### Component Styling
- [ ] Style all shadcn/ui components with theme
- [ ] Create custom button variants
- [ ] Style data tables
- [ ] Style forms and inputs
- [ ] Style cards and containers
- [ ] Style modals and dialogs
- [ ] Style notifications and alerts
- [ ] Style loading states

### Responsive Design
- [ ] Mobile-first approach
- [ ] Breakpoints: sm, md, lg, xl
- [ ] Touch-friendly targets
- [ ] Responsive tables
- [ ] Responsive forms
- [ ] Responsive navigation

---

## 🔧 Environment Configuration

### Development Environment
- [ ] Node.js 18+ installed
- [ ] pnpm/npm/yarn configured
- [ ] Git configured
- [ ] VS Code with extensions
- [ ] Environment variables set (.env.local)

### Required Environment Variables
```env
# Database
DATABASE_URL=

# NextAuth
NEXTAUTH_SECRET=
NEXTAUTH_URL=

# Application
NODE_ENV=development

# Optional
NEXT_PUBLIC_APP_URL=
```

### Production Environment
- [ ] Neon DB production instance
- [ ] Vercel project configured
- [ ] Domain configured
- [ ] SSL certificate
- [ ] Environment variables set
- [ ] Monitoring configured
- [ ] Backup strategy
- [ ] Error tracking (Sentry)

---

## ⚠️ Risk Mitigation Strategies

### Technical Risks
- [ ] **Database Performance:** Implement connection pooling, add indexes, monitor query performance
- [ ] **Scalability:** Use serverless architecture, implement caching, optimize bundle size
- [ ] **Data Integrity:** Implement strict validation, use database constraints, add audit logs
- [ ] **Security:** Implement authentication, validate inputs, use HTTPS, secure environment variables

### Project Risks
- [ ] **Timeline:** Break down tasks, prioritize features, have buffer time
- [ ] **Scope Creep:** Define clear requirements, have change management process
- [ ] **Resource Allocation:** Plan resources ahead, have backup plans
- [ ] **Knowledge Transfer:** Document everything, conduct code reviews, pair programming

### Business Risks
- [ ] **User Adoption:** Create intuitive UI, provide training, gather feedback
- [ ] **Data Migration:** Plan migration strategy, test thoroughly, have rollback plan
- [ ] **Compliance:** Follow regulations, implement audit trails, secure data
- [ ] **Maintenance:** Create maintenance plan, monitor system, have support process

---

## 📊 Progress Tracking

### Overall Progress
- [ ] Phase 1: Foundation (0/20 tasks)
- [ ] Phase 2: Master Data CRUD (0/20 tasks)
- [ ] Phase 3: Operational Data (0/20 tasks)
- [ ] Phase 4: Grades & Calculations (0/20 tasks)
- [ ] Phase 5: Report Cards & Finalization (0/20 tasks) ⚠️ CRITICAL
- [ ] Phase 6: Personality & Attendance (0/18 tasks)
- [ ] Phase 7: Frontend Development (0/50 tasks)
- [ ] Phase 8: Testing & Polish (0/20 tasks)

### Milestones
- [ ] MVP Complete (End of Phase 5)
- [ ] Beta Release (End of Phase 7)
- [ ] Production Launch (End of Phase 8)

---

## 📝 Notes

### Important Reminders
- Finalization is CRITICAL - once finalized, data is permanently read-only
- All business rules must be implemented before testing
- Test coverage must meet requirements before deployment
- Performance targets must be met
- Security must be prioritized throughout

### Dependencies
- Neon DB account required
- Vercel account required
- GitHub repository required
- Domain name (optional for production)

### Resources
- Next.js Documentation: https://nextjs.org/docs
- Prisma Documentation: https://www.prisma.io/docs
- NextAuth.js Documentation: https://authjs.dev
- shadcn/ui Documentation: https://ui.shadcn.com
- Tailwind CSS Documentation: https://tailwindcss.com/docs

---

**Last Updated:** 2026-02-07  
**Version:** 1.0  
**Status:** Planning Phase
