# Contributing to 2027 SWE Jobs

Thank you for helping keep this list accurate and up to date!

---

## Ways to Contribute

| Action | How |
|--------|-----|
| Add a new job listing | Submit an issue or open a pull request |
| Update an application status | Open a PR marking the role 🔒 |
| Fix a broken link | Open a PR with the corrected URL |
| Remove a closed/expired listing | Open a PR deleting the row |

---

## Adding a Job Listing

### Step 1: Find the right file

| Role Type | File |
|-----------|------|
| Summer 2027 Internship | `internships/summer-2027.md` |
| Fall 2027 Co-op | `internships/fall-2027.md` |
| Winter 2027 Co-op | `internships/winter-2027.md` |
| 2027 New Grad | `new-grad/2027.md` |

### Step 2: Format the row

Each row must follow this exact format:

```markdown
| Company Name | Role Title | City, State | <a href="APPLY_URL"><img src="https://i.imgur.com/u1KNU8z.png" width="118" alt="Apply"></a> | Mon DD |
```

**Column definitions:**

| Column | Description |
|--------|-------------|
| `Company` | Plain company name — **no hyperlink** |
| `Role` | Exact job title from the posting. Append 🛂 if no sponsorship, 🇺🇸 if US citizenship required. |
| `Location` | City, State (US) or City, Country. Multiple locations: `City1</br>City2`. Many locations: use `<details>` block. |
| `Application/Link` | HTML image-link button (see format above). Use 🔒 when closed. |
| `Date Posted` | `Mon DD` format, e.g. `Jul 5` |

**Multiple roles at the same company** — use `↳` in the Company column:

```markdown
| Acme Corp | Software Engineer Intern | San Francisco, CA | <a href="URL1"><img src="https://i.imgur.com/u1KNU8z.png" width="118" alt="Apply"></a> | Jul 5 |
| ↳ | Backend Engineer Intern | New York, NY | <a href="URL2"><img src="https://i.imgur.com/u1KNU8z.png" width="118" alt="Apply"></a> | Jul 5 |
```

**Many locations** — use a `<details>` block:

```markdown
| Acme Corp | Software Engineer Intern | <details><summary>**3 locations**</summary>San Francisco, CA</br>New York, NY</br>Seattle, WA</details> | <a href="URL"><img src="https://i.imgur.com/u1KNU8z.png" width="118" alt="Apply"></a> | Jul 5 |
```

**Marking a role as closed:**

```markdown
| Acme Corp | Software Engineer Intern | San Francisco, CA | 🔒 | Jul 5 |
```

### Step 3: Insert in alphabetical order

Entries are sorted **alphabetically by company name**. The only exception is `↳` rows, which always immediately follow their parent company row.

### Step 4: Verify your link

- The apply link goes directly to the job posting, not just the careers homepage.
- The posting is publicly accessible (no login required to view it).

---

## Scope

This repository is **exclusively for roles in the United States, Canada, or Remote** positions. International-only roles (outside US/Canada) will not be merged.

---

## Submitting a Pull Request

1. **Fork** this repository.
2. **Create a branch** from `main`:
   ```bash
   git checkout -b add/company-name-role
   ```
3. **Make your changes** following the guidelines above.
4. **Commit** with a descriptive message:
   ```bash
   git commit -m "Add [Company] [Role] - Summer 2027"
   ```
5. **Open a pull request** against `main` and fill out the PR template.

---

## Opening an Issue

If you prefer not to submit a PR, [open an issue](https://github.com/aprameyak/2027-swe-jobs/issues/new/choose) using the Add Job template and a maintainer will add the listing.

---

Thank you for contributing!
