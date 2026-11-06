# HireFlow — HTML / CSS / JavaScript Hackathon MVP

A polished static applicant portal and browser-only HR administration demo. Uses only HTML, CSS and vanilla JavaScript. No server, npm, build step or real authentication needed.

## Start

- For quickest local preview, open `index.html` in a browser. Local `file://` paths use `#/admin` instead of `/admin` due to browser limitations.
- For exact routes (including `/admin`), run a local HTTP static server with fallback to `index.html` for client-side routes, or deploy to Vercel/Netlify. `vercel.json` and `_redirects` are included.
- The app begins with **synthetic sample job vacancies and applicant data**. No actual company statistics are claimed.
- Admin login: go to `/admin`, choose **Demo hesabı ilə daxil ol** (or use email `admin@hireflow.local`, password `demo123`). This is intentionally NOT secure and cannot protect real candidate information.

## Public site

- Home with clear presentation, subtle CSS-3D hover/orbit visual, public demo metrics.
- Vacancy listing with title/company/criteria search and employment-type filter.
- Vacancy detail with requirements, application form, required CV PDF/DOCX/TXT, optional certificate, applicant skills, motivation, GitHub/LinkedIn links only when requested by HR.
- About: project positioning and clearly labeled sample HR team profiles.
- FAQ controlled from admin.
- Contact form stored locally; email address displayed as hireflow.ai@gmail.com.
- Responsive typography, mobile navigation, semantic elements, motion reduction preference.

## Admin

- Demo login, dashboard, activity log.
- Create/edit vacancies; add/remove criteria and comma-separated aliases, mark required/optional, switch active/inactive, configure optional GitHub/LinkedIn fields.
- Vacancy-level views, total applications, interview statuses.
- Upload up to 100 PDF/DOCX/TXT CVs per batch in the vacancy application admin view; filename-based placeholder fields need manual review. Generate 100 clearly synthetic applicants for demo testing.
- Candidate list grouped by **full**, **partial**, **no confirmed criteria**. Each criterion is backed by matched string evidence. Unmatched criteria are **unknown**, not confirmed failures.
- Candidate detail includes application details, optional retained small file attachments, extracted CV text, heuristic criterion check, manual status and email drafting.
- Interview invite draft can include proposed time and place, HR sender identity, and applicant address. Clicking "E-poçt tətbiqində aç" triggers `mailto:`. **The app cannot send a message from the entered HR address**; mailto uses the user's configured email application. Manually mark messages as recorded only after actual sending.
- Candidate reply input appends supplemental information and re-runs local criterion checks.
- Contact inbox with mailto reply, manual answered status.
- FAQ CRUD and CSV applicant export.

## CV parsing / storage

- TXT uses browser-native decoding.
- PDF uses PDF.js 3.11.174 from cdnjs, dynamically loaded.
- DOCX uses Mammoth 1.9.1 from jsDelivr, dynamically loaded.
- Requires internet for PDF/DOCX libraries; image-only scanned PDF has no OCR; if extraction fails the application can still be submitted with manually entered skills/motivation. Extraction failure is announced.
- Files <= 250 KB are optionally retained as data URLs; larger files keep metadata/text only to reduce localStorage quota usage.
- Files over 4 MB (CV) / 1 MB (certificate) rejected.
- localStorage is per browser origin/device and has limited quota. No synchronization, no access-control isolation; do NOT enter real personal/HR information.

## What it does NOT do

- Real AI/LLM analysis. The rule-based matching simply searches candidate-supplied fields and extracted text for literal criterion names/keywords. It does not infer capabilities, validate certificates or make hiring decisions. Missing a keyword is `unknown`, never proof of incompetence.
- Real email sending, SMTP, inbox synchronization, true role separation, secure login, server database, server-side audit or production privacy safeguards.
- Real 3D mesh/WebGL model. 3D-like animation and hover are CSS-only and deliberately lightweight.

## Production roadmap

Replace localStorage with a permissioned backend, implement secure authentication, file upload and malware scanning, consent/retention workflow, actual text extraction and OCR, structured model-assisted extraction with source citations and manual review, and email provider integration with authenticated sender identity. Do not expose any API credentials in static frontend source.

## Files

- `index.html` — app document and SEO metadata
- `styles.css` — responsive design and animations
- `script.js` — state, app routes, forms, rules and UI
- Brend bütün səhifələrdə yalnız yazı olaraq göstərilir; PNG loqolar çıxarılıb.
- `vercel.json` / `_redirects` — path fallback for Vercel/Netlify


## GitHub Pages marşrut düzəlişi
- `https://es001-es.github.io/HireFlow/` layihənin ana səhifəsini birbaşa açır.
- Naviqasiya keçidləri cari `script.js` ünvanından layihənin baza yolunu tapır.
- GitHub Pages-də `/HireFlow/admin` kimi daxili ünvan birbaşa açılanda `404.html` onu `/#/admin` formasına yönləndirir; normal menyu linkləri əvvəlki kimi qalır.
- Lokal fayl rejimi `#/admin` marşrutunu dəstəkləyir.
- Köhnə PNG loqoları çıxarılıb, brend sadəcə `HireFlow` mətnindən ibarətdir.

**Qeyd:** GitHub Pages-də server backend olmadığından `localStorage` bütün cihazlarda paylaşılmır.
