# The 3 emails

Email 1 offers 1 free thing and asks for a yes. Email 2, 3 days later, gives 1 new reason. Email 3, about 5 days
after that, closes the door.
They go into the campaign as its 3 steps, and nowhere else.

## The law

- Built off `squad/business.md` only: THE SHAPE, THE SENTENCE, THE PROBLEM, BUYER WORDS. Nothing invented
  about any business on the list.
- Email 1 under 80 words, the footer not counted.
- No price. No call ask. No link, no attachment, no image.
- The only merge fields are `{{Reviews}}` and `{{City}}`, spelled with that case. They match the lead's
  custom variables, and `{{reviews}}` merges nothing.
- The problem is said about businesses like theirs, never as a fact about this one. A scrape cannot see what
  a business needs.
- Never a moment the founder did not have ("a dentist told me last week"), and never a crowd made out of 1
  source ("some dentists say", "owners tell me"). 1 BUYER WORDS line is 1 person, so say the problem itself.
- The founder's plain words, the way the voice sample in `.claude/squad-roots.md` talks. Numerals. No em dash.
- Never a bump: "just following up", "bumping this", "did you see my last email".

## The free thing, off THE SHAPE

It is what `/the-demo` builds for a real business. The ask names it in plain words.

| THE SHAPE | What /the-demo builds | The free thing, said in the email |
|---|---|---|
| website | 1 phone-first homepage with their real details | a free demo of a new homepage |
| content | a small set of posts and 1 short video in their look | a free set of posts and a short video in your look |
| consulting program | a board of the program's stages with this week's action | a free plan of your first 4 weeks with me, stage by stage |
| software | 3 clickable screens of the tool | a free clickable demo of <the tool in 2 to 4 words, off THE SENTENCE> |

The subject is the free thing in 2 to 5 words, lowercase except AI, and it keeps the tool's name whole: "a free homepage demo", "a free AI receptionist demo".

## The templates

`<founder first name>` and `<founder name>` come off the `founder name` row. `<postal address>` off the
`postal address` row.

**Email 1** · step 1 · wait 3 days

```
Subject: <the free thing, 2 to 5 words>

You have {{Reviews}} Google reviews in {{City}}.

<1 plain line off THE PROBLEM, about businesses like theirs, naming the part THE SENTENCE fixes (for an AI receptionist, the phones), under 25 words. A line that only describes their day, with no pain in it, is not a problem line. THE PROBLEM holds no pain (a need or advice): write what a business like theirs loses without the part THE SENTENCE fixes, in plain words, with no number and no "most" (the call goes to the next dentist), never a vague cost like "gets in the way".>

Would it be okay if I made you <the free thing>? Just say yes.

<founder first name>

<founder name>
<postal address>
Not useful? Reply "stop" and I won't write again.
```

**Email 2** · step 2 · subject empty · wait 5 days

```
<1 new reason: the problem the way buyers put it, off a BUYER WORDS line email 1 did not quote, said about businesses like theirs and never with "your" (a scrape cannot see his trucks, his staff or his site). Never say who says it: the problem itself ("The work isn't the hard part. Finding it is."), not "some owners say". A line whose source is a seller's own page is not a buyer's words, and a line with no pain in it (advice, a to-do list, a description of the day) is not a reason. No such line left: a cost of THE PROBLEM that email 1 did not name, in new plain words, with no number and no "most".>

I'd make your <the subject without its first word> with your real details, so you see it before you decide anything. Just say yes.

<founder first name>

<founder name>
<postal address>
Not useful? Reply "stop" and I won't write again.
```

**Email 3** · step 3 · subject empty · wait 0

```
Last note from me. If <the subject> would help, just say yes.

<founder first name>

<founder name>
<postal address>
Not useful? Reply "stop" and I won't write again.
```

The empty subject threads emails 2 and 3 under email 1, so they read as 1 conversation.

## The footer, on all 3

No `postal address` row, or a row without its town, state and zip code: ask for it once, with this line.

```
Your postal address goes under every email. US law (CAN-SPAM) requires a real postal address and a working opt-out on every commercial email, business to business included, up to $53,088 for each email that breaks it. A P.O. box or a mailbox service works. A home address goes out on every email you send.
```

No address given, or one without its town, state and zip code (its postal code outside the US), like "PO Box 123": write no row and no email, say why in 1 line, and ask for the whole address. Never fill in a town, state or zip code for the founder, not even as an example. A made-up address is worse than none.

The opt-out works this way: a reply stops that lead's emails (stop on reply is on), the lead stays in the
Instantly workspace, and `skip_if_in_workspace` keeps them out of every later batch. The law gives 10
business days to honor it.

## A change from the Sunday read

The `Change:` line comes from the Sunday read in `squad/outreach-read.md`. Only email 1 changes. Emails 2
and 3 stay as they are.

- `Change: a new problem line in email 1.` Write the problem line off a BUYER WORDS line neither email 1 nor
  email 2 has used.
- `Change: a smaller free thing in email 1.` Offer the smallest piece of the free thing the demo still shows,
  and change the subject to match.

Print email 1 whole, then "Change any word, or say yes."
