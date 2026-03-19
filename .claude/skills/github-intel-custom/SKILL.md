---
name: github-intel-custom
description: Scan GitHub for trending repos and new projects matching your interests. Runs quietly during /daily-plan.
---

# GitHub Intel

Discover new GitHub repos matching your tech interests — trending projects, new releases in your domains, and repos gaining momentum.

## Usage

```
/github-intel-custom              # Full scan + display
/github-intel-custom --scan       # Compact mode (used in /daily-plan)
/github-intel-custom --config     # Update your tracked topics/keywords
/github-intel-custom --seen       # Show all repos you've already been shown
```

---

## Process

### Step 0: Check Config

Read `System/github-intel.yaml`.

**If missing:** Run First-Time Setup before continuing.

**If `--config` flag:** Skip to First-Time Setup (re-run config).

**If `--seen` flag:** Skip to Show Seen Repos.

---

### First-Time Setup

Ask the user:

```
Let me set up GitHub Intel for you.

What should I track? Tell me:
1. Tech areas / topics (e.g. "AI agents", "developer tools", "PKM")
2. Specific GitHub topics (e.g. "llm", "mcp", "obsidian") — optional
3. Minimum stars to surface (default: 50 — filters out noise)
4. Languages to focus on (e.g. Python, TypeScript) — optional, leave blank for all
```

Save their response to `System/github-intel.yaml` in this format:

```yaml
# GitHub Intel — Your Interest Config
# Edit anytime or run /github-intel-custom --config to update

# GitHub topic slugs (from github.com/topics/{slug})
topics:
  - llm
  - ai-agents
  - developer-tools

# Free-form keywords searched in repo name/description
keywords:
  - "MCP server"
  - "personal knowledge"

# Minimum stars (filters noise)
min_stars: 50

# Programming languages to focus on (empty = all)
languages: []

# How many days back counts as "new"
lookback_days: 7

# Max repos to surface per scan
max_per_scan: 8
```

Confirm: "Config saved. Running your first scan now..." then proceed to Step 1.

---

### Show Seen Repos (`--seen` flag)

Read `System/github-intel-state.json` → `seen_repos` array.

Display:
```
📚 REPOS ALREADY SURFACED (X total)

[full_name] — surfaced [date]
...

Run /github-intel-custom to scan for new ones.
```

---

### Step 1: Read State

Read `System/github-intel-state.json`. If missing, initialize:

```json
{
  "seen_repos": [],
  "last_scan": null,
  "total_surfaced": 0
}
```

---

### Step 2: GitHub API Search

Read config from `System/github-intel.yaml`.

Calculate `since_date`: today's date minus `lookback_days` (format: YYYY-MM-DD).

**Rate limit awareness:** Public GitHub API = 60 req/hr unauthenticated. Combine topics into a single query where possible.

**Topic search (batch topics with OR to save API calls):**

```bash
curl -s "https://api.github.com/search/repositories?q=topic:TOPIC1+OR+topic:TOPIC2+created:>SINCE_DATE&sort=stars&order=desc&per_page=20" \
  -H "Accept: application/vnd.github.v3+json" \
  -H "User-Agent: Dex-GitHub-Intel"
```

**Keyword search (one call per keyword, or batch with OR):**

```bash
curl -s "https://api.github.com/search/repositories?q=KEYWORD+in:name,description+created:>SINCE_DATE+stars:>MIN_STARS&sort=stars&order=desc&per_page=10" \
  -H "Accept: application/vnd.github.v3+json" \
  -H "User-Agent: Dex-GitHub-Intel"
```

**Language filter** (if languages configured, append): `+language:python`

**If API returns 403 (rate limited):** Show message:
```
⚠️ GitHub API rate limit reached (60 req/hr for unauthenticated).
Next scan will work once the limit resets (~1 hour).
Add a GitHub token to System/github-intel.yaml as `github_token: ghp_...` to raise the limit to 5000/hr.
```

Extract from each result:
- `full_name` (e.g., `owner/repo`)
- `description`
- `stargazers_count`
- `html_url`
- `topics` array
- `created_at`
- `updated_at`
- `language`

---

### Step 3: Trending Supplement (WebSearch)

Use WebSearch to find repos gaining momentum (complements the API's "new" filter with "popular right now"):

Search queries (use 1-2 to save context):
- `"github trending" {top_topic} 2026`
- `site:github.com {top_keyword} stars 2026`

Extract any repo names (owner/repo format) mentioned in results. These get a **trending bonus** in scoring.

---

### Step 4: Filter and Score

From all API results combined:

1. **Remove seen** — filter out any `full_name` already in `seen_repos`
2. **Apply `min_stars`** — drop repos below threshold
3. **Score each repo (0-100):**

| Signal | Points | Logic |
|--------|--------|-------|
| Stars | 0-30 | `min(30, log10(stars) * 10)` |
| Recency | 0-30 | Newer created_at = higher score |
| Keyword match | 0-20 | +5 per keyword found in name/description |
| Trending signal | 0-20 | +20 if appeared in WebSearch trending results |

4. **Sort by score, take top `max_per_scan`**
5. **Extract "why"** — 1-sentence reason this matches user's interests (which topic/keyword triggered it)

---

### Step 5: Display Results

**Full mode (default):**

```
🔭 GITHUB INTEL — [DATE]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✨ NEW THIS WEEK

1. **owner/repo-name** ★ 1.2k
   One-line description from GitHub
   Why: Matches "llm" topic + trending
   → https://github.com/owner/repo-name

2. **owner/repo-name** ★ 340
   One-line description
   Why: Matches "MCP server" keyword
   → https://github.com/owner/repo-name

[up to max_per_scan]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📊 Scan: [N] API queries · [N] repos found · [N] new · [N] already seen
Last scan: [date]

Want to save any of these as a note? (Enter number, 'all', or 'skip')
```

**If nothing new:**

```
✅ Nothing new in your GitHub areas since last scan ([date]).
```

**Compact mode (`--scan`, for daily-plan):**

Only output if there ARE new repos. If nothing new, output nothing (truly silent).

```
🔭 GitHub Intel: [N] new repos →
   • owner/repo (★N, brief description)
   • owner/repo (★N, brief description)
Run /github-intel-custom to explore.
```

---

### Step 6: Save to Note (Optional, Full Mode Only)

If user wants to save a repo:

1. Append to `00-Inbox/Ideas/GitHub_Intel_[YYYY-MM-DD].md` (create if needed):

```markdown
## [owner/repo](https://github.com/owner/repo)

**Stars:** [N] | **Language:** [lang] | **Found:** [date]
**Why:** [matched topic/keyword]

> [description]
```

2. Offer to link to a relevant project: "Want to link this to any active project?"

---

### Step 7: Update State

After displaying results (whether user saves or skips), update `System/github-intel-state.json`:

- Add all surfaced `full_name` values to `seen_repos`
- Update `last_scan` to today (YYYY-MM-DD)
- Increment `total_surfaced` by count of new repos shown

```json
{
  "seen_repos": ["owner/repo-1", "owner/repo-2"],
  "last_scan": "2026-03-19",
  "total_surfaced": 8
}
```

---

## Error Handling

**No config yet:** Run First-Time Setup.

**API rate limited (403):** Show rate limit message, suggest adding token.

**No results from API:** "GitHub returned no repos for your topics in the last [lookback_days] days. Try widening `lookback_days` in System/github-intel.yaml."

**curl not available:** Use `python3 -c "import urllib.request; ..."` as fallback.

---

## Track Usage (Silent)

Update `System/usage_log.md` to mark github-intel as used.
