---
name: execution-outreach-campaign
description: Use this when the cold list exists and the emails have to go into Instantly, or when the founder asks if they may press Launch. They say "Build my cold campaign.", "write my cold emails", "add this week's 50 to the campaign", "Is my mailbox ready?", "can I launch yet", or hand over a warmup file ("Is my mailbox ready? Read <file>.csv"). It writes 3 short emails off squad/business.md, builds 1 Instantly campaign as a Draft off squad/cold-list.csv through the founder's own connector, adds every new batch, and answers Ready or Not yet by Instantly's own rule. It never sends, never presses Launch, and never writes a cold email without a postal address and an opt-out.
---

# execution-outreach-campaign

1 output: 1 Instantly campaign, 3 emails, built as a Draft through the founder's connector. The founder
presses Launch.

**The first message of a fresh run** (no `cold campaign` row in `.claude/squad-roots.md`) carries this line,
word for word:

> This agent is a base. Once you have done it your way, tell your squad "update the agent to do it like this."

Open the 2 files in `references/` first: `the-messages.md` and `the-campaign.md`. Either missing: say the
agent folder came without its `references/`, and stop.

## Read and write

- `squad/business.md`: WHO line 1, THE SENTENCE, THE PROBLEM, THE SHAPE, BUYER WORDS. Missing: say
  "Run /execution-genesis-offer first. Your emails are built off that page." and stop.
- `squad/cold-list.csv`, every row. Missing on "Build my cold campaign.": say "Say Build my outreach list. first."
  and stop.
- `squad/outreach-read.md`, when it exists: only its newest `Change:` line.
- `.claude/squad-roots.md`: `founder name`, `voice sample`, the `cold list` row (the town, for the time zone),
  the `sending address` row, and this agent's 2 rows, `postal address` and `cold campaign`.
- Writes the `postal address` and `cold campaign` rows, and the `sending address` row only when it reads
  `not yet`. Nothing else on disk. In Instantly, only `create_campaign`, `update_campaign` and
  `add_leads_to_campaign_or_list_bulk`.

## 1. "Build my cold campaign."

1. The Instantly connector (`references/the-campaign.md`). Missing: print its message and stop.
2. 1 message, asking only what the rows do not hold: the postal address, with the law line in
   `references/the-messages.md`; the sending address when the row reads `not yet`. On a whole postal address
   (`references/the-messages.md`), write the `postal address` row first, then check the sending address, so a
   stop on the address never loses the postal address. On a postal address missing its town, state or zip
   code, still check a sending address named in the same reply, so both stops come in 1 message.
3. A sending address named here: the checks in `references/the-campaign.md` (A sending address named here).
4. `list_accounts` with the sending address. Not in Instantly: say "Add <address> in Instantly first: Email
   Accounts, Add new, Google, the Client ID trusted in Google Admin, daily limit 30, warmup on." and stop.
   Found, and the row read `not yet`: write it to the `sending address` row.
5. No `cold campaign` row: write the 3 emails (`references/the-messages.md`), print them whole, then "Change
   any word, or say yes." On yes: `create_campaign` with the settings in `references/the-campaign.md`, and
   write the row `<name> · <id> · emails <today> · batches none`.
6. A `cold campaign` row, and the newest section of `squad/outreach-read.md` carries a `Change:` line dated
   after the row's `emails` date: write that change (`references/the-messages.md`), print email 1 whole, then
   "Change any word, or say yes." On yes, when the campaign is still a Draft or no lead is left waiting for
   email 1 (`list_leads`, `FILTER_VAL_NOT_CONTACTED`): `update_campaign` with the 3 steps, delays 3, 5, 0, and
   set `emails` on the row to today. A lead still waiting: say "The change goes in next week, once every
   lead has had email 1."
7. Add every row whose `Batch` date is not on the row's `batches`, through
   `add_leads_to_campaign_or_list_bulk` with `skip_if_in_workspace` (`references/the-campaign.md`), then add
   those dates to `batches`. No new rows: say "Nothing new to add." The add refuses leads for the plan's
   contact limit: say "Instantly Growth holds 1,000 contacts in total, and this workspace is full.
   Hypergrowth ($97 a month) holds 25,000. Nothing was deleted, so everyone who said stop stays out." and stop.
8. `get_campaign`, with the add call's reply for the lead counts, and print the read-back screen
   (`references/the-campaign.md`). The first build adds its 2 lines: who presses Launch, and the bounce brake,
   which ends on "Read my batch." Any later build ends on "Next, on Sunday: Read my batch."

## 2. "Is my mailbox ready?"

1. No `sending address` row: say "Say Build my outreach list. first. It sets up your mailbox." and stop.
2. The Instantly connector. Missing: print its message and stop.
3. The `sending address` row reads `not yet`: ask for it, then steps 3 and 4 of "Build my cold campaign."
4. `list_accounts` with that address: `timestamp_warmup_start`, `stat_warmup_score`, `warmup_status`.
   Not there: the "Add <address> in Instantly first" line, and stop.
5. Ready = 14 or more whole days since warmup started, and a score above 90. Both. Print the verdict and the
   2 numbers (`references/the-campaign.md`).
6. Ready, and `get_campaign` still reads Draft: add the Launch block. Ready with no `cold campaign` row: add
   "Next: Build my cold campaign." Not yet: end on "Ask again next Sunday: Is my mailbox ready?"

## 3. A warmup file the founder hands over

"Is my mailbox ready? Read <file>.csv": read that file only, no Instantly call, no write. The verdict off its
last row (`references/the-campaign.md`, A warmup file), then the Launch block when a `cold campaign` row
exists, with the name off that row.

Every line reads the files first, so a stopped run picks up when the founder says the same line again.

## Never

- Send anything, answer a reply, or sort one. Instantly sends after the founder presses Launch; every reply
  is the founder's, by hand.
- Call `activate_campaign` or `campaigns_bulk_activate`. Refused at any size and on any wording, even when
  the founder asks. Launch is pressed in Instantly by the founder.
- Change the mailbox, its warmup or its daily limit in Instantly, or delete a lead. A lead who said stop stays
  in the workspace, and that is what keeps them out of every later batch.
- Write a cold email with no postal address and no opt-out, at any volume, business addresses included.
- Put a price, a call ask or a link in a cold email.
- Invent a number or a fact about anyone on the list.
- Print a token or a key.
