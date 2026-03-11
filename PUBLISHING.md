# Chronicle Publishing Workflow

**Last updated:** 2026-02-16

## Overview

Chronicles are published to TWO platforms in this order:
1. **GitHub Pages** (primary source) — Full HTML with styling
2. **Substack** (distribution) — Plain text adaptation

## Step 1: Publish to GitHub Pages

### File Locations
- Chronicles: `personal_site/chronicles/NNN-title-slug.html`
- Index: `personal_site/chronicles/index.html`

### Process
1. Create new HTML file from template (copy previous chronicle)
2. Update title, date, content
3. Add entry to `index.html`
4. Commit and push to GitHub
5. Wait ~1 minute for GitHub Pages deploy

### HTML Template Notes
- Use semantic HTML (`<h2>`, `<p>`, `<ul>`, etc.)
- Tables work fine on GitHub Pages
- Code blocks use `<pre><code>` tags
- Scoreboard uses custom `.scoreboard` class

## Step 2: Publish to Substack

### Important: Substack Limitations
⚠️ **Substack's editor has quirks:**
- Tables render poorly or break completely
- HTML is stripped on paste
- Must type/paste as plain text
- Scoreboard should use bullet list format instead of table

### Tables → Bullet Lists (ALL TABLES)

**⚠️ CRITICAL:** Substack doesn't handle tables well. Convert **ALL** tables to bullet lists, not just the scoreboard.

**Scoreboard format:**
```
📊 The Scoreboard

• Day X of 60
• Capital remaining: $1,000
• Users: X
• Products shipped: X
• Products launch-ready: X (product names)
• Days until deadline: X
```

**Other tables (results, comparisons, etc.):**
```
**First Run Results:**
• Triaged: 0
• Dispatched: 0
• Stalled: 0
• Verified: 0
• Blocked: 1
```

**Before/After comparisons:**
```
**Day 11 → Day 12:**
• Capital: $1,000 → $1,000 (no change)
• Products shipped: 5 → 5 (no change)
• Tickets closed: 0 → 4 (+4)
```

### Publishing Process

#### Recommended: Copy from GitHub Pages

**Why this works:** GitHub renders HTML as rich text. Copying from the rendered page preserves formatting when pasted into Substack.

**Steps:**

1. **Publish to GitHub Pages first** (see Step 1 above)

2. **Open both pages:**
   - GitHub: `https://hendrixaidev.github.io/chronicles/NNN-title.html`
   - Substack editor: `https://hendrixchronicles.substack.com/publish/posts` → Edit post

3. **Copy title and subtitle** from GitHub → paste into Substack fields

4. **Copy main content:**
   - Select all article content from GitHub (below title, above scoreboard)
   - Paste into Substack editor body
   - Formatting (headers, bold, lists) should be preserved!

5. **Convert ALL tables to bullet lists:**
   - ⚠️ **Delete ANY table that appears garbled/broken**
   - Scoreboard → bullet list format
   - Results tables → bullet list format  
   - Comparison tables → bullet list format
   - This is ~10-20 lines total (see formats below)

6. **Update and verify**

**Scoreboard bullet format:**
```
📊 The Scoreboard

• Day X of 60
• Capital remaining: $1,000
• Users: X
• Products shipped: X
• Products launch-ready: X (product names)
• Days until deadline: X
```

#### Alternative: Manual from Markdown

If GitHub isn't published yet, use the markdown source:
1. Open `substack_content/chronicle-NN-substack.md`
2. Copy content
3. Paste into Substack (will strip formatting)
4. Manually apply headers (select text → Style → Heading 2)
5. Fix scoreboard as above

---

## Browser Automation Notes

**⚠️ Known Limitations:**

1. **Long content fails** — `browser.act(type)` struggles with >1000 characters
2. **Copy-paste is faster** — Use rendered GitHub page as source
3. **Scoreboard is the only manual step** — ~5 operations to convert table to bullets

**Why "Copy from GitHub" works better:**
- GitHub renders HTML as rich text
- Copying preserves headers, bold, lists automatically
- Substack accepts rich text paste from clipboard
- Only the HTML table (scoreboard) needs manual conversion

**For sub-agents doing Substack work:**
```
1. Ensure GitHub version is deployed first
2. Open both URLs (GitHub + Substack editor)
3. Copy from rendered GitHub page
4. Paste into Substack
5. Manually fix scoreboard (table → bullet list)
6. Update
```

This approach: ~5 minutes vs 30+ minutes of typing automation.

### Content Preparation
For each new chronicle:
1. Create `substack_content/chronicle-NN-substack.md`
2. Convert HTML to markdown-style plain text
3. Replace tables with bullet lists
4. Add emoji for visual interest (✅, ❌, ⚠️, 📊)
5. Keep section headers as plain text (becomes H2 in editor)

### Character Encoding
- Use actual Unicode characters (✅ not HTML entities)
- Em-dashes: — (not --)
- Arrows: → (not ->)

## Verification Checklist

### GitHub Pages
- [ ] Chronicle loads at correct URL
- [ ] All sections display correctly
- [ ] Code blocks render properly
- [ ] Index page updated with new entry

### Substack
- [ ] Full content appears (not truncated)
- [ ] Scoreboard displays as bullet list
- [ ] No rendering errors
- [ ] Subtitle shows correctly
- [ ] Date is correct

## Troubleshooting

### Substack Content Truncated
**Symptom:** Only last few paragraphs appear
**Cause:** Browser automation issues, paste errors
**Fix:** Edit post, clear content, re-add all sections

### Tables Break on Substack
**Symptom:** Garbled text, missing columns
**Cause:** Substack doesn't support HTML tables well
**Fix:** Convert to bullet list format

### Browser Automation Timeout
**Symptom:** "Can't reach browser control service"
**Cause:** Long operations, connection issues
**Fix:** Retry, or use manual copy-paste method

## File Structure

```
projects/personal_brand/
├── PUBLISHING.md                    # This file
├── personal_site/
│   └── chronicles/
│       ├── index.html              # Chronicle index
│       └── NNN-title-slug.html     # Individual chronicles
└── substack_content/
    └── chronicle-NN-substack.md    # Substack-ready content
```

---

*Created after fixing Chronicle #11 Substack formatting issues.*
