# Inbox Onboarding

*Everything you need for your first days on inbox duty. Work through each section in order, and check things off as you go.*

---

## Part 1 — Access

Ask for all of this at once, on day one. Half of it requires someone else to act, and the gaps don't surface until you're mid-reply to a student.

- [ ] **`liz@` mailbox access** — This *is* the inbox. Student mail, refund requests, escalations, the weekly schedule. The primary address you'll be working from. *Verify: You can read liz@ and compose as it*
- [ ] **`aethrix@` mailbox access** — Automated student mail lands here — receipts, enrollment, magic links, digests. The second monitored address. *Verify: You can read aethrix@ and compose as it*
- [ ] **Site account with admin flag** — Log in via magic link at [themultiverse.school/login](https://themultiverse.school/login). Once your account exists, Liz sets `admin = true` on your row so every `/admin/*` page works. *Verify: [/admin/dashboard](https://themultiverse.school/admin/dashboard) loads*
- [ ] **Matrix account + staff rooms** — Where students and staff actually talk. Sign in via Element, homeserver `matrix.themultiverse.school`. *Verify: You're in the staff room and can send a message*
- [ ] **Stripe dashboard (read-only)** — Confirming what someone actually paid, and under which email. Ask Liz for an Analyst invite. *Verify: You can find a charge from an email address*
- [ ] **Google Drive & Calendar** — Approving recording access requests and checking class times. *Verify: You can open a class recording folder and see this week's classes*

> Not your job, don't ask for it: Coolify, deploys, server access, Vaultwarden, SendGrid, GitHub, production DB tokens. Nothing in the inbox needs them.

---

## Part 2 — Reading List

Read in this order — each one assumes the last. The point is the takeaway, not finishing the document.

- [ ] **[INBOX_HANDBOOK.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/INBOX_HANDBOOK.md), sections 1–4** — What "done" means, which addresses are real, the five-minute mental model, and what to do when the mail isn't a support ticket. Section 4 is the one to have read before you need it.
- [ ] **[INBOX_HANDBOOK.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/INBOX_HANDBOOK.md), sections 5–9** — The FAQ, the lookup table, the escalation tree, and the map. Skim now, return constantly.
- [ ] **[MATRIX_STUDENT_SUPPORT.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/MATRIX_STUDENT_SUPPORT.md)** — The privacy ceiling and the two meanings of "verified". Also the best example of what a good runbook looks like.
- [ ] **[Student handbook repo](https://github.com/lizTheDeveloper/multiverse-admin-handbook)** — Skim the code of conduct and the emergency flowchart. Know it exists and roughly what's in it.
- [ ] **[Terms page](https://themultiverse.school/terms) & [/forms/scholarship](https://themultiverse.school/forms/scholarship)** — Read what we have actually promised students, in the words they read.
- [ ] **[OWNERSHIP_AREAS.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/OWNERSHIP_AREAS.md)** — Who to hand a thing to.
- [ ] **[GDPR_DATA_RETENTION.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/GDPR_DATA_RETENTION.md)** — What deletion deletes and what it keeps.
- [ ] **A tour of [/admin/*](https://themultiverse.school/admin/dashboard)** — Open every page in the handbook's lookup table once, so you've seen them before you need one in a hurry.

---

## Part 3 — Getting Your Hands Dirty

These aren't tests. They're things to try so you've seen them before a student asks about them. Someone will shadow you through your first inbox sessions, and you can always ask questions in the **Multiverse Operations** channel in Element.

> **Be curious.** Poke around the admin pages, look up real students, click the links students click. The whole point of the docs and tools is that you don't have to memorize anything — you just need to know where to look.

- [ ] **Look up a real student in [`/admin/student/<id>/crm`](https://themultiverse.school/admin/dashboard)** — Get a feel for what's there: what they bought, what they're enrolled in, what they can access. This is the page you'll live in.
- [ ] **Find a charge in Stripe from an email address** — Then find the same person in the CRM page. Getting comfortable moving between Stripe and our admin is the core skill.
- [ ] **Send yourself a durable classroom link and click it** — See what the student sees — the airlock page, the destination options. This is the link you'll send people constantly.
- [ ] **Find a class recording the way a student would** — Open a class's curriculum page and watch a video from it. Then open one that has *no* videos, so you know both shapes before someone describes one to you.
- [ ] **Draft a reply to a current email and run it by someone** — Pick one that looks interesting — a prospective student question, an access problem, whatever catches your eye. Share your draft in the operations channel before sending.
- [ ] **Read through the escalation paths in the [handbook](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/INBOX_HANDBOOK.md)** — Refunds go to Megs or Liz (Liz processes them). Campus issues go to Neek. Partnerships, enterprise requests, or custom classes go to Spencer. Crisis disclosures have a specific procedure (section 4). You don't need to memorize this — it's all in the Quick Ref and Triage sections here.

### Settling in

- [ ] **Notice what's hard to read, broken, or confusing** — If a link doesn't work, a page is hard to read, or you're seeing multiple students confused about the same thing — that's a pattern worth mentioning in the operations channel. You're seeing the site with fresh eyes right now.
- [ ] **Tell us when something doesn't match the docs** — You're the person best positioned to catch it — you're reading the handbook and looking at the real system at the same time. If something's off, say so in the operations channel. That's a contribution, not a complaint.

---

## Quick Reference

### The Addresses

Two mailboxes are monitored. That is the whole list.

| Address | What lands here |
|---|---|
| `liz@` | The default inbox. Student mail, refund requests (the terms name it), escalations, the weekly schedule. **Your primary mailbox.** |
| `aethrix@` | Automated student mail — receipts, enrollment, magic links, digests. The second monitored address. |

**Send-only addresses** (appear on From lines but are not inboxes):

| Address | What sends as it |
|---|---|
| `care@` | Mutual-aid resource packs and unmet-needs replies. Treat replies here with priority and care. |
| `matching@` | CRM intro and matching drafts. |

> **Give students `liz@` when they ask for a contact address.** `aethrix@` is the automated sender; `support@` is a forward, not a destination.

### The Five-Minute Mental Model

- **Stripe is the source of truth for enrollment.** Never fix an enrollment by editing a table directly — the batch job will overwrite it.
- **Three enrollment paths exist**, and a batch job sweeps every ~10 minutes as a safety net. So "I paid and nothing happened" is often ten minutes old and about to resolve itself.
- **Curriculum access comes from enrollment**, not from a per-student grant. A student can see a curriculum if they're enrolled in any class whose `curriculum_slug` matches.
- **Community chat is Matrix**, self-hosted. Students use the Element app. Homeserver: `matrix.themultiverse.school`. User IDs read `@name:themultiverse.school`.
- **The durable classroom link** is `/classroom/<class_id>` — permanent, always safe to send. Never paste a raw Google Meet URL.

### How to Look Things Up

All require admin on your account. In roughly the order you'll reach for them.

| What you need | Where |
|---|---|
| Everything about one student | [`/admin/student/<id>/crm`](https://themultiverse.school/admin/dashboard) |
| Their notes | [`/admin/student/<id>/notes`](https://themultiverse.school/admin/dashboard) |
| Did enrollment complete | [`/admin/enrollment-status`](https://themultiverse.school/admin/enrollment-status) |
| Resend a receipt | `/admin/student/<id>/resend-receipt` |
| Send a payment link | `/admin/student/<id>/send-payment-link` |
| Re-trigger enrollment email | `/admin/api/student/<id>/retrigger-email` |
| Enroll or unenroll by hand | [`/admin/enroll_student`](https://themultiverse.school/admin/enroll_student) |
| Scholarships | [`/admin/scholarships`](https://themultiverse.school/admin/scholarships) |
| Form submissions that failed to save | [`/admin/form-fallback`](https://themultiverse.school/admin/form-fallback) |
| Two accounts for one human | [`/admin/students/merge`](https://themultiverse.school/admin/students/merge) |
| Deletion request | `/admin/student/<id>/gdpr-delete` |
| Mutual aid queue | [`/admin/unmet-needs`](https://themultiverse.school/admin/unmet-needs) |
| Class and schedule admin | [`/admin/dashboard`](https://themultiverse.school/admin/dashboard) |

> **The admin dashboard has a database assistant tool.** If you need to look something up that isn't on one of the admin pages above, you can ask it a question in plain language and it will query the database for you.

### Voice & Small Rules

- Warm, specific, no corporate hedging. Say the true thing including when it's no. Sign off "See you in the Multiverse~"
- Match the register of what arrived. Someone writing "halp" wants a link and a friendly sentence, not a policy paragraph.
- **Never forward a magic link or auth token** to anyone but the account holder.
- **Check identity before repointing a record.** Someone writing from a different address is the most common support request and also what an account takeover looks like.
- **Don't fix enrollment by editing the database.** Stripe is the source of truth and the batch job will overwrite you.
- **Reply in the same channel they wrote from.** A student who can't read Matrix DMs is exactly the student you can't reach by Matrix DM.

---

## FAQ — Frequently Asked, With Answers

Ordered by how much mail each actually generates.

### The payment-email mismatch

**What the student says:** "I paid but never got the email." "Apple Pay used a different address." "My account is screwed up."

**What actually happened:** Checkout autofilled a different email than the one they use with us. Stripe is the source of truth, so enrollment attached to *that* email and created a second account.

**How to check:** Look them up by both addresses in [`/admin/student/<id>/crm`](https://themultiverse.school/admin/dashboard), and search Stripe by the payment email. Two accounts, one human.

**The fix:** Update the email on the existing account, or move the enrollment to the right account. [`/admin/students/merge`](https://themultiverse.school/admin/students/merge) when there are genuinely two records. Don't tell them to make a new account.

**Paste-ready reply:**
> "It looks like when you checked out, the payment was tied to [other address] — that created a second account. I've moved your enrollment onto [right address] and your class materials should be there now. You can log in at https://themultiverse.school/login. See you in the Multiverse~"

### "I paid and nothing happened"

Sometimes this is the email mismatch above. Sometimes it's the batch job, which sweeps every ~10 minutes.

**Check [`/admin/enrollment-status`](https://themultiverse.school/admin/enrollment-status) before doing anything.** If it stalled, `/admin/api/student/<id>/retrigger-email` resends.

Enrollment mail lands in spam often enough that "check your junk folder" is a real first question, not a brush-off.

### "How do I join class?" / "Send me the link"

One answer: **`https://themultiverse.school/classroom/<class_id>`**

That link is permanent. It never changes. Get the class id from the class page URL (`/classes/204` → `204`). It also records attendance when they go through during a live session.

They already have it — it's in the registration email, the weekly digest, and calendar invites. So "can you send me the link" is usually "I can't find the email."

**Never paste a raw Google Meet URL.** That is the problem this link exists to solve.

> **If the link doesn't work:** "Not enrolled" page → enrollment problem. Lands on campus home → known, harmless. "Nowhere to go" → no meeting link set, ours to fix.

### Recordings and materials

Recordings live inside the class's curriculum page at `/curriculum/<slug>/`. The answer is almost always **"it's in your class materials"** with a direct link.

**Check before promising:** Not every class has videos. Open the page yourself and look. And **do not send anyone to `/recordings`** — the archive page exists but the table is empty.

When a recording hasn't been attached yet and a student hits a "request access" wall on Drive: a non-Google email cannot be granted Drive access at all. Send the file another way, and get the recording attached to the materials.

### Purchasing past class recordings

Someone wants to pay for access to a class that has already finished — they want the recordings and curriculum materials, not a live seat.

**The process:**
1. Go to `/admin/classes/[class_id]/edit` → Pricing section → copy the **Stripe Payment Link** URL.
2. Send them the link. The checkout page is PWYC — they can adjust the amount down to the minimum (50% of suggested price, floor $100).
3. After payment, the Stripe webhook auto-enrolls them (even for past classes). Verify at `/student_list`.
4. If the webhook didn't fire (rare), enroll manually at [`/admin/enroll_student`](https://themultiverse.school/admin/enroll_student).

**Paste-ready reply:**
> "Great news — recordings and curriculum materials are available for [Class Name]. Recording access is Pay What You Can — you can adjust the amount on the checkout page. Here's your link:
>
> [Stripe payment link from /admin/classes/[id]/edit]
>
> Once your payment goes through, you'll be set up automatically and can access everything right away.
>
> See ya in the Multiverse~"

**Already paid?** Skip payment — enroll them at `/admin/enroll_student`. **Scholarship student?** Enroll them free. **Want multiple past classes?** Suggest the pathway subscription ($250/mo) which includes all recordings.

Full process doc: [Students Purchasing Past Class Recordings](https://claude.ai/code/artifact/e749a18f-3bc1-4241-9bf4-b563d1a51f7a). Self-serve feature tracked in [#1287](https://github.com/lizTheDeveloper/themultiverse.school/issues/1287).

### Scholarships

Largest label by volume, and mostly replies to automated mail, not applications.

- **"How do I join?"** → the scholarship form at [`/forms/scholarship`](https://themultiverse.school/forms/scholarship). Nobody is turned away for lack of funds.
- **"No scholarship seats available"** is deliberate friction. A student writing in about it has done the intended thing, not hit a wall. See section 8 of the [handbook](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/INBOX_HANDBOOK.md).
- **"I applied but was given standups"** — standups are the default scholarship award. Say so plainly; it reads as a mistake otherwise.
- **Payment plans** — flexibility: shift the date, or waive it. **Waivers and refunds go to Megs or Liz; Liz processes them.**
- **The contract's likeness clause** frightens people. Answer it warmly and quickly — students have sat blocked on this for weeks.

### Refunds, cancellations, transfers

**Refund questions go to Megs or Liz.** Liz is the one who processes them. You gather the facts and say what you see; you do not grant them.

- Full refund **before the class starts** — no questions asked.
- Full refund if class links or access never arrived.
- **Non-refundable once the class has begun.** Tuition goes to payroll.
- **Transfers:** to a future cohort of the same class, free, before start date.
- **Alumni re-attendance:** free, self-serve. "Rejoin as Alumni" on the dashboard.
- **Subscriptions** cancel from the Stripe billing portal; cancelling leaves dashboard access.

### Matrix and Element

Full runbook: [MATRIX_STUDENT_SUPPORT.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/MATRIX_STUDENT_SUPPORT.md). Three things to know:

- **"I can't get verified"** almost always means Element's encryption prompt, not us checking their enrollment.
- **Class rooms are unencrypted; DMs are encrypted.** A student who can't read DMs can still use class chat — and can't be helped by DM either.
- The homeserver is `matrix.themultiverse.school`; user IDs read `@name:themultiverse.school`. Typing the wrong one is a common login failure.

"I need an invite to the room" is usually enrollment, not Matrix.

### Magic links and login

24-hour expiry; a new one can always be requested. The mail comes from `aethrix@`. **Spam is the most common cause** of "I never got it."

### Class logistics

Live and online, recorded. 18+. No prerequisites for most classes. Sessions are Pacific time. Two people may share one enrollment. We are **not** Multiverse.io, the UK apprenticeship company.

### Campus troubleshooting — "I can't get in"

**If class is happening now:** send the durable classroom link and tell them to use the video call option. Diagnose after.

**Paste-ready reply:**
> "Here's the link for class: [link] — it'll offer you Campus and the video call. Use the video call for today so you don't miss anything, and let's sort out Campus after."

**The one question that sorts it:** "What exactly does it say on the screen — word for word?"

- "Camera and microphone are blocked" → **Theirs** — re-allow in browser settings
- "No camera or microphone found" → **Theirs** — hardware
- "In use by another app" → **Theirs** — close Zoom/Teams/FaceTime
- Multiple students at once in the same class → probably **ours**, escalate to Neek

---

## How We Handle Student Problems

> The most important thing is to **care about the human in front of you**. Help them first, figure out the rest after.

When something comes in, help the student, then mention it in the **Multiverse Operations** channel in Element. If you're seeing the same thing from multiple students, that's especially worth flagging — patterns are how we know what to fix next.

### What You Can Handle

Walking students through login, sending them a classroom link, looking up their enrollment status, answering questions about classes and scheduling, and anything where the answer is already in the FAQ section above.

### Escalate to Megs or Liz

- Anything involving **money or scholarships** (eligibility, refunds, scholarship records) — Liz processes refunds
- **Merging or deleting** student records or Matrix accounts
- Any case where you can't confidently identify the "real" account
- Anything you're not sure about — asking is always fine

> When you escalate, share **what you found and what you think**. "Here's what I'm seeing, here's what I'd do, does that sound right?" is a great way to learn and a great way to hand something off.

### Reading the Room

| Type | Examples | What to do |
|---|---|---|
| **Quick answer** | Is this for me? Are classes remote? Which class do I start with? | Use the FAQ section. Send without agonising. |
| **Lookup first** | They paid and got nothing, can't see materials, wrong email | Check the admin pages before you answer. Most of these have a specific cause and a specific fix. |
| **Hand off** | Refunds, anything irreversible, anything you're unsure about | Share what you found in the operations channel and escalate to Megs or Liz. |

### When You Don't Know

Say so, and say when you'll come back. **"I want to get this right — let me check and come back to you today"** is a complete, professional answer. The student is not comparing you to someone faster; they're comparing you to silence.

### Sensitive Disclosures

Scholarship and unmet-needs submissions describe food and housing instability. Treat them with care and discretion. Don't share details in chat — describe the shape of the problem, not the person.

If a student tells you they're in crisis: ask "are you safe right now?", share crisis resources (988 Suicide & Crisis Lifeline, Crisis Text Line: text HOME to 741741), and escalate to Liz. **You are not expected to handle this alone.**

---

## Who Owns What

Areas are assigned, not issues. When something needs to go to someone else, send it.

| Person | Areas |
|---|---|
| **Megs** | Money & enrollment. Community, mutual aid & comms. The enrollment pipeline, purchases, scholarship slots, receipts, the funnel. Contributor flows, outbound comms. |
| **Neek** | Auth, sessions & security. Jobs, infra & monitoring. Campus & game. The world, calls, agents, quests, deploys. |
| **Liz** | Curriculum & content. Site front end. Processes refunds, scholarship eligibility, merges, deletions, anything irreversible. |
| **Spencer** | New revenue, partnerships & enterprise. Custom class requests, enterprise inquiries, anything that opens a new money path rather than fixing an existing one. |

> **The short version:** Money → Megs or Liz (Liz processes refunds). Campus broken → Neek. Content → Liz. Partnerships, enterprise, or custom classes → Spencer. Everything else → Megs first, who'll redirect if needed.

### Key Addresses

| Address | Role |
|---|---|
| `liz@themultiverse.school` | The inbox. Student mail, refunds, escalations, weekly schedule. |
| `aethrix@themultiverse.school` | Automated student mail. Receipts, enrollment, magic links, digests. |
| `care@themultiverse.school` | Send-only. Mutual-aid replies. |
| `matching@themultiverse.school` | Send-only. CRM drafts. |

**Not real addresses** despite appearing in old docs: `teacher@`, `admin@`, `security@`, `noreply@`. If you find one being advertised, that's a bug.

### Key Docs Map

All of these live in the `docs/` directory of the [school repo](https://github.com/lizTheDeveloper/themultiverse.school/tree/production/docs).

| Doc | Use it for |
|---|---|
| [INBOX_HANDBOOK.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/INBOX_HANDBOOK.md) | The daily reference. FAQ, lookups, voice, escalation. |
| [ENROLLMENT_ARCHITECTURE.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/ENROLLMENT_ARCHITECTURE.md) | Why enrollment is fragile and the three paths. |
| [MATRIX_STUDENT_SUPPORT.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/MATRIX_STUDENT_SUPPORT.md) | Matrix/Element runbook. |
| [BAD_FAITH_TRIAGE.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/BAD_FAITH_TRIAGE.md) | When you start suspecting the person. |
| [OWNERSHIP_AREAS.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/OWNERSHIP_AREAS.md) | Who to hand a thing to. |
| [GDPR_DATA_RETENTION.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/GDPR_DATA_RETENTION.md) | What deletion deletes. |
| [CLASSROOM_DURABLE_LINK.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/CLASSROOM_DURABLE_LINK.md) | The permanent classroom link. |
| [AUTHENTICATION.md](https://github.com/lizTheDeveloper/themultiverse.school/blob/production/docs/AUTHENTICATION.md) | Magic links, sessions, how login works. |
