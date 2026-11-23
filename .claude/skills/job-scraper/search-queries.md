# Search Queries for Job Scraper

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. None ship with AI Job Search: copy the ones for your market from [community-portals](https://github.com/ai-job-search-dev/community-portals) (e.g. `linkedin-search`, `freehire-search` under `portals/global/`), or build one with `/add-portal`. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

## Search Sites

Primary (your market's job boards - scaffold one with `/add-portal`):
- **linkedin.com/jobs** - LinkedIn job listings (filter: USA, Remote); covered by the community `linkedin-search` CLI once installed
- **greenhouse.io** - Many companies use Greenhouse for their careers page
- **lever.co** - Companies using Lever ATS
- **workday.com** / **myworkdayjobs.com** - Enterprise employers using Workday
- **smartrecruiters.com** - Large job board with corporate listings
- **indeed.com** - General job board (USA-focused)

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies

## Query Categories

Queries are grouped by priority. Write **each category in every language from your Languages table** (see Language scope above). Combine each query with your location terms (e.g. your city, region, or metro area) where the site supports it.

Each priority has two kinds of block. **Plain terms** blocks are what the portal CLIs consume: one term per line, one CLI call per term, no `OR`, no `site:` prefix, and no location (the CLI's location flag, or the city in `--query` where that portal's SKILL.md says so, carries it). Quote a multi-word phrase only if the portal's `Query syntax:` line says quoting is honoured. **WebSearch-only** blocks are Google syntax (`site:`, quotes, `OR`) for the fallback path and are never passed to a CLI.

**Organize by function, not job title.** The same underlying work carries different titles across companies and markets (a "Data Scientist" role at one employer may be posted as "Insights Analyst" or "Data Consultant" at another). Name each priority category after the function it covers, and list several plausible job titles as query variants within that category rather than betting an entire priority tier on one exact title string.

### Priority 1: Full Stack .NET Developer

These match your strongest and most desired career direction.

#### Plain terms (portal CLIs)

```
Full Stack .NET Developer
Senior .NET Developer
ASP.NET Core Developer
.NET Backend Developer
Angular Developer
```

#### WebSearch-only (`site:` fallback)

```
site:linkedin.com/jobs "Full Stack .NET Developer" USA remote
site:linkedin.com/jobs "Senior .NET Developer" USA remote
site:linkedin.com/jobs "ASP.NET Core" "Angular" remote
site:linkedin.com/jobs ".NET Developer" "SQL Server" remote
```

### Priority 2: Financial Services Technology

These match your domain expertise in FinTech and financial services.

#### Plain terms (portal CLIs)

```
Financial Technology Developer
FinTech Engineer
Insurance Tech Developer
Banking Software Engineer
Healthcare IT Developer
```

#### WebSearch-only (`site:` fallback)

```
site:linkedin.com/jobs "Financial Technology" USA remote
site:linkedin.com/jobs "Insurance Technology" .NET
site:linkedin.com/jobs "Healthcare IT" "ASP.NET Core"
```

### Priority 3: Cloud-Native Developer

Adjacent roles you could pivot into with your Azure experience.

#### Plain terms (portal CLIs)

```
Azure Developer
Cloud Software Engineer
Cloud Native Developer
Azure DevOps Engineer
```

#### WebSearch-only (`site:` fallback)

```
site:linkedin.com/jobs "Azure Developer" .NET USA remote
site:linkedin.com/jobs "Cloud Native" "ASP.NET Core" "Docker"
```

### Priority 4: Full-Stack Engineer

Broader net for general technical roles.

#### Plain terms (portal CLIs)

```
Full Stack Engineer
Software Engineer
Senior Software Engineer
```

#### WebSearch-only (`site:` fallback)

```
site:linkedin.com/jobs "Full Stack Engineer" .NET remote
site:linkedin.com/jobs "Senior Software Engineer" "C#" USA
```

## Location Filter

When evaluating results, verify the job location is within reasonable commute distance from your home. Define acceptable areas:
- USA (Remote)
- Sacramento, CA
- Framingham, MA
- Chicago, IL
- Atlanta, GA

## Language Filter

Your working languages and levels are in CLAUDE.md's Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you haven't declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead (see `job-scraper/SKILL.md`'s Step 3 "Quick Fit Assessment" for how the flag surfaces in `/scrape` output). Postings simply *written* in a language you don't work in, that don't require it on the job, are fine.

## Date Filter

Only include jobs posted within the last 14 days, matching `/scrape` Step 1b.3: use a supported recency filter or filter the returned publication dates client-side. A future application deadline does not bypass this discovery window; `/rank` handles deadline expiry and urgency separately after discovery. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries