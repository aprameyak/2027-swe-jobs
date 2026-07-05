# Contributing to 2027 SWE Jobs

Thank you for helping keep this list accurate and up to date! Contributions from the community are what make this resource valuable for everyone in the 2027 recruiting class.

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Ways to Contribute](#ways-to-contribute)
- [Adding a Job Listing](#adding-a-job-listing)
- [Updating a Job Status](#updating-a-job-status)
- [Removing an Expired Listing](#removing-an-expired-listing)
- [Keeping Formatting Consistent](#keeping-formatting-consistent)
- [Submitting a Pull Request](#submitting-a-pull-request)
- [Opening an Issue](#opening-an-issue)

---

## Code of Conduct

Please be respectful. This is a community resource. Contributions that are spam, misleading, or submitted in bad faith will be rejected.

---

## Ways to Contribute

| Action | How |
|--------|-----|
| Add a new job listing | Edit the relevant markdown file and open a PR |
| Update a job status | Change the status emoji and open a PR |
| Fix a broken link | Correct the URL and open a PR |
| Remove a closed/expired listing | Delete the row and open a PR |
| Report an issue | Open a GitHub issue using the job template |
| Improve documentation | Edit README.md or CONTRIBUTING.md and open a PR |

---

## Adding a Job Listing

### Step 1: Find the right file

Choose the correct file based on the type and season of the role:

| Role Type | File |
|-----------|------|
| Summer 2027 Internship | `internships/summer-2027.md` |
| Fall 2027 Co-op | `internships/fall-2027.md` |
| Winter 2027 Co-op | `internships/winter-2027.md` |
| 2027 New Grad | `new-grad/2027.md` |

### Step 2: Format the row correctly

Each row must follow this exact format:

```markdown
| [Company Name](https://company.com/careers) | Role Title | City, State / Country | Yes / No | Yes / No / Unknown | [Apply](https://apply-link.com) | YYYY-MM-DD | 🟢 Open |
```

**Column definitions:**

| Column | Description |
|--------|-------------|
| `Company` | Company name, hyperlinked to its careers page |
| `Role` | Exact job title from the posting |
| `Location` | City, State (for US) or City, Country (international). Use `Multiple` if many locations. |
| `Remote` | `Yes`, `No`, or `Hybrid` |
| `Sponsorship` | `Yes`, `No`, or `Unknown` |
| `Apply` | Direct link to the application page |
| `Date Added` | The date you added the listing in `YYYY-MM-DD` format |
| `Status` | One of: 🟢 Open, 🟡 Rolling, 🔴 Closed |

### Step 3: Keep alphabetical order

Entries are sorted **alphabetically by company name**. Insert your row in the correct position.

### Step 4: Verify your link

Before submitting, confirm that:

- The company careers page link is valid.
- The apply link goes directly to the job posting (not just the careers homepage).
- The posting is publicly accessible (no login required to view it).

---

## Updating a Job Status

To update a job's status:

1. Find the row in the relevant file.
2. Change the emoji in the `Status` column:
   - 🟢 Open — applications are still being accepted
   - 🟡 Rolling — being reviewed on a rolling basis (often means apply soon)
   - 🔴 Closed — applications are no longer accepted
3. Open a pull request with the change.

If a job closes, do **not** remove the row immediately — set it to 🔴 Closed first so others know it existed and that it is no longer available.

---

## Removing an Expired Listing

Listings marked 🔴 Closed for more than **30 days** may be removed to keep the tables clean. To remove a listing:

1. Delete the entire row from the table.
2. In your PR description, note why it was removed (e.g., "Closed > 30 days ago").

Do **not** remove listings that are 🟡 Rolling unless you have confirmed the application window has ended.

---

## Keeping Formatting Consistent

Please follow these formatting rules to keep the tables readable and diffs clean:

- **No trailing spaces** in any line.
- **Pipes `|`** must be present at the start and end of every table row.
- **Company names** must be hyperlinked. Do not add a bare company name without a link.
- **Apply links** must use `[Apply](URL)` format, not bare URLs.
- **Dates** must be in `YYYY-MM-DD` format (e.g., `2026-08-15`), not `Aug 15` or `8/15/26`.
- **Status** must use only the three defined emoji (🟢, 🟡, 🔴). Do not use other symbols.
- **Remote** values: use `Yes`, `No`, or `Hybrid` only.
- **Sponsorship** values: use `Yes`, `No`, or `Unknown` only.

---

## Submitting a Pull Request

1. **Fork** this repository.
2. **Create a new branch** from `main`:
   ```bash
   git checkout -b add/company-name-role
   ```
3. **Make your changes** following the guidelines above.
4. **Commit** with a descriptive message:
   ```bash
   git commit -m "Add [Company] [Role] - Summer 2027"
   ```
5. **Push** your branch and open a pull request against `main`.
6. Fill out the PR template completely.

A maintainer will review your PR. Please allow a few days for a response.

---

## Opening an Issue

If you cannot submit a PR, you can open a GitHub issue using the **Add Job** template. Include as much information as possible so a maintainer can add the listing accurately.

[Open an issue here](https://github.com/aprameyakannan/2027-swe-jobs/issues/new/choose)

---

Thank you for contributing!
