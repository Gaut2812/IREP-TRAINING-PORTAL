# IREP Training Portal

**Industry-Ready Engineer Program (IREP)**\
A role-based training and learning platform for students, trainers,
colleges and parents.

> **Delivery target:** Seven-day MVP\
> **Deployment target:** Vercel (frontend) + Supabase
> (database/auth/storage)\
> **Architecture:** Next.js modular application with optional FastAPI
> services and LiveKit for live classrooms.

------------------------------------------------------------------------

## 1. Project scope

IREP brings learning, assessments, coding practice, project
collaboration, live teaching and placement-readiness tracking into one
portal.

### User roles

  -----------------------------------------------------------------------
  Role                                Main capabilities
  ----------------------------------- -----------------------------------
  Admin                               Platform configuration, users and
                                      college administration

  Student                             Courses, coding practice, tests,
                                      projects and progress

  Trainer                             Batch management, attendance,
                                      assessments and feedback

  College / Placement Cell            Branch-level progress, readiness
                                      and reports

  Parent                              Linked student's attendance and
                                      progress
  -----------------------------------------------------------------------

### Main modules

1.  Authentication and role-based access
2.  Student dashboard
3.  Trainer dashboard
4.  College / placement dashboard
5.  Parent dashboard
6.  Coding Lab and AI-assisted feedback
7.  Practice tests and assessments
8.  Virtual Labs catalogue
9.  Project Sprint Board
10. Mock interviews and feedback
11. Moderated discussion groups
12. Trainer announcements and message hub
13. Live Classroom
14. Live sessions and recordings

**MVP scope note:** Deliver the core workflows first. Virtual lab
provisioning, secure arbitrary-code execution, large-scale video
infrastructure and advanced AI processing require separate services and
should not be represented as complete until implemented and tested.

------------------------------------------------------------------------

## 2. Technology stack and version baseline

The following is the project's selected baseline. Keep exact versions in
`package-lock.json` and `requirements.txt`. Before deployment, verify
package availability and peer-dependency compatibility with the commands
in the verification section.

  --------------------------------------------------------------------------------
  Layer             Technology                Selected version / Responsibility
                                              policy             
  ----------------- ------------------------- ------------------ -----------------
  Runtime           Node.js                   24 LTS             Frontend
                                                                 tooling/runtime

  Frontend          Next.js                   16.4.6 target      App Router,
  framework                                                      routing and
                                                                 rendering

  UI library        React / React DOM         19.3.0 target; use UI rendering
                                              versions           
                                              compatible with    
                                              selected Next.js   
                                              release            

  Language          TypeScript                5.x                Type safety

  Styling           Tailwind CSS              4.x                Utility-first
                                                                 styling

  UI components     shadcn/ui                 CLI-generated      Accessible UI
                                              components; commit primitives
                                              generated source   

  Icons             Lucide React              Compatible stable  Icons
                                              release            

  Database          Supabase PostgreSQL       Supabase-managed   Persistent
                                                                 relational data

  Auth              Supabase Auth             Supabase-managed   Sign-in and
                                                                 sessions

  Authorization     PostgreSQL RLS            Supabase           Tenant and role
                                              PostgreSQL         data access

  Storage           Supabase Storage          Supabase-managed   Documents and
                                                                 media

  Realtime          Supabase Realtime         Supabase-managed   Discussion and
                                                                 live updates

  Supabase JS       `@supabase/supabase-js`   2.119.0 target     Browser/server
                                                                 SDK

  Next.js SSR       `@supabase/ssr`           Compatible stable  Cookie-based auth
  integration                                 0.x release        integration

  AI/custom API     FastAPI                   Compatible stable  Specialized
                                              release            server-side
                                                                 workflows

  Python            Python                    3.12.x             AI and custom
                                                                 backend services

  Video             LiveKit                   2.x SDK family     Live audio/video
                                                                 rooms

  Hosting           Vercel                    Managed platform   Next.js
                                                                 deployment

  Source control    GitHub                    Managed platform   Repository and CI
                                                                 workflow
  --------------------------------------------------------------------------------

### Important version policy

-   Treat the versions above as the selected project baseline, not proof
    that every package combination has already passed integration
    testing.
-   Do not independently force React versions that conflict with the
    selected Next.js release. Check Next.js peer dependencies and let
    the installer resolve compatible React packages if necessary.
-   LiveKit React Components and `livekit-client` must use compatible
    2.x releases. The exact package versions must be verified together
    before locking.
-   Supporting packages listed below should be installed at compatible
    stable versions and pinned by the generated lockfile.
-   Avoid dependency upgrades during the seven-day delivery window
    unless a security or blocking compatibility issue requires one.

------------------------------------------------------------------------

## 3. Frontend packages

### Core framework

  -----------------------------------------------------------------------
  Package                             Purpose
  ----------------------------------- -----------------------------------
  `next`                              Next.js application framework

  `react`                             Component rendering

  `react-dom`                         React DOM renderer

  `typescript`                        Static type checking

  `tailwindcss`                       Styling

  `@tailwindcss/postcss`              Tailwind CSS 4 PostCSS integration,
                                      when required by the generated
                                      setup
  -----------------------------------------------------------------------

### Supabase integration

  Package                   Purpose
  ------------------------- -------------------------------------------------
  `@supabase/supabase-js`   Supabase client
  `@supabase/ssr`           Server-side rendering and cookie-based sessions

### State, data and forms

  -----------------------------------------------------------------------
  Package                             Purpose
  ----------------------------------- -----------------------------------
  `zustand`                           Lightweight client state

  `@tanstack/react-query`             Server-state fetching, caching and
                                      mutations

  `axios`                             HTTP requests to custom APIs, if
                                      needed

  `react-hook-form`                   Form state and submission

  `zod`                               Runtime schema validation

  `@hookform/resolvers`               Connect Zod to React Hook Form
  -----------------------------------------------------------------------

### UI, charts and utilities

  Package                      Purpose
  ---------------------------- ----------------------------------
  `lucide-react`               Icons
  `recharts`                   Dashboard charts
  `framer-motion`              UI animation
  `clsx`                       Conditional class names
  `tailwind-merge`             Merge Tailwind classes
  `class-variance-authority`   Component variants
  `date-fns`                   Date formatting and calculations
  `sonner`                     Toast notifications
  `react-markdown`             Render Markdown learning content
  `react-dropzone`             File selection and upload UI

### IREP feature packages

  Package                        Module
  ------------------------------ ---------------------------------
  `@monaco-editor/react`         Coding Lab editor
  `@dnd-kit/core`                Sprint Board drag-and-drop
  `@dnd-kit/sortable`            Sortable task columns and cards
  `@dnd-kit/utilities`           Drag-and-drop utilities
  `livekit-client`               LiveKit browser client
  `@livekit/components-react`    LiveKit React UI components
  `@livekit/components-styles`   LiveKit component styles

### Development and testing

  Package                       Purpose
  ----------------------------- -------------------------------
  `supabase`                    Supabase CLI
  `vitest`                      Unit tests
  `@testing-library/react`      React component tests
  `@testing-library/jest-dom`   DOM assertions
  `@playwright/test`            Browser end-to-end tests
  `eslint`                      JavaScript/TypeScript linting

------------------------------------------------------------------------

## 4. Backend packages

FastAPI is an **optional specialized service**, not a second
implementation of every Supabase CRUD endpoint. Use it for trusted
server-side operations such as AI feedback, LiveKit token generation and
integrations that need private credentials.

  Package               Purpose
  --------------------- ----------------------------------------------
  `fastapi`             HTTP API framework
  `uvicorn[standard]`   ASGI server
  `pydantic`            Request and response validation
  `pydantic-settings`   Environment-based configuration
  `supabase`            Supabase Python SDK, where required
  `google-genai`        Gemini API integration, if selected
  `livekit-api`         Server-side LiveKit API and token generation
  `httpx`               Async HTTP client
  `python-multipart`    Multipart form uploads, if needed
  `pytest`              Backend tests
  `ruff`                Python linting and formatting

Pin exact Python package versions in a tested `requirements.txt` before
production deployment.

------------------------------------------------------------------------

## 5. Component-to-technology mapping

  -----------------------------------------------------------------------
  IREP screen / feature   Frontend components     Data / service
  ----------------------- ----------------------- -----------------------
  Login and session       Next.js forms, React    Supabase Auth
                          Hook Form, Zod          

  Student dashboard       shadcn cards, Recharts  Supabase PostgreSQL

  Coding Lab              Monaco Editor           FastAPI AI service;
                                                  isolated code runner

  Practice tests          Forms, timer UI,        Supabase; trusted
                          question palette        server-side
                                                  timing/scoring

  Virtual Labs            Lab catalogue and       Future lab orchestrator
                          status components       

  Sprint Board            DnD Kit, cards, dialogs Supabase PostgreSQL /
                                                  Realtime

  Mock Interviews         Calendar, forms, tables Supabase PostgreSQL

  Trainer dashboard       Tables, filters, charts Supabase PostgreSQL

  College dashboard       Recharts, tables        College-scoped database
                                                  queries

  Parent dashboard        Cards, charts, progress RLS-protected
                                                  linked-student records

  Discussion groups       Message list and        Supabase Realtime +
                          composer                PostgreSQL

  Trainer Message Hub     Announcements and       Supabase + server-side
                          moderation UI           authorization

  Live Classroom          LiveKit React           LiveKit server and
                          components              token API

  Recordings              Video player and        LiveKit Egress / object
                          session list            storage
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 6. LiveKit configuration

Use the LiveKit **2.x SDK family**.

Selected package targets from the project plan:

  Package                        Target
  ------------------------------ ---------------------------
  `livekit-client`               2.23.0
  `@livekit/components-react`    2.9.25
  `@livekit/components-styles`   Compatible release
  `livekit-api` (Python)         Compatible stable release

Verify package peer dependencies before pinning the final versions.

### LiveKit capabilities

-   Trainer and student audio/video
-   Screen sharing
-   Participant list and participant tiles
-   Raise-hand interaction
-   Room connection and disconnection
-   Session recording through a configured Egress workflow

Application-owned features:

-   Role checks and room access rules
-   Session scheduling
-   Attendance calculation
-   Polls and Q&A
-   Moderation and audit records
-   Parent-facing attendance summaries

Never expose the LiveKit API secret in frontend code. Generate room
tokens on a trusted server after checking the authenticated user's role
and session permissions.

------------------------------------------------------------------------

## 7. Supabase setup

Create a Supabase project and configure:

1.  PostgreSQL database
2.  Supabase Auth
3.  Row Level Security (RLS)
4.  Private Storage buckets
5.  Realtime publication for approved tables
6.  Database migrations
7.  Backup and retention settings appropriate to the project plan

### Initial database entities

-   `profiles`
-   `colleges`
-   `batches`
-   `students`
-   `trainers`
-   `parents`
-   `parent_student`
-   `courses`
-   `attendance`
-   `tests`
-   `questions`
-   `test_attempts`
-   `projects`
-   `sprint_tasks`
-   `mock_interviews`
-   `announcements`
-   `discussion_groups`
-   `messages`
-   `live_sessions`
-   `session_attendance`

Use UUID primary keys where appropriate. Add `college_id` to
college-scoped records and enforce tenant boundaries in RLS policies. A
user role stored in a profile table must not be freely editable by that
same user.

### Suggested Storage buckets

  -----------------------------------------------------------------------
  Bucket                              Access recommendation
  ----------------------------------- -----------------------------------
  `profile-images`                    Public only if profile images are
                                      intentionally public; otherwise
                                      private

  `certificates`                      Private

  `course-materials`                  Private or authenticated read

  `project-files`                     Private

  `recordings`                        Private, with session-based
                                      authorization
  -----------------------------------------------------------------------

Create Storage policies for each bucket. Do not assume that hiding a
download link in the UI protects a file.

------------------------------------------------------------------------

## 8. Installation

### Prerequisites

-   Node.js 24 LTS
-   npm
-   Python 3.12.x (only if using FastAPI)
-   Git
-   VS Code or another editor
-   Supabase account
-   GitHub account
-   Vercel account

PostgreSQL does not need to be installed locally when using Supabase
Cloud.

### Create the frontend

``` bash
npx create-next-app@16.4.6 frontend
cd frontend
```

Use the installer-generated App Router, TypeScript and Tailwind setup.
If the installer reports that a pinned release is unavailable or
incompatible, use the supported Next.js 16 release it offers and update
this README baseline.

### Install core frontend dependencies

``` bash
npm install @supabase/supabase-js@2.119.0 @supabase/ssr
npm install zustand @tanstack/react-query axios
npm install react-hook-form zod @hookform/resolvers
npm install lucide-react recharts framer-motion
npm install clsx tailwind-merge class-variance-authority
npm install date-fns sonner react-markdown react-dropzone
```

### Install IREP feature dependencies

``` bash
npm install @monaco-editor/react
npm install @dnd-kit/core @dnd-kit/sortable @dnd-kit/utilities
npm install livekit-client@2.23.0
npm install @livekit/components-react@2.9.25
npm install @livekit/components-styles
```

### Initialize shadcn/ui

``` bash
npx shadcn@latest init
```

Add the components required by the portal:

``` bash
npx shadcn@latest add button card input table dialog
npx shadcn@latest add dropdown-menu sidebar tabs badge
npx shadcn@latest add avatar calendar progress select sheet
npx shadcn@latest add alert-dialog skeleton tooltip
```

### Install development tools

``` bash
npm install -D supabase vitest @playwright/test
npm install -D @testing-library/react @testing-library/jest-dom
```

### Initialize Supabase locally

``` bash
npx supabase init
npx supabase login
npx supabase link --project-ref YOUR_PROJECT_REF
```

Create migrations:

``` bash
npx supabase migration new initial_schema
```

Apply reviewed migrations:

``` bash
npx supabase db push
```

### Optional FastAPI service

``` bash
mkdir backend
cd backend

python -m venv .venv
```

Activate on Windows:

``` powershell
.venv\Scripts\Activate.ps1
```

Install:

``` bash
pip install fastapi "uvicorn[standard]"
pip install pydantic pydantic-settings
pip install supabase google-genai livekit-api
pip install httpx python-multipart pytest ruff
```

Run locally:

``` bash
uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

------------------------------------------------------------------------

## 9. Environment variables

### Frontend: `frontend/.env.local`

``` env
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=
NEXT_PUBLIC_API_URL=
NEXT_PUBLIC_LIVEKIT_URL=
```

### Backend: `backend/.env`

``` env
SUPABASE_URL=
SUPABASE_SECRET_KEY=
GOOGLE_API_KEY=
LIVEKIT_URL=
LIVEKIT_API_KEY=
LIVEKIT_API_SECRET=
SECRET_KEY=
```

Rules:

-   Only browser-safe values may use the `NEXT_PUBLIC_` prefix.
-   Never expose Supabase secret/service-role keys, Gemini keys, LiveKit
    secrets or application signing secrets to the browser.
-   Do not commit `.env` or `.env.local`.
-   Configure production secrets in the relevant hosting provider's
    environment settings.
-   Validate required variables at application startup.

------------------------------------------------------------------------

## 10. Suggested project structure

``` text
irep-training-portal/
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   │   ├── (auth)/
│   │   │   └── (dashboard)/
│   │   │       ├── admin/
│   │   │       ├── student/
│   │   │       ├── trainer/
│   │   │       ├── college/
│   │   │       └── parent/
│   │   ├── components/
│   │   │   ├── ui/
│   │   │   ├── layout/
│   │   │   ├── dashboard/
│   │   │   └── classroom/
│   │   ├── lib/
│   │   │   └── supabase/
│   │   ├── services/
│   │   ├── hooks/
│   │   ├── stores/
│   │   ├── types/
│   │   └── utils/
│   ├── public/
│   ├── .env.local
│   └── package.json
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── core/
│   │   ├── schemas/
│   │   ├── services/
│   │   └── main.py
│   ├── tests/
│   └── requirements.txt
├── supabase/
│   ├── migrations/
│   └── seed.sql
├── docs/
├── .gitignore
└── README.md
```

------------------------------------------------------------------------

## 11. Deployment

  Component               Hosting
  ----------------------- ----------------------
  Next.js frontend        Vercel
  PostgreSQL              Supabase
  Authentication          Supabase
  Storage and Realtime    Supabase
  FastAPI (if required)   Render or equivalent
  AI API                  Gemini API
  Video infrastructure    LiveKit Cloud
  Source control          GitHub

### Vercel deployment

1.  Push the repository to GitHub.
2.  Import the repository into Vercel.
3.  Set the project Root Directory to `frontend`.
4.  Add the frontend environment variables.
5.  Deploy.
6.  Configure Supabase authentication redirect URLs with the production
    domain.
7.  Configure the backend CORS allowlist if a FastAPI service is
    deployed.
8.  Test all roles and protected data access in production.

Use Vercel Preview Deployments for review before merging changes into
the production branch.

### Build verification

``` bash
npm ls next react react-dom
npm ls @supabase/supabase-js @supabase/ssr
npm ls livekit-client @livekit/components-react
npm run build
```

Commit `package-lock.json` and use `npm ci` in reproducible
CI/deployment workflows.

------------------------------------------------------------------------

## 12. Security requirements

-   Enable RLS on every exposed application table.
-   Enforce college and user data boundaries in database policies.
-   Validate role and ownership on trusted server-side operations.
-   Use private storage buckets for sensitive records.
-   Validate uploaded file type, size and authorization.
-   Rate-limit login, assessment and AI endpoints.
-   Generate LiveKit tokens server-side only.
-   Execute untrusted student code only in a separately isolated
    execution environment.
-   Record consent and retention rules for classroom recordings.
-   Maintain audit logs for sensitive administrative actions.
-   Never commit credentials or production secrets.

------------------------------------------------------------------------

## 13. Testing

  Tool                    Testing responsibility
  ----------------------- -------------------------------
  Vitest                  Frontend unit tests
  React Testing Library   UI component tests
  Playwright              End-to-end workflows
  Pytest                  FastAPI tests
  Ruff                    Python linting and formatting

Test authentication, role permissions, parent-student access, college
isolation, attendance, test submission, file access, LiveKit room
authorization and production deployment.

------------------------------------------------------------------------

## 14. Future scalability

The initial release intentionally avoids unnecessary infrastructure. The
following components may be introduced after the MVP when measured
requirements justify them:

  Technology       Future purpose
  ---------------- ---------------------------------------
  Redis / Valkey   Caching, counters and ephemeral state
  RabbitMQ         Distributed background jobs
  Celery           Background task workers
  Kubernetes       Container orchestration
  Keycloak         Independent identity infrastructure
  OpenFGA          Relationship-based authorization
  JupyterHub       Managed notebook labs
  gVisor / Kata    Isolated code execution
  Prometheus       Metrics collection
  Grafana          Monitoring dashboards
  Loki             Centralized logs
  vLLM             Self-hosted AI inference

These are roadmap items, not dependencies of the first release.

------------------------------------------------------------------------

## 15. Seven-day delivery plan

  Day     Deliverable
  ------- --------------------------------------------------------------
  Day 1   Repository, Next.js, Supabase schema, authentication and RLS
  Day 2   Four role-based dashboards
  Day 3   Coding Lab and Practice Tests
  Day 4   Trainer and College workflows
  Day 5   Parent, Discussions and Sprint Board
  Day 6   LiveKit integration, testing and security
  Day 7   Vercel deployment and production verification

------------------------------------------------------------------------

## 16. Project status

  Item               Value
  ------------------ -----------------------------------------
  Project            IREP Training Portal
  Application type   Role-based training management platform
  Frontend           Next.js + React + TypeScript
  Backend            Supabase + optional FastAPI
  Database           PostgreSQL
  Authentication     Supabase Auth
  Authorization      PostgreSQL RLS
  Realtime           Supabase Realtime + LiveKit
  AI                 Gemini API through trusted backend
  Deployment         Vercel + Supabase

**Implementation status:** This README describes the selected
architecture and implementation plan. A listed technology or module
should only be marked complete after it has been implemented, tested and
deployed.

------------------------------------------------------------------------

## Official documentation

-   [Next.js](https://nextjs.org/docs)
-   [React](https://react.dev/)
-   [Tailwind CSS](https://tailwindcss.com/docs)
-   [shadcn/ui](https://ui.shadcn.com/docs)
-   [Supabase](https://supabase.com/docs)
-   [LiveKit](https://docs.livekit.io/)
-   [FastAPI](https://fastapi.tiangolo.com/)
-   [Vercel](https://vercel.com/docs)
-   [Playwright](https://playwright.dev/docs/intro)
