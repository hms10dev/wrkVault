# Meeting Notes - Framework Focus & Sprint Planning

## Key Decisions & Action Items

### Sprint Goals

- **Target:** 5-6 story points this sprint (moving toward 6 as standard)
- **Strategy:** Focus on framework/UI stories vs. complex business logic
- **Timeline:** Code freeze Tuesday/Wednesday, planning Thursday/Friday

### Current Sprint Work

- ✅ Auto aggregate story - DONE
- ✅ Quick defect fix - DONE
- 🔄 Lifecycle status research - waiting on Abolash backend changes
- 📝 Percent field change - new easy story to boost stats

### New Meeting Structure

**Friday Office Hours** (replacing daily check-ins)

- Weekly sprint planning & story review
- Technical discussion time
- Flexible timing (closer to lunch/afternoon)
- Include DA if needed

**Presentation Dry Run**

- Scheduled for next Friday
- Include: David, Hollis, Achea
- Goal: Final feedback before presentation

---

## Strategic Shift: Framework Focus

### Why This Change

- More available resources & documentation for framework/UI
- Less dependency on limited business logic experts
- Easier to achieve story point targets while learning
- Reduces pressure while still building domain knowledge

### What This Means

- **Primary focus:** Framework, UI, entity creation, async operations
- **Secondary learning:** Business logic through observation & discussion
- **Knowledge building:** Understanding backend changes without implementation pressure

---

## Lifecycle Status Deep Dive

### Business Context

**What it is:** Tracks where items are in their lifecycle (new → active → discontinued)

- Standard statuses: Active, Inactive, Discontinued
- Each status has ~10-15 boolean flags (should forecast, should order, etc.)
- Critical for forecasting decisions

### Technical Implementation

**Inheritance Challenge:**

- Status can be set at global, region, class, item, or item location level
- Item locations inherit from higher levels
- 16M item locations vs 300K items = performance considerations
- Status fetched "on the fly" rather than stored at item location level

**Current Process:**

1. Forecasting runs → fetches lifecycle status from item location
2. Status saved on forecast entity
3. Only updates when forecasting runs again
4. Status reflects "last time forecasting system checked" not real-time

### Your Work

- Abolash: Backend changes to fetch/display lifecycle status
- Hollis: UI implementation to show status on forecast entity list
- **Learning opportunity:** Review Abolash's code, understand inheritance framework

---

## Career Development Plan

### Learning Strategy

1. **Hands-on:** Framework/UI stories for consistent delivery
2. **Observation:** Review backend changes, ask for code walkthroughs
3. **Documentation:** Log business logic learning in residency training
4. **Discussion:** Friday sessions for deeper technical understanding

### Success Metrics

- Consistent 5-6 story point delivery
- Growing framework expertise
- Business domain knowledge through osmosis
- Proactive story ownership & closure

### Tools & Process

- Continue using Obsidian for notes
- Use spaced repetition plugins for review
- Set calendar reminders for sprint planning
- Own story closure process (chase testing, QE, etc.)

---

## Next Week Actions

### Immediate (This Week)

- [ ] Complete percent field change story
- [ ] Stay on top of aggregate story testing (Rama)
- [ ] Prep for lifecycle status work (understand requirements)

### Sprint Planning (Friday)

- [ ] Review next sprint stories in advance
- [ ] Prepare questions for office hours
- [ ] Alert David by Thursday if no stories assigned

### Ongoing

- [ ] Log lifecycle status learning in residency training
- [ ] Schedule brief code review with Abolash when ready
- [ ] Maintain proactive communication on story progress