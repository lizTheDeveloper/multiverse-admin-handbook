# The Email Inbox

**Where**: [`/admin/email`](https://themultiverse.school/admin/email), from the Ops tab on [Admin Home](ADMIN_HOME.md) or **Every screen → Email**.

One admin page for answering the mail to `liz@` and `aethrix@`, and for finding out what
happened to a student's email. It reads the cases the inbox agent stores, and decides through
the same route as the review queue at `/admin/inbox-agent`, so the two pages can never disagree.

**For:** Ivy, Angela, Liz, and anyone working the inbox.

## The tabs

| Tab | What it's for |
|---|---|
| **Inbox** | The queue: Needs you, Waiting on them, Crisis, For someone else, Answered automatically, Done, Skipped. Open an email to see who wrote, what they bought and attended, their email settings, what we sent them, and the drafted reply. |
| **Unsubscribes** | Who turned email off, when, and how. Change a student's settings here; every change is logged as made by an admin. |
| **Journey** | Find a student by name, number or any address they've used. "Should they have received this?" for five emails, their messages, and their whole time with us. |
| **Delivery** | Who SendGrid won't deliver to: bounces, blocks, spam reports, invalid addresses and global unsubscribes. Also a read-only Stripe search by email. |
| **Repeats** | Which kinds of email keep coming in, and how long they take to answer. A repeating kind can be filed as one ticket. |
| **Reports** | Leadership, Teachers, Operations and Engineering views. All read-only. |

Each tab has its own link, for example `/admin/email#journey-student-123` or
`/admin/email#reports-leadership`.

## Answering an email

1. Open it from **Needs you**. The newest in the list is not always the most urgent: anything
   flagged **Crisis** comes first.
2. **Claim it** if you're going to work on it, so nobody else drafts the same reply. A claim is
   advice, not a lock: anyone can still answer, and **Take it over** moves it to you.
3. Read the panel before the draft. **Who this is**, **Purchases and attendance** and **Email
   settings** usually answer the question before you write anything.
4. Approve the reply, edit it first, or choose **Don't send this reply**. The button says what
   will happen in the current mode (Practice, Drafts or Live).
5. If you've asked them something and are waiting for an answer, use **Waiting on them**. The
   email leaves Needs you, and comes back on its own when they write back in the same thread.

**"Stop emailing me" mail** is sorted as its own kind and always waits for a person, in every
mode. The panel links to that student's settings on **Unsubscribes**, and nothing is turned off
until you do it there.

## What the answers mean

On the Journey, each of five emails gets one answer:

| Answer | Meaning |
|---|---|
| **Marked sent** | Our job marked it sent. That isn't proof it arrived; **Can we reach them?** says what SendGrid knows. |
| **Missing** | It should have gone by now, and hasn't been marked sent. |
| **Not due** | It isn't time yet, they don't qualify, or the job may not have run yet. |
| **Opted out** | That setting is off, whoever turned it off. Only the weekly schedule has a setting. |
| **Can't tell** | We don't have what we'd need to judge. Never read this as fine. |

Missing and Can't tell also show **What to do**, **What we found** and **What we don't know**.
What we found is only what the page can see, such as a failed step, a missing saved receipt or
a job's last run. It never guesses at a cause.

**Receipts read Missing on most recent purchases.** That's real, and it's tracked in #1860:
our own receipt job has been skipping most purchases since April. Whether buyers get a receipt
from Stripe instead is still being checked. Until then, nothing needs doing for one student
unless they ask; if they do, open Student CRM and send them the purchase's **View** link.

**To check whether any email went out**, not just these five, use [Sent emails](ADMIN_HOME.md#sent-emails).

## Filing a ticket

Every Missing or Can't tell answer, every email, a repeating kind of email, and a failed
SendGrid update can be filed as a ticket. A ticket always has the same parts: what we found,
what we don't know, what I tried, and how this would stop needing a human.

- **File a ticket** puts it on GitHub for you and names you as the filer, when the server has a
  bot token.
- Without the token, or on a preview, the page says so. Use **Copy ticket text**, or **Open it
  on GitHub** if you're signed in there.

**Never put crisis or mutual aid details in a ticket**, even by typing them in afterwards.
Tickets name a student by number only, and addresses are removed from what the page puts in.

## The reply target

Liz set it at **2 business days**, Monday to Friday, Pacific time. **Reports → Leadership**
flags any email waiting longer than that for a reply from us. Holidays aren't skipped yet.

## What the page keeps private

- No email text in any list. Crisis and mutual aid mail shows no sender or subject until it's
  opened, and a crisis message's text only loads when someone asks for it.
- Unverified senders get no student record, and aren't tied to a student in a ticket.
- Erased students never appear anywhere on the page.
- Reports show counts only, and never compare staff with each other. Teacher counts under 3
  show as "a few", so a small class can't identify who wrote in.
