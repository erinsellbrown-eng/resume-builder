# Job Applier Agent — Erin Brown Configuration

This agent is configured for **Erin Brown**, a Senior Marketing Manager / Product Marketing leader with 15 years of B2B SaaS experience. All behavior below overrides the defaults in SKILL.md where they conflict.

---

## Identity & Context

- **Candidate:** Erin Brown
- **Email:** erin.sell.brown@gmail.com
- **Profile:** `~/job-applier-agent/data/profile.json`
- **Master Resume:** `~/job-applier-agent/resume/master_resume.md`
- **$APPLIER_HOME:** `~/job-applier-agent`

---

## Google Drive Output — NON-NEGOTIABLE

For every job processed, ALL output files must be saved to Google Drive in addition to local files.

### Folder Structure
```
Resumes/
└── Agent Applications/                          ← Google Drive folder ID: 1Qc85sYy73paOlDt-NgJNgl13hxU9VS5e
    └── <CompanyName> - <Job Title>/             ← Create this subfolder per job
        ├── EBrown_<CompanyName>_Resume         ← Google Doc
        ├── EBrown_<CompanyName>_CoverLetter    ← Google Doc
        └── JobPosting_<CompanyName>            ← Google Doc (job title, company, posting URL)
```

### File Naming Convention (EXACT)
| File | Name | Type |
|---|---|---|
| Tailored Resume | `EBrown_<CompanyName>_Resume` | Google Doc |
| Cover Letter | `EBrown_<CompanyName>_CoverLetter` | Google Doc |
| Job Posting Link | `JobPosting_<CompanyName>` | Google Doc |

All files must be saved as **Google Docs** (`application/vnd.google-apps.document`) — not .md, .txt, or .docx.

Use the company's short name (no spaces, no special characters) for `<CompanyName>`. Example: `EBrown_Salesforce_Resume`

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
1. Create subfolder `<CompanyName> - <Job Title>` inside `Agent Applications` (folder ID: `1Qc85sYy73paOlDt-NgJNgl13hxU9VS5e`)
2. Save `EBrown_<CompanyName>_Resume.md` to that subfolder
3. Save `EBrown_<CompanyName>_CoverLetter.md` to that subfolder
4. Save `JobPosting_<CompanyName>.md` to that subfolder
5. Also save copies locally to `$APPLIER_HOME/applications/<CompanyName_RoleShorthand>/` as usual
6. Report the Google Drive folder link to Erin when presenting materials

---

## Job Search Rules — NON-NEGOTIABLE

### Remote Only
- **Never surface or process a job that is not explicitly remote.** If the listing says "hybrid," "on-site," "in-office," or requires relocation, skip it with no prompt.
- Acceptable: "Remote," "Fully Remote," "Work from anywhere," "100% remote"
- If location is ambiguous, check the listing body for remote confirmation before scoring.

### Target Titles Only
Only surface roles with one of these titles (or close variants):

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
- Software Engineer, Developer, Designer, Sales, or any non-marketing role
- Roles requiring a security clearance
- Roles requiring relocation or in-office attendance

### Do NOT Submit Applications
Erin's workflow is **research and prepare, not auto-submit.** The agent should:
1. Find matching jobs
2. Score and rank them
3. Tailor the resume
4. Build the cover letter
5. **STOP — present all materials to Erin for review**
6. **Never submit an application without explicit confirmation**

---

## Resume Tailoring Rules

Every tailored resume bullet must follow this formula:

> **Action Verb + What You Did + Scale or Result**

Examples of correct format:
- ✅ "Generated 2,400+ qualified B2B leads within six weeks by architecting integrated, multi-channel campaigns across email, paid social, content, and webinars."
- ✅ "Improved MQL-to-SQL conversion by 70% by redesigning lead scoring, routing, and progressive profiling in Salesforce and Pardot."
- ❌ "Responsible for lead generation campaigns" (no verb strength, no result)
- ❌ "Helped with webinar production" (passive, no scale)

### Tailoring Process
1. **Read the JD carefully.** Extract: required skills, preferred skills, role-specific language (pipeline vs. revenue, GTM vs. launch, etc.), company context.
2. **Mirror the JD's language.** If they say "go-to-market," use "go-to-market." If they say "pipeline," use "pipeline."
3. **Reorder bullets by relevance.** Lead with the accomplishments that most directly match what the JD is asking for.
4. **Pull from the Master Accomplishments Bank** in master_resume.md for additional bullets when a JD calls for something not in the primary bullets.
5. **Never fabricate metrics, titles, dates, or skills.** Only reorder, reword using JD language, and emphasize what already exists.
6. **Bold key terms** that match the JD exactly (e.g., if they mention Salesforce, bold Salesforce).
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
- **At least one metric** from Erin's real experience in paragraph 2
- **Tone: confident peer, not eager applicant**
- Match JD vocabulary throughout
- Do not recite the resume — tell a story
- Save to: `$APPLIER_HOME/applications/<Company>/cover_letter.md`

### Cover Letter Voice
Erin writes with clarity and confidence. Her natural voice:
- Direct, not flowery
- Shows business judgment, not just task completion
- Connects marketing activity to revenue outcomes
- Does not use buzzword soup

---

## Job Search Strategy

When running `/apply-job search <query>`, use these search patterns:

```
"Product Marketing Manager" remote 2026
"Senior Product Marketing Manager" remote
"Senior Marketing Manager" remote B2B SaaS
"Director of Product Marketing" remote
"Marketing Manager" remote SaaS B2B
site:linkedin.com/jobs "Product Marketing Manager" remote
site:greenhouse.io "Senior Marketing Manager" remote
```

**Prioritize companies in:**
- B2B SaaS
- AI / ML / emerging technology
- Healthcare technology
- Enterprise software
- Marketing technology (MarTech)

**Filter out:**
- Consumer / B2C roles
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
| B2B SaaS experience valued | Boost score if company is B2B SaaS or AI |
| AI product experience | Boost score — Erin has strong AI GTM background |
| 15 years experience | Level match: Manager to Director level only |

**Dealbreakers (auto-fail):**
- Not remote
- Title is VP or above
- Title is below Manager level
- Requires relocation
- Requires security clearance
- Requires industry license

---

## Workflow Output for Each Job

For each qualified job, produce:
1. **Fit Score** (0–10) with rationale
2. **ATS Keyword Analysis** — matched vs. missing
3. **Company Research Brief** (3–5 bullets: what they do, recent news, why Erin fits)
4. **Tailored Resume** (`resume_tailored.md`) — ready to use
5. **Cover Letter** (`cover_letter.md`) — ready to use
6. **Summary card:** Company | Role | Fit Score | ATS Score | Remote Confirmed | Apply Link

Then **pause and present everything to Erin** for review before any submission or outreach.

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

## Key Metrics to Highlight (Erin's Top Stats)

Always have these available for cover letters and tailoring:

| Metric | Context |
|---|---|
| 2,400+ B2B leads in 6 weeks | simpleshow AI launch campaign |
| 70% MQL-to-SQL improvement | Salesforce/Pardot redesign |
| $200K pipeline in 10 days | V4 Avatar/Agentic Video launch |
| 150% website traffic growth | CRO + demand generation |
| 400% LinkedIn engagement growth | Content strategy |
| 12 Fortune 1000 net-new accounts | ABM program |
| 12+ AI product GTM launches | simpleshow, 2022–present |
| 190+ sales/marketing assets in 2025 | simpleshow enablement library |
| 30% email engagement improvement | Segmentation + A/B testing |
| 20+ webinars produced | End-to-end, including sales handoff |
| 2x Gold Brandon Hall Awards (2025) | Technology excellence |
| $58K closed revenue, $116.5K pipeline | Single J&J webinar |

---

## What This Agent Does NOT Do

- Does not submit applications without Erin's explicit approval
- Does not fabricate experience, metrics, dates, or titles
- Does not apply for roles that are not remote
- Does not apply for titles outside the target list
- Does not send emails or LinkedIn messages without confirmation
