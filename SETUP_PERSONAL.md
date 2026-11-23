# Personal Setup Guide

This guide helps you configure the AI Job Search framework for your personal use on both mobile and desktop devices.

## Quick Start (Recommended)

### Option 1: Via Claude Code CLI (Desktop)
```bash
cd D:\job search\job-search
claude /setup
```

Follow the interview prompts to complete your profile setup.

### Option 2: Via Claude.ai/Code (Any Device)
1. Visit [claude.ai/code](https://claude.ai/code)
2. Sign in with your Anthropic account
3. Connect your GitHub repository: `psree114-web/job-search`
4. Run `/setup` in the chat

## Your Profile Summary

Already configured with your profile:
- **Name:** Sreemanth
- **Expertise:** 10+ years full-stack .NET development
- **Key Skills:** C#, ASP.NET Core, Angular, Azure, SQL Server
- **Target Roles:** Full Stack .NET Developer, Senior .NET Developer
- **Location:** Remote (Sacramento/Framingham/Chicago acceptable)

## Job Portals Setup

### Recommended portals for your market:
1. **LinkedIn** - `linkedin-search` (remote .NET jobs)
2. **Indeed** - General tech job board
3. **Greenhouse/Lever** - Direct employer career pages

### To add portals:
```bash
# Copy from community-portals
# Then install:
python tools/install_portal_clis.py
```

## Workflow Commands

| Command | Purpose |
|---------|---------|
| `/setup` | Profile setup/refresh |
| `/scrape` | Find new job postings |
| `/scrape <topic>` | Search by topic (e.g., "Azure") |
| `/apply <URL>` | Apply to job (auto-tailors CV/cover letter) |
| `/rank` | Score scraped jobs, get ranked shortlist |
| `/interview <company>` | Prepare interview materials |
| `/outcome <company>` | Track application results |
| `/html-report` | Generate application dashboard |

## Mobile Usage Tips

### Using Claude.ai/Code mobile app:
1. Download Claude app from App Store or Play Store
2. Sign in with same Anthropic account
3. Open your repository
4. Run commands directly in chat

### Best practices for mobile:
- Run `/scrape` to find jobs, then `/rank` for shortlist
- Use `/apply <URL>` - Claude will auto-generate documents
- Check results on desktop when compiling PDFs (requires LaTeX)

## PDF Compilation

**Desktop:**
```bash
cd cv && lualatex main_<company>_<role>.tex
cd ../cover_letters && xelatex cover_<company>_<role>.tex
```

**Mobile:** PDFs will be generated but need desktop for final verification.

## Files Created/Modified

- `CLAUDE.md` - Your candidate profile
- `.claude/skills/job-application-assistant/01-candidate-profile.md` - Structured profile
- `.claude/skills/job-application-assistant/04-job-evaluation.md` - Job evaluation framework
- `.claude/skills/job-scraper/search-queries.md` - Job search queries

## Next Steps

1. Add your CV to `documents/cv/` (PDF or .tex)
2. Add LinkedIn export to `documents/linkedin/`
3. Run `/setup --section skills` to refine your skill definitions
4. Run `/scrape` to find jobs matching your profile

## Support

- README.md - Full documentation
- SETUP.md - Detailed setup instructions
- SECURITY.md - Security guidelines