# Job Application Tracker — Requirements Document

## 1. Purpose
A web application that lets a job seeker track applications through their
lifecycle (Applied → Interviewing → Offer / Rejected), attach notes to each
application, and view basic stats on their search. Built as a full-stack
portfolio project demonstrating both React and Angular frontends against a
shared NestJS + PostgreSQL backend.

## 2. Actors
- **Authenticated User** — the only actor. No admin role, no multi-tenant
  orgs. Keeping this single-actor is a deliberate scope decision, not an
  oversight — it keeps the auth and authorization logic simple enough to
  finish in the project timeline while still being real (not mocked).

## 3. Functional Requirements

| ID | Requirement |
|----|-------------|
| FR1 | A user can register with email + password |
| FR2 | A user can log in and receive a session (JWT) |
| FR3 | A user can create, view, edit, and delete a job application |
| FR4 | A user can change an application's status (Applied / Interviewing / Offer / Rejected) |
| FR5 | A user can add notes to an application |
| FR6 | A user can view a dashboard of applications grouped by status (kanban-style) |
| FR7 | A user can see basic stats (total applications, response rate, offer rate) |

## 4. Non-Functional Requirements

| ID | Requirement |
|----|-------------|
| NFR1 | API responses under 300ms for standard CRUD operations |
| NFR2 | Passwords stored hashed (bcrypt/argon2), never in plaintext |
| NFR3 | Frontend must be responsive (mobile + desktop) |
| NFR4 | Core user flows covered by automated tests (backend + frontend) |
| NFR5 | Application must be deployable via CI/CD, zero manual server steps |

## 5. Out of Scope (v1)
- Admin roles, multi-tenant organizations
- OAuth / social login
- Reminders / scheduled notifications
- Email verification on signup

## 6. Future Enhancements (fast-follow, not v1)
- **Password reset flow** — deferred deliberately. Once core auth (FR1/FR2)
  is working, this is a small, self-contained addition: a reset-token model
  plus one email-sending step. Good candidate for a "v1.1" commit after the
  core project is deployed, to show iterative development in the commit
  history rather than doing everything in one pass.

## 7. Status Model Decision
Status is modeled as a fixed enum (`APPLIED`, `INTERVIEWING`, `OFFER`,
`REJECTED`) rather than a user-configurable table. This was a deliberate
scope trade-off: a dynamic status table is more "realistic SaaS," but for
this project's timeline, the enum lets time be spent on things with more
hiring signal — testing, architecture, deployment — instead of an
over-engineered feature nobody asked for.
