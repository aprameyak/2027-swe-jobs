# CLAUDE.md — Agent Rules for this Repo

## Commits
- Never append `Co-Authored-By` to commit messages
- Never reference other job boards, repos, or external sources in commit messages
- Add each new listing as a separate commit
- Do not push without asking the user first unless they have explicitly said to push

## Data Integrity
- `listings.json` is the canonical source of truth for all listings — treat it with care
- `README.md` tables are always rebuilt from `listings.json` — never edit table rows in the README directly
- When making any bulk change (removals, reclassifications, date fixes), update `listings.json` first then rebuild all three README tables using `python3 .github/scripts/rebuild_readme.py`
- Before any destructive operation (bulk delete, reclassification, rebuild), read the current state of `listings.json` and confirm the change with the user
- Never overwrite `listings.json` or `README.md` without having read them first in the same session
- Always verify entry counts before and after bulk changes to confirm nothing was unintentionally lost
- If unsure about any change — scope, classification, data format — ask before acting

## Closed Listings (🔒)
- When a posting closes, **keep the row** — do not delete it from `listings.json`
- Set **only** `url` to `""` (empty string); `rebuild_readme.py` renders this as **🔒** in the Apply column
- **Preserve all original metadata unchanged** when marking closed — never rewrite or drop:
  - `date_added` (when the listing was first added — not the close date)
  - `company`, `role`, `location`, `type`, `season`, `education`
  - `sponsorship`, `citizenship`, and `grad_date` (if present)
- Do not add a separate “closed date” field; do not move closed rows to a different table or re-sort them by close date
- Closed listings remain in their original table (`summer`, `offcycle`, or `newgrad`) at their original sort position (by `date_added`, then company)
- The nightly link checker (`check_links.py`) marks dead URLs this way automatically; agents must not undo this by bulk-removing empty-URL rows
- **Do not hide closed listings** in the webapp or README — users rely on 🔒 to see that a role existed but is no longer accepting applications
- Only remove a closed listing entirely when the user explicitly asks to delete it, or when reclassifying/removing for scope (out-of-scope role, wrong table with no valid target)

## Adding Listings
- Use `add_listing.py` via the `ISSUE_BODY` environment variable
- Before adding, normalize the URL and check it against existing URLs in `listings.json` to avoid duplicates (UTM and tracking params are stripped; Workday board name segment is also normalized away during comparison)
- Each listing must have: `company`, `role`, `location`, `type`, `season`, `education`, `url`, `sponsorship`, `citizenship`, `date_added`
- For Workday URLs: the URL must include the board name — `tenant.instance.myworkdayjobs.com/[en-US/]BOARDNAME/job/...`. Board names for known companies are in `companies.yml`. URLs missing the board name (just `/job/...`) will 404.

## Role Scope
- In scope: software engineering, data science, ML/AI, quantitative research/trading, product management, product development, cybersecurity, DevOps/SRE, cloud engineering, mobile engineering, technical consulting, technology analyst, business analyst (tech-focused), solutions engineering, IT, and any directly adjacent technical discipline
- Out of scope: EE, ME, civil, chemical, manufacturing, process engineering, hardware, embedded/firmware, sales (non-technical), marketing, HR, legal, finance (non-quant), compliance, supply chain, logistics, warehouse, customer support
- When uncertain, err toward inclusion — the human reviewer will make the final call

## Table Classification
- **summer**: Summer 2027 internships only. No 2026 or earlier internships.
- **offcycle**: Fall/Spring/Winter internships, co-ops, and any non-Summer-2027 term. Also Summer 2026 roles still actively accepting applications.
- **newgrad**: Full-time 2027 entry-level roles. No senior/staff/director/principal/manager titles unless explicitly labeled PhD Early Career.

## Location Rules
- US and Canada only — no international listings
- Format: `City, State` or `City, Province` (e.g. `San Francisco, CA`, `Toronto, ON`)
- Multiple locations: semicolon-separated in `listings.json` (e.g. `New York, NY; Chicago, IL`)
- "Remote" is acceptable only if explicitly US or Canada remote

## Education
- Valid values: `Undergrad`, `Masters`, `PhD` — these are the only three
- Default to `Undergrad` only — do not add Masters or PhD unless the posting explicitly specifies them
- Multiple levels are semicolon-separated (e.g. `Undergrad; PhD`, `Masters; PhD`, `Undergrad; Masters; PhD`)
- Only list multiple values when the posting explicitly targets more than one level — do not infer
- A role open to "undergraduates and PhD students" → `Undergrad; PhD`
- A role open to "bachelor's or master's" → `Undergrad; Masters`
- A role open to "graduate students" (which covers both) → `Undergrad; Masters; PhD`
- A role open to "PhD and masters students" with no mention of undergrads → `Masters; PhD`
- A PhD-exclusive role → `PhD`

## Sponsorship Flags
- 🛂 appended to company name when sponsorship is explicitly not offered
- 🇺🇸 appended when US citizenship is explicitly required
- When unknown, leave as `Unknown` — do not assume

## Sorting & Grouping
- Rows are sorted **date descending** (newest `date_added` first), then **company name alphabetically** within the same date
- This sort order must be preserved on every rebuild — never sort by company alone or by any other field
- Multiple roles from the same company added on the same date are grouped: the first row uses the company name, subsequent rows use `↳` in the company column
- `↳` grouping applies only when both the company key AND the date match — same company on different dates are separate rows, not grouped
- When rebuilding tables, sort and group all entries fresh from `listings.json` using the above rules; do not rely on the existing README order
- `date_added` in `listings.json` reflects when the listing was originally added and must never be changed when reordering, reclassifying, or rebuilding tables — it is not a display date, it is a historical record

## Company Tracking Files
- `companies.md` lists every company whose ATS is actively scraped — update it whenever a company is added to or removed from `companies.yml`
- `not-covered.md` lists companies known to post CS roles but that cannot be auto-scraped — update it whenever a new company is identified as unsupported, or when a company moves to `companies.yml`
- When adding a new company to `companies.yml`, also add it to `companies.md`
- When a company cannot be scraped (unsupported ATS, disabled API, custom site), add it to `not-covered.md` with a reason
- When a company moves from `not-covered.md` to `companies.yml`, update its entry in `not-covered.md` to note the move and add it to `companies.md`
- Keep both files in alphabetical order

## Scraper
- The scraper (`scrape_jobs.py`) routes jobs by confidence: high-confidence titles are added directly to `listings.json` and `README.md`; low-confidence titles create GitHub Issues for manual review
- The workflow commits `.github/data/seen_jobs.json`, `.github/data/title_classifications.json`, `.github/data/gemini_usage.json`, `listings.json`, and `README.md`
- Low-confidence jobs and all issue-submitted jobs require manual review before being added

## Auditing
- Periodically check for: international listings, 2026 internships in the summer table, senior/staff roles in new grad, misclassified co-ops or fall internships in the summer table, and duplicate URLs
- **Closed listings (`url: ""` / 🔒) are intentional — never remove them during a cleanup pass** (see Closed Listings above)
- When roles are removed, check if they belong in a different table (e.g. a summer 2026 role may belong in offcycle) before deleting entirely

## Competitor Repos
For reference only — do not cite these in commit messages or issue bodies.

**Internships:**
- `SimplifyJobs/Summer2026-Internships` — most popular (~45k stars). Maintained daily by Pitt CS Club + Simplify; Simplify scrapes career pages hourly. Covers SWE, data science, quant, hardware, AI/ML, PM. Tables split by discipline (SWE/ML/Quant/PM/Hardware).
- `speedyapply/2027-SWE-College-Jobs` — comprehensive daily-updated list split into internships and new-grad, prioritizes postings from the last 120 days. Has a companion AI/ML jobs list.
- `zapplyjobs/Internships-2027` — newer entrant, updated frequently, includes a gamified "streaks" feature for tracking applications.
- `sndsh404/summer-2027-internships` — Summer 2027 internship list.

**New Grad:**
- `SimplifyJobs/New-Grad-Positions` — new-grad sibling of the Summer Internships repo, same maintainers and trust level.
- `vanshb03/New-Grad-2027` — maintained by WeCracked and Resumes.fyi; covers entry-level SWE, tech, CS, PM, and quant; restricted to US, Canada, or remote. Has a companion Canada-specific repo (`cvrve/New-Grad` Canada.md).
- `jobright-ai/2027-Software-Engineer-New-Grad` — ATS-scraped daily via Greenhouse, Lever, and Workday; good for catching non-FAANG enterprise tech roles early.

**Quant / Trading:**
- `pittcsc/quant-internships` and companion new-grad repo — focused purely on quantitative research, trading, and quant SWE roles; covers Citadel, Jane Street, HRT, Five Rings, etc.

**Canada:**
- `Western-Dev-Society/Canada-Tech-Internships` and `Canada-New-Grad` — essential for full North American coverage; captures Toronto, Vancouver, and Waterloo postings that US-only repos miss.
