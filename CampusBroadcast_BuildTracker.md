# 📋 Campus Broadcast — Project Build Tracker

**Last Updated:** June 8, 2026 **Status:** Pre-Development — Environment Setup Phase **Developer Experience Level:** Intermediate **Teaching Mode:** Active — learning as we build

---

## 🧭 How To Use This Document

Each time you return to a new Claude session, paste this document in and say:

*"I am a full stack developer in teaching mode. Here is my project build tracker. Pick up where we left off."* Claude will read the current phase, completed steps, and decisions made — and continue without losing context.

---

## 🏗️ Project Overview

**App Name (working title):** Campus Broadcast **Type:** Admin-only PWA (Progressive Web App) — mobile-first, installable, cross-platform **Purpose:** Allow admins to create events and broadcast them simultaneously to SMS, Email, and GroupMe across multiple team "campuses"

### What It Is

A multi-tenant broadcast notification system with an admin CMS. Admins input event data once; the system formats and delivers it across all three communication channels.

### Who Uses It

- **Admins only** — no public-facing UI  
- Each "campus" is an isolated team with its own admins, members, and events  
- Initial test team: \~45 members, expandable to multiple campuses

---

## ✅ Confirmed Feature List

### 🔐 Admin Panel

- [ ] Admin login / authentication (per campus)  
- [ ] Campus creation and management  
- [ ] Dashboard overview

### 👥 Member Management

- [ ] Manual add / remove members  
- [ ] Bulk import via Google Sheets (.xlsx / .csv upload)  
- [ ] QR code → self-registration form (members fill out their own info)  
- [ ] Per-member contact preference: SMS, Email, or GroupMe  
- [ ] *(Phase 2\)* Titles with icons (Campus Chief, Team Lead, Former Officer, Active Officer, etc.)

### 📅 Event Creation (GroupMe-style format)

- [ ] Title  
- [ ] Banner / photo upload  
- [ ] Start date & time  
- [ ] End date & time  
- [ ] Location search → auto-generates Google Maps link  
- [ ] Description / body text  
- [ ] RSVP / sign-up link  
- [ ] Broadcast targets (SMS, Email, GroupMe — all or select)

### 📣 Broadcast Engine

- [ ] Push to GroupMe (post into existing group OR create new group from app)  
- [ ] Push to SMS via Twilio  
- [ ] Push to Email via Resend  
- [ ] All three fire from single event submission

### 👁️ Watch List *(Phase 3\)*

- [ ] Add person with photo \+ details  
- [ ] Broadcast watch list entry to team across all channels

### 📱 PWA / Technical

- [ ] Installable on iOS, Android, Desktop (no App Store needed)  
- [ ] Mobile-first responsive design  
- [ ] Works offline (cached views)  
- [ ] Cross-browser compatible (Chrome, Safari, Firefox)  
- [ ] Git version control (GitHub)  
- [ ] Professional branching strategy (main / dev / feature branches)

---

## 🏆 Confirmed Tech Stack

| Layer | Technology | Purpose | Cost |
| :---- | :---- | :---- | :---- |
| Framework | Next.js 14+ (App Router) | Frontend \+ Backend API routes | Free |
| Language | TypeScript | Type safety, industry standard | Free |
| Styling | Tailwind CSS | Mobile-first utility CSS | Free |
| Database | PostgreSQL via Supabase | Relational, multi-tenant ready | Free tier |
| Auth | Supabase Auth | Admin login, per-campus roles | Free tier |
| File Storage | Supabase Storage | Event photos, watch list photos | Free tier |
| ORM | Prisma | Database interface layer | Free |
| SMS | Twilio | Send text messages | \~$0.0079/msg |
| Email | Resend | Send emails | Free up to 3k/mo |
| GroupMe | GroupMe Bot API | Post into GroupMe groups | Free |
| Sheet Import | SheetJS (xlsx) | Parse .xlsx/.csv uploads | Free |
| QR Codes | qrcode.react | Generate registration QR codes | Free |
| Maps | Google Places API | Location search \+ maps links | Free tier |
| PWA | next-pwa | Service worker, installability | Free |
| Version Control | Git \+ GitHub | Source control | Free |
| Deployment | Vercel | Hosting (built for Next.js) | Free tier |

💡 **Estimated monthly cost at 45 users:** Near $0. Twilio SMS will be the only real cost — pennies per broadcast.

---

## 🗄️ Database Schema (Planned)

Campus

  ├── id, name, createdAt

  ├── → Admins (users)

  ├── → Members

  ├── → Events

  └── → GroupMe Bot Token

Member

  ├── id, name, phone, email

  ├── preferredChannel (SMS | EMAIL | GROUPME)

  ├── campusId (foreign key)

  └── title (Phase 2: Campus Chief, Team Lead, etc.)

Event

  ├── id, title, bannerImageUrl

  ├── description

  ├── startTime, endTime

  ├── location (text), mapsLink (generated)

  ├── rsvpLink

  ├── campusId (foreign key)

  └── broadcastTargets (SMS | EMAIL | GROUPME)

WatchListEntry (Phase 3\)

  ├── id, name, photoUrl, details

  └── campusId (foreign key)

---

## 🗂️ Git Branching Strategy

main          → Production (live app — never commit directly)

dev           → Staging (tested, ready to merge to main)

feature/xxx   → New features (branch from dev, PR back to dev)

hotfix/xxx    → Emergency fixes (branch from main)

---

## 🚦 Build Phases & Progress

### PHASE 0 — Environment Setup

**Status: 🔲 NOT STARTED**

- [ ] Accounts created:  
      - [ ] GitHub (github.com)  
      - [ ] Supabase (supabase.com)  
      - [ ] Vercel (vercel.com)  
      - [ ] Twilio (twilio.com)  
      - [ ] Resend (resend.com)  
      - [ ] GroupMe Developer (dev.groupme.com)  
      - [ ] Google Cloud Console (console.cloud.google.com)  
- [ ] Local environment ready:  
      - [ ] Node.js installed (`node -v` in terminal)  
      - [ ] Git installed (`git --version` in terminal)  
      - [ ] VS Code installed  
- [ ] GitHub repo created  
- [ ] Next.js project scaffolded  
- [ ] First commit pushed to GitHub

---

### PHASE 1 — Foundation

**Status: 🔲 NOT STARTED** *Depends on: Phase 0 complete*

- [ ] Next.js 14 \+ TypeScript project initialized  
- [ ] Tailwind CSS configured  
- [ ] next-pwa installed and configured  
- [ ] manifest.json created (app name, icons, theme)  
- [ ] Supabase project created \+ connected  
- [ ] Prisma ORM installed and schema defined  
- [ ] Database tables created (Campus, Member, Event)  
- [ ] Supabase Auth configured (admin email/password login)  
- [ ] Login page built  
- [ ] Protected routes (redirect to login if not authenticated)  
- [ ] Campus creation form  
- [ ] Basic admin dashboard layout (mobile-first)

---

### PHASE 2 — Member Management

**Status: 🔲 NOT STARTED** *Depends on: Phase 1 complete*

- [ ] Member list view (per campus)  
- [ ] Manual add member form (name, phone, email, preferred channel)  
- [ ] Delete member  
- [ ] Google Sheets / CSV bulk import (SheetJS)  
- [ ] QR code generation for self-registration  
- [ ] Self-registration form (public, minimal — name, phone, email, preference)

---

### PHASE 3 — Events & Broadcast

**Status: 🔲 NOT STARTED** *Depends on: Phase 2 complete*

- [ ] Event creation form (full GroupMe-style fields)  
- [ ] Google Places API location search integration  
- [ ] Photo/banner upload to Supabase Storage  
- [ ] GroupMe Bot setup flow (connect existing group OR create new)  
- [ ] GroupMe broadcast (post event to group)  
- [ ] Twilio SMS broadcast (send to all SMS-preference members)  
- [ ] Resend Email broadcast (send to all Email-preference members)  
- [ ] Broadcast confirmation screen  
- [ ] Event history / log view

---

### PHASE 4 — Polish & PWA

**Status: 🔲 NOT STARTED** *Depends on: Phase 3 complete*

- [ ] Full mobile-first UI polish  
- [ ] PWA install prompt (iOS \+ Android)  
- [ ] Offline support (cached dashboard)  
- [ ] Multi-campus isolation confirmed and tested  
- [ ] Error handling \+ loading states throughout  
- [ ] Deploy to Vercel (production)  
- [ ] Custom domain (optional)

---

### PHASE 5 — Titles & Icons *(Future)*

**Status: 🔲 FUTURE**

- [ ] Title system (Campus Chief, Team Lead, Former Officer, Active Officer, etc.)  
- [ ] Icon set per title  
- [ ] Assign titles to members  
- [ ] Display in member list \+ broadcast messages

---

### PHASE 6 — Watch List *(Future)*

**Status: 🔲 FUTURE**

- [ ] Watch list entry form (name, photo, details)  
- [ ] Photo upload  
- [ ] Broadcast watch list entry to all channels  
- [ ] Watch list history view

---

## 📝 Session Notes

### Session 1 — June 8, 2026

- Defined full project scope and feature list  
- Confirmed multi-tenant "campus" architecture  
- Confirmed PWA \+ mobile-first approach  
- Confirmed Git \+ GitHub version control workflow  
- Finalized tech stack (Next.js, TypeScript, Tailwind, Supabase, Prisma, Twilio, Resend, GroupMe Bot API)  
- Confirmed build phases 0–6  
- **Next step:** Complete Phase 0 checklist (accounts \+ local environment)

---

## 🔑 Key Decisions Made

| Decision | Choice | Reason |
| :---- | :---- | :---- |
| Framework | Next.js 14 | Industry standard, API routes built in, Vercel optimized |
| Language | TypeScript | Catches errors early, industry standard |
| Styling | Tailwind CSS | Mobile-first, fastest for admin UIs |
| Database host | Supabase | Free tier, includes Auth \+ Storage, PostgreSQL |
| App type | PWA | Cross-platform, no App Store needed, mobile-forward |
| SMS provider | Twilio | Industry standard |
| Email provider | Resend | Modern, generous free tier |
| Deployment | Vercel | Built for Next.js, seamless CI/CD with GitHub |

---

*This document is your source of truth. Update the checkboxes as items are completed and add session notes each time you work on the project.*  
