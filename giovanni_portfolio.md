# Giovanni Marcondes — Project Portfolio

**CSU · Fort Collins, CO**

A collection of academic and applied projects spanning AI, data engineering, and product design.

---

## MarcDown AI — Interview Assistant

**BUS 479 · AI Intern Project · 2026**

A production-oriented macOS desktop application that sits alongside a recruiter during live interviews — capturing audio, generating real-time summaries, suggesting ranked follow-up questions, and scoring candidates out of 100.

**Stack:** Tauri v2 + Rust · React + TypeScript · Claude API · macOS Keychain · Local-first · No remote storage

### Core features

#### Real-time transcription

Captures recruiter mic and system audio (works on speaker calls too), producing a single mixed transcript with no raw audio stored by default.

#### Live structured summary

Left pane continuously updates with Question, Key Answer, and Follow-up Needed sections. Editable by the recruiter mid-session with a one-click copy button.

#### Research engine

Right pane surfaces condensed web research on entities mentioned (companies, technologies, projects). Each insight is labeled: Transcript Fact, Inference, or External Research.

#### Fit scoring (out of 100)

End-of-session debrief with a weighted overall score and subscores across Skills Match, Experience Depth, Domain Fit, Communication Clarity, Ownership, and Risk/Credibility.

### Session flow

1. **Setup** — Upload job files, paste job description, add recruiter priorities, review and edit the AI-generated scoring rubric.
2. **Consent check** — Compliance warning displayed before any audio capture begins — recruiter accepts legal responsibility.
3. **Live session** — Two-pane view: summary left, research insights right. Research can be paused independently from transcription.
4. **Debrief** — Score report, strengths & concerns, recommendation, and optional PDF/DOCX export. Data only persists if recruiter clicks Save.

### Bias & compliance rules

#### Protected attributes excluded

Hard-coded rule prevents inference or scoring based on age, ethnicity, religion, disability, health, family status, nationality, or accent-based traits.

#### Security-first architecture

Secrets in macOS Keychain, encrypted local storage, strict Tauri IPC boundary, no raw audio ever sent to the internet, no hidden telemetry.

#### Auditable scoring

Every subscore links back to transcript-derived evidence or external research. Low-confidence items are clearly flagged and never presented as facts.

### Technology stack

`Tauri v2` · `Rust` · `React 18` · `TypeScript` · `Anthropic Claude API` · `macOS Keychain` · `AES-256 local encryption` · `Web Search tool` · `PDF/DOCX export` · `Content Security Policy`

### Reflection

> This was definitely one of the most ambitious tasks I have ever done with AI. I wasn't asking for a simple output or a single HTML file. Managing this AI Agent has been very difficult, and the more I stress-test it, the more problems I find. There is no one answer anymore.
>
> — Giovanni Marcondes, BUS 479 Reflection

---

## DRAGON — SDoH Outreach

**CIS 355 · Snowflake / AI · Fall 2025**

A full end-to-end data pipeline on Snowflake that identifies and prioritizes individuals with high stress and low wellness for targeted mental-health outreach — using Social Determinants of Health (SDoH) lifestyle indicators and AI-generated notes.

**Stack:** Snowflake · Snowpark Python · Streamlit · AI_COMPLETE (LLM) · AnalyticsIQ SDoH Dataset

### Key stats

| Metric | Value |
|--------|--------|
| Individuals in dataset | 1,000 |
| High-priority targets (gap ≥ 2) | 22.9% |
| AI-generated outreach notes | 200 |
| HIGH priority classifications | 122 |

### Pipeline overview

1. **EDA** — Missingness checks, correlation analysis between stress, wellness, exercise, and job satisfaction.
2. **Metrics view** — Created `WELLNESS_FACTOR` view — rescaled scores to 1–7 and computed `stress_minus_wellness_7` gap metric.
3. **Semi-structured** — Built household JSON table using `ARRAY_AGG` and `LATERAL FLATTEN` for household-level risk signals.
4. **AI notes** — Used Snowflake `AI_COMPLETE` to generate triage-based outreach notes with priority labels extracted via regex.
5. **Streamlit app** — Interactive dashboard with priority filter, gap/stress sliders, segment explorer, household lens, and CSV export.

### What the app does

#### Executive summary

Live KPIs (people filtered, avg stress, avg wellness, avg gap), gap distribution bar chart, and AI priority distribution — all updating in real time with sidebar filters.

#### Segment explorer

Group by exercise level, job satisfaction, or ethnicity to identify which demographic segments have the highest average stress-minus-wellness gap.

#### Household lens

Drills into `members_json` VARIANT arrays to surface household-level prioritization using semi-structured SQL.

#### Outreach notes

Full-text search across AI-generated notes. Filter by priority label (HIGH / MEDIUM), matching targeting filters. One-click CSV download for outreach teams.

### Technology stack

`Snowflake SQL` · `Snowpark Python` · `Streamlit in Snowflake` · `AI_COMPLETE (LLM)` · `OBJECT_CONSTRUCT` · `LATERAL FLATTEN` · `ARRAY_AGG` · `Regex label extraction` · `CSV export`

### Business question answered

> How can we identify and prioritize individuals with high stress and low wellness who are most likely to benefit from targeted mental-health outreach using SDoH lifestyle indicators? This enables actionable segmentation for outreach programs (teletherapy/coaching) rather than reporting a single descriptive statistic.
>
> — DRAGON Project Report, CIS 355

---

## Revamping the CSU Rec App

**CIS 360 · UX / Systems Design · 2025**

A full UI/UX redesign and system requirements specification for the Colorado State University Recreation Center mobile app — transforming a cluttered icon-grid into a clean, student-centered experience with persistent QR login, live facility counts, and streamlined class booking.

**Stack:** React Native · Node.js backend · CSU SSO + Duo 2FA · Canva (UI mockups) · Team of 6

### Problems with the current app

| Severity | Issue |
|----------|--------|
| **High** | **Barcode display failures** — 60% of Rec staff reported barcode not displaying. Users forced to re-generate a new QR code every single visit. |
| **High** | **No persistent login** — 70% of staff handled sign-in complaints. Users must re-authenticate from scratch every time they open the app. |
| **Med** | **Cluttered homepage** — 20 equally-sized icon tiles on the home screen with no hierarchy. Users struggle to find barcode access and event booking. |
| **Med** | **Inefficient booking system** — Event sign-up is cumbersome and confusing. Staff receive frequent calls and in-person visits asking about schedules. |
| **Low** | **Limited push notifications** — Users miss class cancellations, waitlist updates, and event openings due to untimely or irrelevant alerts. |

### New design — screen mockups (conceptual)

**Home (REC CENTER)**

- Today's Hours — Main Gym: 6 AM – 11:30 PM  
- Next Activity — Zumba \| 12:00 – 1:00 PM  
- Digital ID — Check-In QR Code  
- Nav: Home · Classes · Facilities · Profile  

**Schedule (GROUP CLASSES)**

- April 2025 · Reserve  
- Ride Fusion — 7:30 – 8:30 AM  
- Mat Pilates — 10:15 – 11:15 AM  

**Facilities**

- Live Occupancy — Sauna 40%, Weight Rm 75%  
- Live Cams — Main Gym, 1st Floor Weight  

**Login**

- School email / NetID password fields  
- Remember Login  
- Sign In with CSU SSO  

### New features delivered

#### Persistent QR code

One permanent QR code per student that doesn't regenerate on every visit. Resolves the #1 pain point reported by both staff and members.

#### Simplified navigation

Replaced 20-icon grid with 4 clear tabs: Home, Classes, Facilities, Profile. Search bar provides discoverability without clutter.

#### Smart notifications

Customizable alerts for class cancellations, waitlist changes, and intramural season opens — without overwhelming users.

#### Live occupancy

Gym traffic data (already collected and posted to the website) surfaced directly in the app. Facility counts visible side-by-side with live camera feeds.

### System requirements (SRS)

#### Performance

App launch ≤ 5 sec. Login with saved credentials ≤ 5 sec. System handles 1,000 concurrent users. Background sync must not affect battery.

#### Security

CSU SSO + Duo 2FA integration. Role-based permissions (admin/student/staff). Encrypted stored credentials. Password field masking with reveal toggle.

#### Design constraints

iOS and Android compatible. React Native shared codebase. Max 80 MB storage footprint. Must support one-handed use. Screen reader accessible.

#### Reliability

Max 1 crash per 10,000 sessions. 99.9% uptime during rec hours (6 AM – 11:30 PM). Failed syncs auto-retry. Bookings confirmed even on poor connections.

### Technology stack

`React Native` · `Node.js` · `CSU SSO` · `Duo 2FA` · `Firebase Cloud Messaging` · `Apple Push Notification Service` · `GitHub` · `Canva (mockups)` · `JSON API`
