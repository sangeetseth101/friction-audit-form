# Nicole Leon — Friction Audit Intake: Full Context

## Origin

Lori Young (founding pro bono client, On A Mission Brands) referred **Nicole Leon** via WhatsApp on March 30, 2026. Lori had been telling Nicole about the systems Sangeet built for her, and Nicole wants something similar.

---

## Who Is Nicole Leon

- **Personal brand:** Confidence mentor helping women show up boldly
- **Second business:** VA (Virtual Assistant) agency supporting online entrepreneurs
- **Core problem:** Maxed out on time. Looking for ways to do things faster and more efficiently.
- **Buying signal:** Lori says Nicole "would rather pay someone because she is very busy" — strong done-for-you buyer intent
- **Referral context:** Lori called her "a dear friend" and asked if Nicole could be Sangeet's first paying client at a discount

---

## Qualification Assessment

**Green flags:**
- Two businesses (more friction surface area = more value to deliver)
- Time-maxed (classic ICP pain: "drowning in repetitive tasks")
- Willing to pay (not a freebie seeker)
- Warm referral from an existing client (trust already transferred)
- Fits the archetype: non-technical expert who is pro-outcome, not anti-tech

**Things to validate on the call:**
- Revenue range (is she in the $100K-$250K sweet spot?)
- Team size (solo? has VAs from her own agency?)
- Has she tried AI tools before? What stuck, what didn't?
- Which business has more friction — the mentoring or the VA agency?

---

## Reply Strategy to Lori

### What Sangeet sent:
> Would love to help her too :) Let me share a quick form and a booking link so she can give me some context about her businesses and pick a time that works. I'd be even happier if you could hop on the call and introduce us — I think she'd feel more comfortable that way. But totally up to you!

### Why this works:
- Thanks Lori without being over-the-top
- Introduces the form + booking flow (structure)
- Invites Lori to the call (builds trust for Nicole)
- Gives Lori an easy out ("totally up to you")
- Does NOT discuss pricing — too early, need the audit first

### Pricing note:
Lori asked for a discount. Sangeet is not addressing this yet. Strategy: run the friction audit first, understand scope, then price fairly. Can offer a friends-and-family rate after knowing what's involved. Never price blind. Never go below $1,500.

---

## The Intake Form

### Purpose
Get enough context about Nicole before the friction audit call so Sangeet can skip small talk, arrive prepared with research, and make the call feel high-value from minute one.

### Design Decisions

**Multi-step flow (3 steps):**
1. **You** — Name, email, phone/WhatsApp, website, LinkedIn, referral source
2. **Business & Friction** — What her business does, years in business, team size, what eats her time, magic wand question, AI experience
3. **Book** — Cal.com inline embed (friction audit booking)

**Why multi-step:**
- Reduces cognitive load for a busy person
- Progress bar creates momentum (sunk cost effect)
- Form data submits to Google Sheets at end of step 2, before she even books — so even if she abandons at the calendar, Sangeet still has her info

**Questions chosen and why:**

| Question | Why it's there |
|---|---|
| Full Name + Email | Basic identification |
| Phone / WhatsApp | Lori referred via WhatsApp. Nicole's world runs on mobile. Need a fast follow-up channel. |
| Website + LinkedIn | Pre-call research. Sangeet can study her business, offers, content, and positioning before the call. |
| How did you hear about this? | Attribution. Also makes the form feel personal when she writes "Lori Young." |
| What does your business do? | Core context. Two businesses = need to understand both. |
| Years in business + Team size | Quick qualification signals (ICP is 3+ years, solo to 3 people). |
| What eats up most of your time? | The #1 friction question. Free-text so she can say things Sangeet wouldn't have thought to ask about. |
| If I could fix ONE thing overnight? | The magic wand question. Her answer tells Sangeet exactly what to lead with in the audit. First instinct = highest pain. |
| Have you tried AI tools? | Calibration. Tells Sangeet whether to explain AI from scratch or skip to specifics. |

**Questions intentionally removed:**
- "Introduce yourself in 2-3 lines" — redundant. Sangeet already knows who she is from Lori. And the business description question covers it.
- "Walk me through a typical workday" — too much homework for a busy person. Save the deep dive for the actual call.
- Chip selector for time drains — replaced with free-text textarea. Chips look nice but limit responses to pre-defined options. Free text captures things you'd never think to list.
- "How did you hear about this" was debated (Sangeet already knows) but kept because: (a) it works as an attribution field for future leads who aren't referrals, and (b) writing "Lori Young referred me" reinforces the trust connection.

### Technical Architecture

**Brand:**
- Colors from claude.sethz.co: dark bg `#0A0A0A`, accent red `#E8453C`, amber `#FF6B35`
- Fonts: Sora (headings) + DM Sans (body)
- Matches the main Friction-Free OS landing page exactly

**Form submission:**
- On "Submit & Pick a Time" click → validates all required fields → saves form data → POSTs to Google Sheets via Google Apps Script web app URL → hides form → shows Cal.com step
- Google Sheets webhook URL placeholder: `YOUR_GOOGLE_APPS_SCRIPT_URL_HERE`
- Sheet headers: `name, email, phone, website, linkedin, referral, business, years, team, time_drains, magic_wand, ai_experience, submitted_at`

**Cal.com embed:**
- Loads on page load (not lazily) so the calendar is pre-rendered by the time the user reaches step 3
- Cal section is positioned offscreen (not `display:none`) to prevent iframe rendering issues
- Uses Sangeet's exact Cal.com embed code with `month_view` layout
- Cal link: `sangeet-seth-vcxo8u/frictionaudit`
- Min-height: 700px for comfortable month view rendering

**Validation:**
- Required fields: name, email, phone, referral, business description, time drains, magic wand
- Email format validation via regex
- Visual error state (red border) on invalid fields
- Auto-focus on first error field

**Privacy:**
- Privacy note at bottom of step 2: "Your responses stay private and are only used to prepare for our call."
- Lock icon SVG for visual trust signal

### Critique & Fixes Applied

The form went through a ruthless review. Issues identified and fixed:

1. ~~No backend~~ → Google Sheets webhook integration added
2. ~~No Cal.com redirect~~ → Cal.com embedded inline as step 3
3. ~~No phone field~~ → Phone/WhatsApp field added (required)
4. ~~Too many optional fields~~ → Critical fields made required, fluff cut
5. ~~Redundant "introduce yourself"~~ → Removed
6. ~~Chip selector limiting responses~~ → Replaced with free-text textarea
7. ~~No privacy signal~~ → Privacy note + lock icon added
8. ~~No data validation~~ → Client-side validation on all required fields + email format check
9. ~~Too many open-ended questions~~ → Trimmed from 4 to 2 key questions (time drains + magic wand)
10. ~~Pointless "how did you hear" for a known referral~~ → Kept for future reuse but deprioritized visually

---

## Files

| File | Description |
|---|---|
| `friction-audit-form-v2.html` | Production-ready intake form. Multi-step with Cal.com embed. Needs Google Apps Script URL to go live. |

---

## Next Steps

1. **Create Google Apps Script** — Write the doPost function, deploy as web app, paste URL into the form
2. **Host the form** — Deploy to Vercel or add as a page on claude.sethz.co (e.g., `claude.sethz.co/intake`)
3. **Send to Lori** — Share the form link + booking flow with Lori so she can forward to Nicole
4. **Pre-call research** — Once Nicole submits, research her website, LinkedIn, and VA agency before the friction audit call
5. **Run the friction audit** — Map Nicole's workflows across both businesses, identify top 5 time-wasters, score by Time × Pain × Automation Potential
6. **Scope and price** — After the audit, determine the right tier. Lori asked for a discount — decide on a friends-and-family rate based on actual scope. Floor: $1,500.

---

## Key Principles (from Friction-Free OS context)

- Never price below $1,500
- Never skip the friction audit — it IS the sales tool
- Never discuss pricing before understanding scope
- Lead with outcomes, not tools
- The audit makes the problem undeniable. 80% of prospects skip a sales call after receiving the audit because it already answers every question.