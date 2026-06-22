# Job Applier Agent — Configuration Template

This is the configuration template for the Job Applier Agent. Copy this file to `CLAUDE.md` and fill in your personal details before using the agent.

```bash
cp CLAUDE.template.md CLAUDE.md
```

> ⚠️ `CLAUDE.md` is gitignored — your personal data stays local only.

---

## Identity & Context

- **Candidate:** [YOUR_FULL_NAME]
- **Email:** [YOUR_EMAIL]
- **Profile:** `~/job-applier-agent/data/profile.json`
- **Master Resume:** `~/job-applier-agent/resume/master_resume.md`
- **$APPLIER_HOME:** `~/job-applier-agent`

---

## Google Drive Output — NON-NEGOTIABLE

For every job processed, ALL output files must be saved to Google Drive in addition to local files.

### Folder Structure
```
Resumes/
└── Agent Applications/                          ← Google Drive folder ID: [YOUR_GDRIVE_FOLDER_ID]
    └── <CompanyName> - <Job Title>/             ← Create this subfolder per job
        ├── [INITIALS]_<CompanyName>_Resume      ← Google Doc
        ├── [INITIALS]_<CompanyName>_CoverLetter ← Google Doc
        └── JobPosting_<CompanyName>             ← Google Doc (job title, company, posting URL)
```

### File Naming Convention (EXACT)
| File | Name | Type |
|---|---|---|
| Tailored Resume | `[INITIALS]_<CompanyName>_Resume` | Google Doc |
| Cover Letter | `[INITIALS]_<CompanyName>_CoverLetter` | Google Doc |
| Job Posting Link | `JobPosting_<CompanyName>` | Google Doc |

All files must be saved as **Google Docs** (`application/vnd.google-apps.document`) — not .md, .txt, or .docx.

Use the company's short name (no spaces, no special characters) for `<CompanyName>`. Example: `[INITIALS]_Salesforce_Resume`

### Job Posting Document Format
The `JobPosting_<CompanyName>.md` file must contain:
```
# <Job Title> — <Company Name>

**Job Posting URL:** <full URL to the job posting>

**Date Found:** <today's date>

**Fit Score:** <X>/10

**Remote Confirmed:** Yes
```

### Google Drive Save Process (every job, no exceptions)
1. Create subfolder `<CompanyName> - <Job Title>` inside `Agent Applications` (folder ID: `[YOUR_GDRIVE_FOLDER_ID]`)
2. Save `[INITIALS]_<CompanyName>_Resume.md` to that subfolder
3. Save `[INITIALS]_<CompanyName>_CoverLetter.md` to that subfolder
4. Save `JobPosting_<CompanyName>.md` to that subfolder
5. Also save copies locally to `$APPLIER_HOME/applications/<CompanyName_RoleShorthand>/` as usual
6. Report the Google Drive folder link when presenting materials

---

## Job Search Rules — NON-NEGOTIABLE

### Remote Only
- **Never surface or process a job that is not explicitly remote.** If the listing says "hybrid," "on-site," "in-office," or requires relocation, skip it with no prompt.
- Acceptable: "Remote," "Fully Remote," "Work from anywhere," "100% remote"
- If location is ambiguous, check the listing body for remote confirmation before scoring.

### Target Titles Only
Only surface roles with one of these titles (or close variants) — **edit this list to match your search:**

| Approved Titles |
|---|
| Product Marketing Manager |
| Senior Product Marketing Manager |
| Director of Product Marketing |
| Marketing Manager |
| Senior Marketing Manager |
| Director of Marketing |

**Exclude automatically:**
- VP, SVP, EVP, Chief, C-Suite (too senior)
- Intern, Associate, Coordinator, Specialist (too junior)
- Roles outside your target function
- Roles requiring a security clearance
- Roles requiring relocation or in-office attendance

### Do NOT Submit Applications
The workflow is **research and prepare, not auto-submit.** The agent should:
1. Find matching jobs
2. Score and rank them
3. Tailor the resume
4. Build the cover letter
5. **STOP — present all materials for review**
6. **Never submit an application without explicit confirmation**

---

## Resume Tailoring Rules

Every tailored resume bullet must follow this formula:

> **Action Verb + What You Did + Scale or Result**

Examples of correct format:
- ✅ "Generated 2,400+ qualified leads within six weeks by architecting integrated, multi-channel campaigns across email, paid social, content, and webinars."
- ✅ "Improved conversion by 70% by redesigning lead scoring, routing, and progressive profiling."
- ❌ "Responsible for lead generation campaigns" (no verb strength, no result)
- ❌ "Helped with webinar production" (passive, no scale)

### Tailoring Process
1. **Read the JD carefully.** Extract: required skills, preferred skills, role-specific language (pipeline vs. revenue, GTM vs. launch, etc.), company context.
2. **Mirror the JD's language.** If they say "go-to-market," use "go-to-market." If they say "pipeline," use "pipeline."
3. **Reorder bullets by relevance.** Lead with the accomplishments that most directly match what the JD is asking for.
4. **Pull from the Master Accomplishments Bank** in master_resume.md for additional bullets when a JD calls for something not in the primary bullets.
5. **Never fabricate metrics, titles, dates, or skills.** Only reorder, reword using JD language, and emphasize what already exists.
6. **Bold key terms** that match the JD exactly.
7. Save tailored resume to: `$APPLIER_HOME/applications/<Company>/resume_tailored.md`

### Positioning Variants (choose based on role)

| Role Type | Use This Positioning Identity |
|---|---|
| Product Marketing Manager / Sr PMM | Core PMM Identity |
| Senior Marketing Manager | Strategic / Senior Marketing Manager Identity |
| Director of Marketing | North America / Regional Lead Identity |
| Growth / Lifecycle roles | Growth / Lifecycle / Activation Identity |
| Marketing Ops focus | Marketing Ops / Revenue Growth Identity |

Full positioning statements are in `~/job-applier-agent/resume/master_resume.md` under EXECUTIVE SUMMARY.

---

## Cover Letter Rules

- **250–350 words maximum**
- **Opening must reference something specific** about the company (product, mission, recent news, funding, customer base) — never generic
- **At least one metric** from your real experience in paragraph 2
- **Tone: confident peer, not eager applicant**
- Match JD vocabulary throughout
- Do not recite the resume — tell a story
- Save to: `$APPLIER_HOME/applications/<Company>/cover_letter.md`

### Cover Letter Voice
Write with clarity and confidence:
- Direct, not flowery
- Shows business judgment, not just task completion
- Connects marketing activity to revenue outcomes
- Does not use buzzword soup

---

## Job Search Strategy

When running `/apply-job search <query>`, use these search patterns:

```
"[YOUR_TARGET_TITLE]" remote 2026
"[YOUR_TARGET_TITLE]" remote B2B SaaS
site:linkedin.com/jobs "[YOUR_TARGET_TITLE]" remote
site:greenhouse.io "[YOUR_TARGET_TITLE]" remote
```

**Prioritize companies in:** *(edit to match your target industries)*
- B2B SaaS
- AI / ML / emerging technology
- Healthcare technology
- Enterprise software
- Marketing technology (MarTech)

**Filter out:**
- Consumer / B2C roles (if not your target)
- Roles requiring industry-specific licenses
- Agencies (unless fractional/contract role is specifically desired)
- Startups with fewer than 20 employees (unless clearly funded)

---

## Fit Scoring Adjustments

Standard fit scoring applies, with these overrides:

| Factor | Weight / Note |
|---|---|
| Remote confirmed | **REQUIRED** — score = 0 if not remote |
| Title match | Must be within target list or close variant |
| Industry match | Boost score if company is in your target industries |
| Years of experience | Level match: adjust for your seniority |

**Dealbreakers (auto-fail):**
- Not remote
- Title too senior or too junior for your target level
- Requires relocation
- Requires security clearance
- Requires industry license

---

## Workflow Output for Each Job

For each qualified job, produce:
1. **Fit Score** (0–10) with rationale
2. **ATS Keyword Analysis** — matched vs. missing
3. **Company Research Brief** (3–5 bullets: what they do, recent news, why you fit)
4. **Tailored Resume** (`resume_tailored.md`) — ready to use
5. **Cover Letter** (`cover_letter.md`) — ready to use
6. **Summary card:** Company | Role | Fit Score | ATS Score | Remote Confirmed | Apply Link

Then **pause and present everything** for review before any submission or outreach.

---

## File Naming Convention

```
$APPLIER_HOME/applications/<CompanyName_RoleShorthand>/
  ├── resume_tailored.md
  ├── cover_letter.md
  ├── research.md
  └── (interview_prep.md — generated on request)
```

Example: `applications/Acme_SrPMM/`

---

## Key Metrics to Highlight

*(Fill in your own real metrics — never fabricate)*

| Metric | Context |
|---|---|
| [X]+ leads in [timeframe] | [Campaign or initiative] |
| [X]% conversion improvement | [What you changed] |
| $[X] pipeline generated | [Launch or program] |
| [X]% traffic/engagement growth | [Channel or initiative] |
| [X] net-new accounts | [Program type] |
| [X]+ product launches owned | [Company, timeframe] |

---

## What This Agent Does NOT Do

- Does not submit applications without explicit approval
- Does not fabricate experience, metrics, dates, or titles
- Does not apply for roles that are not remote
- Does not apply for titles outside the target list
- Does not send emails or LinkedIn messages without confirmation
