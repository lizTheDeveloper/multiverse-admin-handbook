# Inbox Playbook

*You have an email open. Find what the student is asking below, and follow the steps. Each one tells you where to click, what you should see, what to write back, and when to hand it to someone else.*

New to the inbox? Read [Inbox Onboarding](inbox-onboarding.md) first. It explains *why* things work the way they do. This page is only *how*.

---

## Find the email you got

| The student says something like… | Go to |
|---|---|
| "I paid but I can't see my class" · "I never got the welcome email" | [Paid but no class](#paid-but-no-class) |
| "I paid with a different email" · "My account is messed up" | [Two emails, two accounts](#two-emails-two-accounts) |
| "I can't log in" · "The login link didn't come" | [Can't log in](#cant-log-in) |
| "How do I join class?" · "Send me the link" · "The link doesn't work" | [Class link](#class-link) |
| "Can you resend my receipt?" · "I need an invoice" | [Resend a receipt](#resend-a-receipt) |
| "Can you add me to the class?" (no payment, staff approved it) | [Add someone to a class](#add-someone-to-a-class) |
| "Please take me out of the class" | [Remove someone from a class](#remove-someone-from-a-class) |
| "I want a scholarship" · "What happened with my application?" | [Scholarships](#scholarships) |
| "Can I pay a different amount?" · "Send me a payment link" | [Payment links](#payment-links) |
| "I want a refund" | [Refunds](#refunds) |
| "Delete my account" · "Remove my data" | [Delete an account](#delete-an-account) |
| "I filled in the form but it didn't work" | [A form didn't go through](#a-form-didnt-go-through) |
| "Where is the recording?" | [Recordings](#recordings) |
| Anything about not being safe, not having food or housing | [Someone is not safe](#someone-is-not-safe) |

---

## Before every reply

1. **Look the student up first.** Almost every answer is on their student page. See [Find a student](#find-a-student).
2. **Write a note when you change something.** Their student page has an **Admin Notes** box. One line is enough: what they asked, what you did.
3. **Reply from the same place they wrote from.** Email gets email. Matrix gets Matrix.
4. **If you need Liz or Megs, the student still gets a reply today.** They are in Pacific time, so they are often asleep while you work. Send the holding reply below, then post in the **Multiverse Operations** channel in Element.

**Holding reply** (use this any time you are waiting on someone):

> Hi [name], thank you for writing. I've looked into this and I'm checking one thing with the team so I get it right. You'll hear back from me within one working day. See you in the Multiverse~

**When you post in the Operations channel**, include: the student's ID number, what they asked, what you found, and what you think should happen. Do not paste their personal details (address, health, money troubles). The ID number is enough.

---

## Find a student

You'll do this for almost every email.

1. Open the [Admin Dashboard](https://themultiverse.school/admin/dashboard) → **Admin** tab → **Student List**.
   Or go straight to [themultiverse.school/student_list](https://themultiverse.school/student_list).
2. Type their name or email into **Search by name or email…** and click **Search**.
3. In the **ID** column, click the small **CRM** link. This is their student page.

**If you can't find them:**

- Search only checks their *main* email. Try their name, or part of the email (for example, just `jsmith`).
- Try the email they used to pay. Ask the student for it if you need to. It is in their payment receipt from Stripe.
- Still nothing? They may have never made an account. That's normal for someone who hasn't bought anything yet.

**What's on the student page** (top to bottom):

| Section | Tells you |
|---|---|
| Header | Name, email, ID number, membership, scholarship badge. Buttons: **Edit Profile**, **GDPR Delete** |
| **Admin Notes** | What other staff did before you. **Read this first.** |
| **Timeline** | Everything that happened to them, newest first. Use the filter buttons (Enrollment, Purchase, Email, Auth…) |
| **Emails** | The last 50 emails we sent them, and to which address |
| **Classes Taken** | Their classes, and how many sessions they attended |
| **Purchases** | What they paid for, with a **Resend Receipt** button |

---

## Paid but no class

*"I paid but I can't see my class." "I never got the welcome email."*

**Check:**

1. [Find the student](#find-a-student) and open their student page.
2. Look at **Purchases**. Is the payment there?
   - **No payment** → they probably paid with a different email. Go to [Two emails, two accounts](#two-emails-two-accounts).
3. Look at **Classes Taken**. Is the class there?
4. Look at **Emails**. Was a welcome email sent? To which address?

**What you see → what to do:**

| You see | Do this |
|---|---|
| Payment ✓, class ✓, welcome email sent ✓ | It's in their spam folder, or they're looking at a different inbox. Send **Reply A**. |
| Payment ✓, class ✓, no welcome email | Send **Reply A** with the class link (see [Class link](#class-link)) so they are not blocked. Then post in Operations: the welcome email needs to be re-sent, and there's no button for that yet. |
| Payment ✓, class ✗, paid in the last 15 minutes | The system adds people every 10 minutes. Wait 15 minutes and check again. |
| Payment ✓, class ✗, paid more than 15 minutes ago | Check the enrollment status page (steps below). |

**Check the enrollment status page:**

1. Go to [Enrollment Status](https://themultiverse.school/admin/enrollment-status).
2. Find the student's name under **Recent Enrollments** or **Recent Failures** and click it.
   If they aren't listed, type this into your address bar, using their ID number:
   `themultiverse.school/admin/enrollment-status?student_id=12345`
3. You'll see a table of steps for their purchase. Each step says **Success**, **Failed**, **Skipped** or **Pending**.
4. If any step says **Failed**, click **Retry All Failed**.
5. Retry does **not** happen right away. The system tries again on its next run, within about 10 minutes. Come back and check. There is no "success" message.
6. If it fails again, post in Operations with the student ID and the words in the **Error** column.

**Reply A:**

> Hi [name], you're all set for [class name]! Your welcome email went to [email]. It sometimes lands in spam or Promotions, so please check there. Here's your link to class: [classroom link]. You can also log in any time at https://themultiverse.school/login to see your class materials. See you in the Multiverse~

---

## Two emails, two accounts

*"I paid with a different email." "Apple Pay used my old address." "My account is messed up."*

This is the most common email we get. Checkout filled in a different email than the one they use with us, so the payment went to a second account.

**Check:**

1. [Search](#find-a-student) for **both** emails. Write down both ID numbers.
2. Make sure it really is the same person (same name, and they wrote from one of the two addresses). **If you are not sure, stop and ask in Operations.** Someone asking to move an account to a new email is also what an account theft looks like.

**What you see → what to do:**

| You see | Do this |
|---|---|
| Only **one** account exists, and they want to log in with another email too | Add the second email to their account (steps below). Send **Reply B**. |
| **Two** accounts exist | These need to be merged. **Liz does merges.** Prepare the preview (steps below), then post in Operations. Send the holding reply. |

**Add a second email to one account:**

1. On their student page, click **Edit Profile**.
2. Find the box called **Login emails**. (It is written as if to the student. That's fine.)
3. Under **Add another email**, type the email and click **Add**.
4. You should see **"Associated email added."** The email now appears in the list.
   - If it says **"That email is already linked to an account"**, there are two accounts. Go back to the table above.
5. Write an admin note: "Added [email] as a login email, at student's request."

**Prepare a merge for Liz:**

1. Go to [Merge Duplicates](https://themultiverse.school/admin/students/merge).
2. Enter the two ID numbers and click **Preview the merge →**. Nothing changes yet.
3. Read the preview. The account with the **lower** ID number is kept.
4. **Do not click Merge.** Post in Operations: "Merge needed: [ID] and [ID], same person, wrote from [which address]. Preview looks clean / shows a warning: [warning]."

**Reply B:**

> Hi [name], thanks for your patience! Your payment came through under [other email], so I've connected that address to your account. You can now log in with either email at https://themultiverse.school/login and your class will be there. See you in the Multiverse~

---

## Can't log in

*"I can't log in." "The login link didn't come." "The link says expired."*

We don't use passwords. Students type their email at the login page and we email them a link. The link works for 24 hours.

**Check:**

1. [Find the student](#find-a-student). Does an account exist with the email they are typing?
   - **No** → they may be using a different email. Ask which emails they might have used. If they have an account under another email, [add this one to it](#two-emails-two-accounts).
2. On their student page, open **Timeline** and click the **Auth** filter. You can see if login emails were sent.

**What you see → what to do:**

| You see | Do this |
|---|---|
| Login emails were sent | It's in spam, or the link expired. Send **Reply C**. |
| No login emails at all | They may be mistyping the email. Ask them to copy it from your reply. Send **Reply C**. |
| They tried more than 3 times in an hour | They are rate-limited. Ask them to wait one hour, then try once. |

**Sending a login link for them:** there is no admin button for this. If they really need one:

1. Open a **private / incognito window** (if you are logged in, the login page sends you to your own dashboard instead).
2. Go to [themultiverse.school/login](https://themultiverse.school/login), choose **Magic Link**, type **their** email, click **Send Magic Link**.
3. The page always says **"Magic Link Sent!"**, even if the email is wrong. Check their **Timeline → Auth** to make sure it really went.
4. **Never forward a login link to anyone.** It only goes to the student's own inbox.

**Reply C:**

> Hi [name], login links come from aethrix@themultiverse.school and often land in spam, so please check there and mark it "not spam". Each link works for 24 hours. To get a fresh one, go to https://themultiverse.school/login and enter [email] (copy it from here so there are no typos). See you in the Multiverse~

---

## Class link

*"How do I join class?" "Send me the link." "The link doesn't work."*

Every class has **one permanent link** that never changes. Always send this one. **Never send a Google Meet link.**

**Find the link:**

1. Open the [Admin Dashboard](https://themultiverse.school/admin/dashboard) → **Teachers** tab → **Upcoming Classes**.
2. Click the class name. This opens the class editor.
3. Find the **Meeting Link** field. Under it is **Durable link** with a **Copy** button. Click **Copy**.

It looks like: `https://themultiverse.school/classroom/204`. The number is the class ID.

**If they say the link doesn't work**, ask them what the page says:

| The page says | Means | Do this |
|---|---|---|
| "You're not in [class] yet" | They are logged in with a different email than they enrolled with, or they are not enrolled | Check [Paid but no class](#paid-but-no-class) and [Two emails](#two-emails-two-accounts) |
| A login page | They are not logged in | Send [Reply C](#cant-log-in) |
| Nowhere to go / no meeting | The class has no meeting link set. **Our problem.** | Post in Operations right away, especially if class is today |

Testing the link yourself won't tell you much: admins always get through.

**Reply D:**

> Hi [name], here's your link for [class name]: [link]. It's the same link every week, so you can bookmark it. Log in with [email] first and it'll take you straight in. See you in the Multiverse~

---

## Resend a receipt

*"Can you resend my receipt?" "I need an invoice for my employer."*

1. [Find the student](#find-a-student) → student page → **Purchases**.
2. In the **Resend Receipt** box, choose **Send to email** and the **Purchase**.
3. Click **Send Receipt**, then confirm.
4. You should see **"Receipt sent to [email]"**. A note is added for you automatically.

If the purchase says **(no receipt available)**, post in Operations.

**Reply E:**

> Hi [name], I've just re-sent your receipt for [class] to [email]. It comes from aethrix@themultiverse.school, so check spam if you don't see it in a few minutes. See you in the Multiverse~

---

## Add someone to a class

*Only when staff has approved a free seat (a comp). If they want to pay, see [Payment links](#payment-links).*

1. Open [Manual Enrollment](https://themultiverse.school/admin/enroll_student).
2. **Class:** pick the class. Check the date: the list includes old classes too.
3. **Student Email:** type their email. If they have no account, one is made for them.
4. Click **Enroll Student**.
5. You should see **"Successfully enrolled [email] in [class]"**, and a row saying **Email sent**.
   - If it says **No email template**, the welcome email did not go out. Send them [Reply D](#class-link) with the class link yourself.
6. Write an admin note on their student page: who approved the free seat.

---

## Remove someone from a class

1. [Find the student](#find-a-student) → student page → **Classes Taken**.
2. Click **Unenroll** next to the class. Type a short reason and confirm.
3. You should see **"Student unenrolled"**.

**This does not refund money.** If they paid and want money back, see [Refunds](#refunds).

---

## Scholarships

*"I want a scholarship." "What happened with my application?" "Why did I get standups instead of a class?"*

**Answering questions** (you can do this):

| They ask | Answer |
|---|---|
| How do I apply? | Send them to [themultiverse.school/forms/scholarship](https://themultiverse.school/forms/scholarship). Nobody is turned away for lack of money. |
| I got standups, not a class | That's normal. Standups are the usual first award. Say so warmly so it doesn't feel like a mistake. |
| "No scholarship seats available" | They did the right thing by writing in. Post in Operations. |
| What happened to my application? | Look it up (below) and tell them its status. |

**Looking up an application:**

1. Open the [Scholarship Queue](https://themultiverse.school/admin/scholarships).
2. Search their name or email. The buttons at the top filter by **Pending**, **Approved**, **Declined**.

**Granting and declining:** **Liz decides scholarships.** Don't click **Grant** or **Decline**. Note that **Decline** sends no email and asks no "are you sure?". Post in Operations with the applicant's ID and status.

**This page is very private.** It shows people's housing, food, money and personal details. Don't copy any of it into chat or screenshots.

---

## Payment links

*"Can I pay a different amount?" "Can I pay in parts?" "Send me a link to pay."*

Changing the price is a money decision. **Megs or Liz decide.** Send the holding reply, then post in Operations: who, which class, what they asked for.

Once it's approved, for **scholarship students**: open the [Scholarship Queue](https://themultiverse.school/admin/scholarships), find them, click **Send Payment Link**, fill in **For** and **Amount ($)**, click **Send**.

For everyone else, there is no working button yet. (The **Custom Tuition Links** box on the student page does not send anything.) Megs or Liz will send it.

---

## Refunds

*"I want a refund." "Can I cancel?"*

**You never grant refunds.** Liz processes them. Your job is to collect the facts so she can decide fast.

1. [Find the student](#find-a-student). Note: what they paid for, when, and whether the class has started.
2. Check the rule (from the [terms](https://themultiverse.school/terms)):
   - **Before the class starts:** full refund, no questions.
   - **Never got access or links:** full refund.
   - **After the class has started:** no refund. They can move to a future group of the same class for free, if they ask before it starts.
3. Send the holding reply.
4. Post in Operations: "Refund request: [ID], [class], paid [date], class starts/started [date], their reason: [one line]."

**Never mention cancelling to someone who hasn't asked about it.**

---

## Delete an account

*"Delete my account." "Remove my data."*

**Liz handles deletions.** Deleting cancels their subscriptions and cannot be undone after 7 days.

1. Make sure the email came **from the account's own email address.** If not, ask them to write from that address.
2. [Find the student](#find-a-student) and note their ID.
3. Send the holding reply.
4. Post in Operations: "Deletion request from [ID], sent from their account email."

---

## A form didn't go through

*"I filled in the form but got an error." "I applied but never heard back."*

When a form fails to save, we keep a copy.

1. Open [Form submission recovery](https://themultiverse.school/admin/form-fallback). (It is not on the dashboard. Bookmark it.)
2. Find their email in the list. The **Form** column says which form.
3. Reply to the student: tell them we have it and what happens next. If they need to fill it in again, send them the link.
4. Click **Resolve** on that row.

If the list says **"No unresolved form submissions"**, their form saved fine. Look it up in the normal place (for example, the [Scholarship Queue](https://themultiverse.school/admin/scholarships)).

---

## Recordings

*"Where is the recording?" "I missed class."*

1. Recordings are inside the class's materials. To find them: [Admin Dashboard](https://themultiverse.school/admin/dashboard) → **Teachers** tab → **Upcoming Classes** → click **🎛️ Hub** next to the class → **View as student**. Copy that page's address to send to the student.
2. **Open it and check before you promise.** Not every class has videos.
3. Do **not** send people to `/recordings`. That page is empty.
4. If the recording is missing, post in Operations with the class name and date.

**Reply F:**

> Hi [name], the recordings are in your class materials here: [link]. Log in with [email] and scroll to [session]. See you in the Multiverse~

---

## Someone is not safe

*Anything about wanting to hurt themselves, not being safe at home, no food, or no place to live.*

**Help first. Paperwork after.**

1. Reply right away. Ask: **"Are you safe right now?"**
2. Share crisis help:
   - **United States:** call or text [988](tel:988) ([988 Lifeline](https://988lifeline.org)), or text HOME to [741741](sms:741741) ([Crisis Text Line](https://www.crisistextline.org))
   - **Anywhere else:** [findahelpline.com](https://findahelpline.com) lists free lines in every country
3. Message Liz directly, not only the channel. **You are not expected to handle this alone.**

For food, housing or money trouble (not an emergency), send them to the [unmet needs form](https://themultiverse.school/forms/unmet-needs). A person reads every one.

More detail: [Crisis Resource Appendix](crisis_resource_appendix.md) · [Emergency Flowchart](quick-reference/emergency-flowchart.md)

---

## Things that need an engineer

You'll hit these. They're not your fault, and there's no button for them yet. Post in Operations with the student ID.

- Re-sending a welcome email
- A payment link for a regular (non-scholarship) student
- Changing a scholarship student's attendance requirements
- Stopping a deletion that is already scheduled
- A merge that says **Cannot merge**
- A receipt that says **(no receipt available)**

If you find something that should be on this list, say so in Operations. That is how this page gets better.
