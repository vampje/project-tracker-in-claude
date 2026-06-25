# Bi-Weekly JIRA Epic Updates Workflow

## Overview

**Purpose:** Systematic workflow for updating JIRA epics with executive-friendly status updates

**Cadence:** Every 2 weeks (adjust to your organization's reporting schedule)

**Time Investment:** 30 minutes with AI assistance, 2 hours manually

**Why This Matters:**
- Keeps leadership informed without constant status meetings
- Provides consistent visibility across all initiatives
- Enables early identification of at-risk work
- Creates historical record of progress

---

## The Problem This Solves

**Before this workflow:**
- Spent 2+ hours every 2 weeks manually updating 15-20 epics
- Inconsistent update formats across epics
- Hard to remember what changed in last 2 weeks
- Easy to miss updating important epics
- Difficult to aggregate status for milestone rollups

**After this workflow:**
- 30-minute interactive conversation with AI assistant
- Consistent executive-friendly format
- AI helps recall what happened
- Systematic review ensures nothing missed
- Automatic milestone aggregation

---

## Prerequisites

**JIRA Setup Required:**
- Custom fields for RAG status and Latest Update (see "JIRA Fields" section below)
- Epics tagged with delivery quarter/quarter label
- Active sprints defined in JIRA
- Epic Link field populated on stories

**AI Assistant Setup (Optional but Recommended):**
- Claude, ChatGPT, or similar AI assistant
- Access to your JIRA instance (via MCP, API, or manual copy/paste)
- Familiarity with your project structure

---

## Workflow Steps

### Step 1: Verify Current Date
**Why:** Ensures accurate date references in updates

**With AI:**
- AI automatically checks current date
- References correct reporting period

**Manual:**
```bash
date '+%Y-%m-%d (%A)'
```

---

### Step 2: Get List of Epics to Update

**Option A: Query by Delivery Quarter**
```jql
project = YOURPROJECT AND type = Epic AND "Delivery Quarter" = "26.2" AND status != Done
```

**Option B: Query by Active Sprint**
```jql
project = YOURPROJECT AND sprint in openSprints() AND type = Story
```
Then extract unique Epic Links from results.

**Option C: Manually List Epics**
Create a list of epics you need to update each cycle.

---

### Step 3: Review Each Epic

**For each epic, gather:**
- What shipped/completed in last 2 weeks
- What's currently in progress
- What's planned next
- Any blockers or risks
- Key dates or milestones

**Interactive Approach with AI:**
AI asks: "Is this your epic to update, or skip?"
- Update: AI helps draft status
- Skip: Move to next epic

**Manual Approach:**
Open each epic, review recent activity, write update.

---

### Step 4: Draft Executive-Friendly Update

**Format:**
- 1-2 sentences maximum
- Focus on outcomes, not activities
- Include specific deliverables
- Mention clear dates
- Note blockers if any

**Good Examples:**
- "Pilot with XX touring and select clients successful. Beginning phased rollout by market over next 4 weeks. Release delayed 1 day to Tuesday 3/25 due to incident affecting testing. Mobile work begins Sprint 26.2.1."
- "8 of 11 tickets (73%) shipped in Tuesday release. Remaining 3 tickets complete next sprint. Dashboard pilot scheduled with Finance team for March 20."
- "Data team dependency resolved. Front-end development complete. Backend work begins this sprint, targeting April 3 release."

**Bad Examples:**
- "Working on stuff." (too vague)
- "In progress." (no details)
- "Completed PROJ-123, PROJ-456, PROJ-789, started PROJ-1011, PROJ-1012, refined PROJ-1314, reviewed PROJ-1516..." (too detailed, not executive-friendly)

**Formula:**
`[Major accomplishment] + [Current status] + [What's next] + [Any blockers/dates]`

---

### Step 5: Set RAG Status

**On Track (Green):**
- Progressing as planned
- No major blockers
- On schedule for delivery
- Team has what they need

**At Risk (Yellow):**
- Minor delays or concerns
- Solvable blockers
- Might slip timeline slightly
- Needs attention but not critical

**Off Track (Red):**
- Significant blockers
- Will miss timeline
- Needs immediate intervention
- Leadership escalation needed

**Not Started (Gray):**
- Planned but not begun
- Waiting on dependencies
- Scheduled for future sprint

---

### Step 6: Update JIRA

**Update these fields:**
- RAG Status (customfield_XXXXX)
- Latest Update (customfield_YYYYY)
- Updated date (automatic)

**With AI:** AI makes the updates via API
**Manual:** Edit epic in JIRA, paste your drafted text

---

### Step 7: Aggregate Milestone Status (If Applicable)

If you have parent milestones with multiple child epics:

**Aggregation Rules:**
- If ANY epic = "Off Track" → milestone = "Off Track"
- Else if ANY epic = "At Risk" → milestone = "At Risk"
- Else if ALL epics = "On Track" → milestone = "On Track"
- Else if ALL epics = "Not Started" → milestone = "Not Started"

**Milestone Update:**
Combine updates from all child epics into cohesive summary.

Example:
```
"Dashboard: Pilot successful, beginning rollout (On Track).
Reports: 8/11 tickets shipped, 3 remaining next sprint (On Track).
Mobile: Data dependency resolved, development begins this sprint (At Risk due to 1-week delay)."
```

---

## JIRA Fields Reference

**You'll need these custom fields in your JIRA:**

### RAG Status Field
- **Type:** Single Select
- **Values:** On Track, At Risk, Off Track, Not Started
- **Where:** Epic level
- **Purpose:** Quick visual status

### Latest Update Field
- **Type:** Text (multi-line)
- **Where:** Epic level
- **Purpose:** Executive summary of progress

**How to Find Your Field IDs:**
1. Go to JIRA Settings → Issues → Custom Fields
2. Find your RAG and Update fields
3. Note the customfield_XXXXX IDs
4. Update your queries/automation to use these IDs

**Don't Have These Fields?**
- Use regular "Description" field for updates
- Use Labels for RAG status (labels: "rag-green", "rag-yellow", "rag-red")
- Or request custom fields from your JIRA admin

---

## Update Schedule Planning

**Sample 2026 Schedule (Bi-weekly on Thursdays):**

| Update # | Date | Period Covered |
|----------|------|----------------|
| 1 | Thu 3/20 | 3/6 - 3/20 |
| 2 | Thu 4/3 | 3/21 - 4/3 |
| 3 | Thu 4/17 | 4/4 - 4/17 |
| 4 | Thu 5/1 | 4/18 - 5/1 |

**Adjust for:**
- Your organization's reporting cadence (weekly, bi-weekly, monthly)
- Sprint boundaries (align with sprint end dates)
- Leadership meeting schedules (update before key meetings)
- Holidays and blackout periods

---

## Tips for Success

### Before Your First Update Cycle
- [ ] Identify which epics need regular updates
- [ ] Define your RAG status criteria
- [ ] Create update format/template
- [ ] Set up calendar reminder
- [ ] Get AI assistant configured (if using)

### During Each Update Cycle
- [ ] Review your daily log for what happened
- [ ] Check sprint completion reports
- [ ] Note any blockers or risks
- [ ] Draft updates in executive-friendly language
- [ ] Double-check dates and metrics
- [ ] Update all epics systematically

### After Each Update Cycle
- [ ] Share summary with your manager (optional)
- [ ] Note epics that are at risk for follow-up
- [ ] Update your project dashboard
- [ ] Schedule any needed stakeholder meetings

### Making It Easier
- **Keep notes as you go**: Add comments to epics throughout the 2 weeks
- **Link sprint completion reports**: Easy reference for what shipped
- **Use consistent language**: Build a library of phrases that work
- **Celebrate wins**: Note accomplishments, not just problems
- **Be honest about risks**: Early visibility enables early help

---

## Common Epics to Track

**Adapt this list to your organization:**

**Quarterly Initiatives:**
- New product features
- Major integrations
- Platform migrations
- Market expansion work

**Always-Active Epics:**
- Infrastructure improvements
- Security & compliance work
- General enhancements
- Technical debt reduction
- Support & bug fixes

**Cross-Team Dependencies:**
- Blocked on other teams
- Providing work to other teams
- Shared initiatives

---

## Integration with Other Tracking

**How this fits with your other tools:**

**Project Dashboard:**
- Dashboard: High-level project status
- JIRA Epics: Detailed execution status
- Updates flow: Dashboard → Epic Updates → Leadership

**Daily Log:**
- Daily Log: Track daily work
- Epic Updates: Summarize last 2 weeks
- Updates flow: Daily notes → Epic summary

**Weekly Updates:**
- Weekly Updates: Your work for your manager
- Epic Updates: Epic status for leadership
- Audience: Manager vs. Executives

---

## Automation Ideas

**With AI Assistant:**
- AI reads your daily log and drafts epic updates
- AI queries JIRA for sprint completions
- AI formats updates consistently
- AI handles milestone aggregation

**With JIRA Automation:**
- Auto-update "Updated" date when RAG changes
- Send Slack notification when epic goes "At Risk"
- Create dashboard report of all epic statuses
- Auto-generate email summary for leadership

**With Scripts:**
- Python script to query JIRA and format updates
- Slack bot to remind you it's update day
- Export epic statuses to spreadsheet

---

## Customization Guide

### For Different Team Structures

**Single Team:**
- Track your epics only
- Simple status updates
- No milestone aggregation needed

**Multiple Teams:**
- Track epics across teams
- Note cross-team dependencies
- Aggregate by team or initiative

**Program/Portfolio:**
- Track milestones (parent epics)
- Aggregate child epic status
- Include cross-program dependencies

### For Different Reporting Audiences

**Your Manager:**
- More detailed updates
- Include technical context
- Note team capacity issues

**Executive Leadership:**
- High-level outcomes only
- Business impact focus
- Clear dates and deliverables

**Stakeholders:**
- Feature-focused updates
- User impact highlighted
- Release timeline visibility

---

## FAQ

**Q: What if I have 50+ epics?**
A: Filter to active epics only (in current quarter + in active sprints). Archive completed work.

**Q: What if nothing changed in 2 weeks?**
A: Still update with "No change - continues on track for [date]" or similar. Silence is confusing.

**Q: Do I update epics that are blocked?**
A: YES! Especially important. "Still blocked on [dependency]. Following up with [person] by [date]."

**Q: How detailed should updates be?**
A: 1-2 sentences. If it needs more explanation, link to a doc or schedule a meeting.

**Q: What if I forget to update?**
A: Set calendar reminder. Make it a recurring meeting with yourself. Use AI assistant to make it faster.

**Q: Can I do this weekly instead of bi-weekly?**
A: Yes! Adjust cadence to match your organization. Weekly is great for fast-moving teams.

---

## Success Metrics

**You'll know this is working when:**
- ✅ Leadership stops asking "what's the status of X?"
- ✅ You can answer status questions without scrambling
- ✅ At-risk work gets identified early (before it's a crisis)
- ✅ You spend less time in status meetings
- ✅ Your updates are cited in leadership meetings
- ✅ Other PMs ask how you stay so organized

**Time saved:**
- Before: 2 hours every 2 weeks = 52 hours/year
- After: 30 minutes every 2 weeks = 13 hours/year
- **Savings: 39 hours/year** (almost a full work week!)

---

## Example: Full Update Cycle

**Sample Epics to Update (Week of March 20, 2026):**

1. **Mobile Dashboard Release** (PROJ-100)
   - Latest Update: "8 of 11 tickets (73%) shipped Tuesday 3/17. Remaining 3 tickets (Pendo guides, E2E tests, metrics fix) complete by 3/24. UK pilot begins 3/27."
   - RAG: On Track

2. **VIP International Expansion** (PROJ-200)
   - Latest Update: "Data team dependency on PROJ-5300 resolved. Front-end work complete. Backend development begins Sprint 26.2.1, targeting 4/3 release."
   - RAG: On Track

3. **Payment Integration** (PROJ-300)
   - Latest Update: "Blocked on Payments API team - awaiting sandbox environment. Following up with Sarah by 3/22. Front-end work ready to begin once unblocked."
   - RAG: At Risk

4. **Infrastructure Migration** (PROJ-400)
   - Latest Update: "Pilot with 5 clients successful. Migration paused until Q3 due to competing priorities (Mobile Dashboard, VIP International). Planning resumes in June."
   - RAG: Not Started (Q3)

**Milestone Aggregation (Q2 Product Initiatives):**
- **Status:** At Risk (one epic at risk)
- **Update:** "Mobile Dashboard shipped 73% (On Track). VIP International dependency resolved, development begins next sprint (On Track). Payment Integration blocked on Payments API team sandbox (At Risk). Infrastructure Migration paused until Q3 due to prioritization (Not Started for Q2)."

---

_This workflow template was created by a PM who went from dreading bi-weekly updates to actually enjoying them (with AI help). Adapt it to your needs and make it your own!_
