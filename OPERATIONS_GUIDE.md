# Operations Guide: How to Actually Use the System

This is the hands-on companion to the rest of the handbook. It covers what each admin tool does, when you'd use it, and the things that aren't obvious.

**You don't need to read this top to bottom.** Jump to the section you need.

---

## Student List

**Where**: `/student_list` (from the Admin tab → "Student List")

### Finding students

Type a name or email in the search box — it searches both fields, case-insensitive. Use the report-type filters for quick views:

| Filter | What it shows |
|---|---|
| All | Every student ever, newest first |
| Active | Enrolled in upcoming classes, active membership, scholarship, or researcher |
| Scholarship | Only scholarship recipients |
| Expelled | The ban list (students with `is_expelled`) |
| Membership | Members with active subscriptions |
| By Class | Students in a specific class (select from dropdown) |

Results are paginated at 50 per page.

### Editing a student

Click into a student and you can edit these fields inline — changes save immediately:

- **Name, email, pronouns, phone, timezone**
- **Membership level** — the subscription tier. Don't change this manually unless you know what you're doing; the enrollment pipeline manages it.
- **Scholarship** — toggle scholarship status on/off
- **Support tier** — supporter/sustainer/patron
- **Tuition rate** — custom rate (for sliding scale)

### Per-student actions

From a student's profile, you can:

- **Enroll in a class** — dropdown of upcoming classes, instant enrollment
- **View enrollments** — see what they're enrolled in and whether welcome emails were sent
- **Re-trigger welcome email** — if they never got their welcome email
- **Unenroll** — remove from a class (creates a withdrawal record for audit)
- **Expel** — sets `is_expelled` with a reason and timestamp. Can be undone. The student is blocked from new enrollments and excluded from weekly emails.
- **GDPR delete** — anonymises the record (irreversible)

### Associated emails

Students can log in with multiple email addresses. They add new ones from their profile; a confirmation link is sent. You can also add associated emails directly from the admin student edit page. This matters because enrollment matches on email — if someone buys with `jane@gmail.com` but their account is `jane@work.com`, the enrollment won't find them until the emails are associated.

---

## DB Assistant

**Where**: `/admin/db-assistant` (from the Admin tab → "DB Assistant")

### What it is

A chat interface where you ask questions about the database in plain English. An AI writes and runs SQL for you.

**Examples of things you can ask:**
- "How many students enrolled this month?"
- "Show me all scholarship students who haven't attended in 30 days"
- "What classes does student jane@example.com have?"
- "What's our MRR broken down by support tier?"

### Safety rails

- **Reads are instant** — SELECT queries run immediately and show results
- **Writes get a dry-run first** — UPDATEs show you what rows would change and ask for confirmation before executing
- **Deletes use mark-and-sweep** — nothing is deleted immediately. Records are snapshotted and scheduled for removal after a grace period (7 days by default). You can undo a pending deletion.
- **Dangerous operations are blocked** — DROP, ALTER, TRUNCATE, CREATE, GRANT, etc. are forbidden
- **Everything is audit-logged** — every query goes to the audit log

### When to use it

Use the DB Assistant when you need information that isn't on a dashboard, or when you need a one-off data fix. Don't use it for routine work that has its own admin page (enrollment, scholarships, etc.) — those pages have their own safety checks.

---

## Financial Dashboard

**Where**: `/admin/financials` (from the Admin tab → "Financial Transparency")

Faculty and admins both have access. Admins also get the costs editor.

### Key sections to pay attention to

**Summary** (top): Total revenue in four time windows — last 24 hours, week-to-date, month-to-date, and all-time. Quick pulse check.

**MRR**: Monthly recurring revenue from active subscriptions. This is the number that matters most for sustainability.

**Class financials**: Revenue per class run, broken down by time window. Tells you which classes are earning and which aren't.

**Class run comparison**: Same class across different cohorts — is revenue trending up or down?

**Membership breakdown**: How many students are at each membership level. Watch for concentration risk (too many at one level).

**Scholarships**: How many scholarship students and the implied value of their scholarships.

**Revenue month-over-month / week-over-week**: Trend lines. Are things growing?

**Visit funnel**: Visit → signup → purchase conversion. Where are people dropping off?

**LTV and cohorts**: Long-term value and retention. How well do we keep people?

### Reading the numbers

- All revenue is in dollars (the database stores cents; the dashboard converts)
- Time windows use Pacific time
- If a section errors, the others still render — one broken section doesn't take down the page

### Costs editor (admin only)

At `/admin/financials/costs`, admins can manage:
- **Compensation** — payroll and contractor payments
- **Platform costs** — SaaS subscriptions (hosting, email, etc.)
- **Other income** — revenue from sources other than Stripe
- **Financial goals** — targets and progress tracking

---

## Scholarship Queue

**Where**: `/admin/scholarships` (from the Admin tab → "Scholarship Queue")

### Reviewing applications

Applications come in from the scholarship form. The queue has tabs:
- **Pending** — new applications waiting for review
- **Approved** — granted
- **Declined** — rejected

Search by name or email, filter by month.

### What happens when you grant a scholarship

When you approve and grant a scholarship:
1. The student's account gets `scholarship = TRUE`
2. They're enrolled in the classes you select
3. They get a track pass if their pathway can be determined from the application
4. A welcome email goes out

### Other actions

- **Send payment link** — for reduced-rate scholarships (student pays something)
- **Send coupon** — one-time discount code
- **Send payment plan** — weekly payment plan via Stripe
- **Enroll without scholarship** — direct enrollment, no scholarship flag

### Attendance gates

Scholarship students have participation requirements:
- They need to attend Job Search standup (or Learn to Code drop-in) regularly
- Falling below the attendance threshold → `scholarship_suspended = TRUE` → access pauses
- They get back in by re-engaging

The dashboard shows attendance data. Suspension logic runs automatically in background jobs — you don't need to manually suspend anyone.

### Capacity view

The capacity panel shows paid vs. scholarship counts per class and how many funded slots are available. This helps you make grant decisions without overcommitting.

---

## Enrollment Status

**Where**: `/admin/enrollment-status` (from the Admin tab → "Enrollment Status")

### Global health view (default)

Shows the enrollment pipeline's vital signs:
- **Purchase counts** — how many purchases in the last 24h, 7d, 30d
- **Success rate** — fully enrolled vs. failed vs. partial
- **Failing phases** — WHERE in the pipeline things are breaking (email send, calendar invite, Matrix room, etc.)
- **Recent failures** — specific errors with messages

### Student journey view

Add `?student_id=N` to see a specific student's enrollment history — every purchase, which phases completed, which failed, error messages, and attempt counts. You can get here by clicking from the student list.

### Retry button

Failed enrollments can be retried from this page. The retry re-processes the failed event through the enrollment pipeline.

### When to check it

- After a batch of new signups, to confirm they all enrolled cleanly
- When a student reports they never got their welcome email or class links
- When the enrollment batch job reports failures
- As a daily health check

---

## Class Creation

**Where**: `/admin/create_class` (from the Teachers tab → "Create Class")

Both faculty and admins can create classes. Faculty only see their own previous classes for reposting; admins see all.

### Repost from existing

The fastest way to create a new cohort: select a previous class and clone its settings. Everything copies — name, description, curriculum slug, meeting link, Stripe product, email template. You just update the dates.

### Minimum viable class

A class needs at minimum:
- **Name**
- **At least one scheduled session** (date + time)
- **Curriculum slug** (links to the course materials)

For a class to be fully functional, it should also have:
- **Teacher** assigned
- **Registration email template** configured
- **Meeting link** (Google Meet or Zoom)
- **Stripe product** for payment

Use the [Class Health](#class-health) page to verify everything's set up.

---

## Community Resource Submissions

**Where**: `/admin/community/submissions` (from the Community tab)

### What you see

Community members submit resources to the library. Each submission shows:
- Resource name, URL, category, and region
- **AI verification results** — confidence score, category match, government-resource flag, notes
- Contributor email and trust level

### Moderation actions

Three choices per submission:
- **Accept** — adds the resource to the public library (with automatic duplicate checking). Updates the contributor's trust score.
- **Reject** — marks as rejected
- **Needs info** — sends back for more detail

The page also shows **open flags** — issues community members reported with existing resources.

---

## Manual Enrollment

**Where**: `/admin/enroll_student` (from the Admin tab → "Manual Enrollment")

Enter an email address and optionally select a class:
- **Email only** — creates the student account (if it doesn't exist)
- **Email + class** — creates the account AND enrolls in the class

### When to use it

- Comp enrollments (free access without Stripe)
- Scholarship recipients who need manual setup
- Fixing enrollment failures where the webhook didn't fire
- Creating accounts for people who need dashboard access but aren't buying a class

### Important gotcha

Manual enrollment bypasses Stripe. The student won't have a purchase record, which means the batch job can't process membership updates, calendar invites, or receipts through the normal pipeline. For those, you'll need to handle them separately or use the student profile to trigger them.

---

## Merge Duplicates

**Where**: `/admin/students/merge` (from the Admin tab → "Merge Duplicates")

### When to use it

When one person has two accounts — usually because they bought classes with different email addresses, or the enrollment pipeline created a duplicate.

### How it works

1. Enter two student IDs
2. The system shows a **preview** of exactly what will happen — which record survives, what data moves, which enrollments transfer
3. Confirm the merge
4. **What you saw in the preview is what runs** — no surprises

The lower ID always wins. Its field values are kept; blanks get filled from the other account. Enrollments, purchases, and other references are moved to the surviving record. The merge is logged in the `student_merges` table for audit.

---

## Class Health

**Where**: `/admin/program-health` (from the Admin tab → "Class Health")

### What it checks

For every upcoming class, the system runs readiness checks:
- **Registration email** — is the welcome email template configured?
- **Lifecycle emails** — is the email automation set up?
- **Curriculum slug** — is the class linked to course materials?
- **Teacher** — is an instructor assigned?
- **Meeting link** — is there a Google Meet or Zoom link?
- **Stripe product** — can students pay for this?

Status is either `ready` (all good) or `warnings` (something's missing).

### Other panels

- **Portfolio** — per-cohort enrollment counts, revenue, and dates
- **Rerun candidates** — classes that ran before but have no upcoming cohort (consider rescheduling?)
- **Capacity plan** — the next ~6 weeks of scheduling recommendations
- **Draft cohorts** — rescheduled classes not yet published

---

## Orientation Videos

**Where**: `/admin/orientation`

Each learning path can have its own orientation video. Students see their path's video (or a general fallback) on their dashboard and at URLs like `/orientation/build-ai-systems`.

Just paste a Loom video ID — changes take effect immediately, no deploy needed.

---

## Job Monitor

**Where**: `/admin/jobs` (from the Admin tab)

### What it shows

The job monitor tracks every background job in the system — the enrollment pipeline, email sends, calendar syncs, membership updates, and more.

- **Run history** — when each job last ran, how long it took, whether it succeeded
- **Active jobs** — what's running right now
- **Schedules** — when each job is set to run next

### When to check it

- If enrollment emails aren't going out
- If calendar invites aren't being sent
- If the enrollment batch job (FEP) seems stuck
- As part of a daily operations check

---

## Quick Reference: "How Do I..."

| Task | Where to go |
|---|---|
| Find a student | `/student_list` → search by name or email |
| Check if someone is enrolled | Student list → click student → view enrollments |
| Enroll someone for free | `/admin/enroll_student` → enter email + class |
| Grant a scholarship | `/admin/scholarships` → find application → grant |
| Check why enrollment failed | `/admin/enrollment-status` → look at failing phases |
| See revenue this month | `/admin/financials` → top summary (MTD) |
| Check if a class is ready to run | `/admin/program-health` → check readiness status |
| Merge duplicate accounts | `/admin/students/merge` → enter two IDs → preview → confirm |
| Moderate a community resource | `/admin/community/submissions` → accept/reject |
| Ask a data question | `/admin/db-assistant` → type your question |
| Remove a harmful student | Student list → find student → expel (with reason) |
| Check scholarship attendance | `/admin/scholarships` → view student's attendance data |
| Create a new class cohort | `/admin/create_class` → repost from existing |
| Set an orientation video | `/admin/orientation` → paste Loom ID |
| Check background jobs | `/admin/jobs` → view run history and active jobs |

---

**Version 2.0** | September 2026
