<div align="center">

# 🏫 School Management System

**A full-stack, role-based school management platform built with Next.js 14**

[![Next.js](https://img.shields.io/badge/Next.js_14-black?style=for-the-badge&logo=next.js&logoColor=white)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Prisma](https://img.shields.io/badge/Prisma_v7-2D3748?style=for-the-badge&logo=prisma&logoColor=white)](https://www.prisma.io/)
[![NextAuth](https://img.shields.io/badge/NextAuth.js_v5-7C3AED?style=for-the-badge&logo=auth0&logoColor=white)](https://next-auth.js.org/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![Vercel](https://img.shields.io/badge/Deployed_on_Vercel-black?style=for-the-badge&logo=vercel&logoColor=white)](https://vercel.com/)
[![MIT License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)](LICENSE)

[Live Demo](#live-demo) · [Features](#features) · [Getting Started](#getting-started) · [Screenshots](#screenshots)

</div>

---

## About the Project

A production-grade **School Management System** built as a capstone portfolio project. It provides a unified platform for administrators, teachers, students, and parents — each with a tailored dashboard and role-specific access controls. The system covers the full academic lifecycle: enrollment, scheduling, attendance, examinations, results, and real-time announcements.

Built to demonstrate end-to-end full-stack engineering: relational database modeling, server-side rendering, type-safe APIs, role-based authentication, and data visualization.

---

## Features

### 👑 Admin
- Manage all users: students, teachers, and parents
- Create and configure classes, subjects, and academic years
- Publish school-wide announcements
- Access analytics dashboard with enrollment, attendance, and performance charts
- Oversee timetable scheduling across all classes

### 👨‍🏫 Teacher
- View assigned classes and subjects
- Record and manage daily attendance per class
- Create exams and enter student results (score, grade, pass/fail)
- Manage weekly timetable
- Post class-targeted announcements
- View per-class performance analytics

### 🎓 Student
- View personal profile, enrolled class, and roll number
- Check weekly timetable
- Track own attendance history
- View exam results with grades (A–F) and pass/fail status
- Read announcements targeted to their role or class

### 👨‍👩‍👧 Parent
- View linked children's profiles
- Monitor each child's attendance record
- View exam results and academic performance
- Receive announcements relevant to their children's classes

---

## Tech Stack

| Category | Technology |
|---|---|
| **Framework** | Next.js 14 (App Router) |
| **Language** | TypeScript |
| **Styling** | Tailwind CSS v4, shadcn/ui |
| **Database** | PostgreSQL |
| **ORM** | Prisma v7 |
| **Authentication** | NextAuth.js v5 |
| **Deployment** | Vercel |
| **Runtime** | Node.js, React 19 |

---

## Database Schema

13 models across 4 enums covering every aspect of school operations:

| Model | Description |
|---|---|
| `User` | Authentication entity shared by all roles (Admin, Teacher, Student, Parent) |
| `Student` | Academic profile: class assignment, roll number, DOB, gender |
| `Teacher` | Staff profile: phone, specialization, qualification, join date |
| `Parent` | Parent/guardian profile linked to one or more students |
| `ParentStudent` | Many-to-many join table linking parents to their children |
| `Class` | A class cohort: name, year, section, academic year, homeroom teacher |
| `Subject` | A taught subject assigned across classes and teachers |
| `Assignment` | Links a teacher to a subject within a class |
| `Exam` | An exam event: name, total marks, date, subject, and class |
| `Result` | A student's exam result: score, grade (A–F), pass/fail status |
| `Attendance` | Daily attendance record per student per class (Present/Absent/Late) |
| `Timetable` | Weekly schedule: class, subject, teacher, day, start/end time |
| `Announcement` | Broadcasts targeted by role (Admin/Teacher/Student/Parent) or class |

**Enums:** `Role` (ADMIN, TEACHER, STUDENT, PARENT) · `Gender` (MALE, FEMALE, OTHER) · `Grade` (A, B, C, D, F) · `AttendanceStatus` (PRESENT, ABSENT, LATE)

---

## Getting Started

### Prerequisites

- Node.js 18+
- PostgreSQL database (local or [Neon](https://neon.tech) / [Supabase](https://supabase.com))
- npm or yarn

### Installation

**1. Clone the repository**

```bash
git clone https://github.com/thaethaehsu/school-management.git
cd school-management
```

**2. Install dependencies**

```bash
npm install
```

**3. Configure environment variables**

```bash
cp .env.example .env
```

Fill in the values in `.env` (see the [Environment Variables](#environment-variables) section below).

**4. Push the database schema**

```bash
npx prisma db push
```

**5. (Optional) Seed the database**

```bash
npx prisma db seed
```

**6. Run the development server**

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Environment Variables

Create a `.env` file in the project root with the following variables:

| Variable | Description | Example |
|---|---|---|
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://user:pass@host:5432/school_db` |
| `DIRECT_URL` | Direct DB URL (required for Prisma on Vercel) | `postgresql://user:pass@host:5432/school_db` |
| `NEXTAUTH_SECRET` | Random secret for NextAuth session signing | `openssl rand -base64 32` |
| `NEXTAUTH_URL` | Canonical URL of the deployed app | `http://localhost:3000` |

**.env.example**

```env
# Database
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE"
DIRECT_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE"

# NextAuth
NEXTAUTH_SECRET="your-secret-here"
NEXTAUTH_URL="http://localhost:3000"
```

---

## Project Structure

```
school-management/
├── prisma/
│   └── schema.prisma          # Database schema (13 models)
├── public/                    # Static assets
├── src/
│   ├── app/
│   │   ├── (auth)/            # Auth routes: login, register
│   │   │   ├── login/
│   │   │   └── register/
│   │   ├── (dashboard)/       # Protected role-based dashboards
│   │   │   ├── admin/
│   │   │   ├── teacher/
│   │   │   ├── student/
│   │   │   └── parent/
│   │   ├── api/               # API route handlers
│   │   │   └── auth/
│   │   ├── globals.css
│   │   └── layout.tsx
│   ├── components/
│   │   ├── ui/                # shadcn/ui base components
│   │   ├── charts/            # Dashboard chart components
│   │   ├── forms/             # CRUD forms per entity
│   │   └── shared/            # Navbar, Sidebar, Table, etc.
│   ├── generated/
│   │   └── prisma/            # Prisma client (auto-generated)
│   ├── lib/
│   │   ├── auth.ts            # NextAuth config
│   │   ├── db.ts              # Prisma client instance
│   │   └── utils.ts           # Shared utilities
│   └── types/                 # Global TypeScript types
├── .env.example
├── next.config.ts
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

---

## Sprint Roadmap

| Sprint | Focus | Status |
|---|---|---|
| **Sprint 1** | Project setup, Prisma schema, DB connection | ✅ Complete |
| **Sprint 2** | NextAuth v5 auth, login/register, role-based routing | 🔄 In Progress |
| **Sprint 3** | Admin dashboard: student, teacher, class, subject CRUD | 📅 Planned |
| **Sprint 4** | Teacher features: attendance, exams, results, timetable | 📅 Planned |
| **Sprint 5** | Student & Parent dashboards, read-only views, announcements | 📅 Planned |
| **Sprint 6** | Analytics charts, polish, testing, Vercel deployment | 📅 Planned |

---

## Screenshots

> Screenshots will be added as features are completed.

| View | Preview |
|---|---|
| Login Page | _Coming soon_ |
| Admin Dashboard | _Coming soon_ |
| Teacher — Attendance | _Coming soon_ |
| Student — Results | _Coming soon_ |
| Parent — Child Overview | _Coming soon_ |

---

## Live Demo

> 🔗 **Live Demo:** _Coming soon — will be deployed to Vercel_

Demo credentials will be provided upon deployment:

| Role | Email | Password |
|---|---|---|
| Admin | `admin@demo.com` | `demo1234` |
| Teacher | `teacher@demo.com` | `demo1234` |
| Student | `student@demo.com` | `demo1234` |
| Parent | `parent@demo.com` | `demo1234` |

---

## Author

**Thae Thae Hsu**

- GitHub: [@thaethaehsu](https://github.com/your-username)
- LinkedIn: [linkedin.com/in/thae-thae-hsu-539b35168](https://linkedin.com/in/your-profile)
- Portfolio: [](https://your-portfolio.dev)

---

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for more information.

---

<div align="center">

Built with dedication as a full-stack capstone project · 2025

⭐ If you find this project useful, please consider giving it a star!

</div>
