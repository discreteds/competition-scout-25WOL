# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

This is the **data repository** for "25 Words or Less" competition tracking. Competitions are stored as GitHub issues with entries, strategy, and submission tracking as comments.

The skills that power this workflow live in the separate `competition-scout` repository.

## Available Skills

Invoke skills by asking naturally:

| Request | Skill Used |
|---------|------------|
| "Scrape competitions from the usual sites" | `comp-scout-scrape` |
| "Analyze this competition for strategy" | `comp-scout-analyze` |
| "Write entries for this competition" | `comp-scout-compose` |
| "Save this competition to GitHub" | `comp-scout-persist` |

## Workflow

```
Scrape → Persist (create issue) → Analyze → Compose → Persist (add entry as comment)
```

### Deduplication

Competitions from multiple aggregator sites are deduplicated:
- 80% fuzzy title match → adds as comment on existing issue
- New competition → creates new issue with milestone and labels

### Issue Structure

Each competition gets ONE issue. All activity becomes comments:
- Additional sources
- Strategy analysis
- Draft entries (with star ratings)
- Submission confirmation
- Win/loss notification

## GitHub Project Integration

- **Project:** Competition Scout - 25WOL Competitions (#6)
- **Config:** `.hiivmind/github/config.yaml` (shared, commit this)
- **User:** `.hiivmind/github/user.yaml` (personal, gitignored)

### Labels

**Status labels:**
`competition`, `25wol`, `closing-soon`, `entry-drafted`, `entry-submitted`, `won`

**Filter labels:**
- `not-interested` - Not interested in this competition
- `for-kids` - Prize is primarily for children (auto-close, user has no kids)
- `already-entered` - Already submitted an entry (from earlier process)
- `cruise` - Prize involves a cruise (auto-close, user gets seasick)

### Auto-Filtering Rules

When analyzing competitions, apply these rules and auto-close with appropriate label:
- **Kids/family prizes** (toys, kids books, baby products, theme parks marketed to families): Tag `for-kids`
- **Cruise prizes**: Tag `cruise`

**User context:**
- No children - not interested in child-focused prizes
- Gets seasick - not interested in cruises

### Milestones

Grouped by closing date month (auto-assigned on persist).

## Prerequisites

```bash
# GitHub CLI authenticated
gh auth status

# Playwright for scraping (in competition-scout repo)
pip install playwright
playwright install chromium
```

## Sponsor → Tone Matrix

Strategy analysis maps sponsor category to winning tone:

| Sponsor Type | Tone |
|--------------|------|
| Wellness/luxury | Sincere, aspirational |
| Tech/gaming | Self-aware humour |
| Food/beverage | Relatable, sensory |
| Travel | Discovery energy |
| Retail/general | Personality, memorable |
| Rural/agricultural | Practical, authentic |

## Entry Arc Structures

Compose skill uses 5 arc types:
1. **Sincere** - Admission → Aspiration → Warm landing
2. **Comedic** - Setup → Pivot → Callback
3. **Self-deprecating** - Confession → Resolution → Optional undercut
4. **List-pivot** - Credentials → Gap → Aspiration
5. **Sensory** - Scene → Vivid detail → Emotional resonance

Arc selection should match sponsor category. Landing strength (1-5 stars) predicts competitiveness.
