# Clinic Queue

A live patient-queue and prescription-prep web app, originally built for a family member's clinic that runs till 3 AM.

An attendant enters vitals and vision data on a phone. The doctor sees the live queue on a computer and **copies pre-formatted tables straight into his existing Word prescription template**, with the original table format preserved.

**Live demo:** <demo-url> (no login, synthetic data only)

> **About this repo.** The production app runs at the clinic on Firebase (Auth, Firestore, Hosting) with access restricted to authorised staff, because it holds patient data. This public demo is the same UI and logic with the backend swapped for in-browser `localStorage`, so it needs no login and contains no patient data. Open the Doctor tab in a second browser tab to see the queue sync live.

## Features

- Adult and child intake, with auto-calculated BMI, ideal weight, mid-parental height, and age from DOB (years, months, days)
- Queue the attendant can reorder; the doctor can call any patient; emergency patients jump the queue
- Abnormal values flagged in red: BMI (adults <18.5 or ≥25; children against IAP 2015 BMI-for-age) and vision worse than 6/6
- Word-ready tables (Header, Vitals, Vision) copied as HTML so Word keeps the exact layout
- Permanent, searchable, dated history with view, re-add and delete
- The clinic day rolls over at 6 AM so late-night patients stay in the same queue

## Stack

Vanilla JS single page. Production: Firebase Auth, Firestore (real-time listeners and transactions), Hosting. Demo: `localStorage`.

## Key decisions

- **Paste into Word instead of generating prescriptions in-app.** I rejected an in-app prescription/PDF generator because the doctor's Word template is his workflow, and a new tool at 2 AM with patients waiting would not get used. The cost was handling clipboard HTML and exact table widths myself.
- **Firestore transactions for the queue (production).** Phone and computer edit the same queue, so each change is a transaction to avoid lost updates and duplicate tokens.
- **Firebase over a custom backend.** Real-time sync and auth without running servers for a one-clinic deployment.

## Run it

Open `index.html` in a browser, or host it on GitHub Pages.

_Production built: [Sept 2026]. Public demo prepared: Oct 2026._
