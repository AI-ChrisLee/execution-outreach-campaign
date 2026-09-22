# The campaign · Instantly

1 output: 1 campaign, built through the founder's Instantly connector, left a Draft. The founder presses Launch.

## A sending address named here

Only when the `sending address` row reads `not yet`. The mailbox setup and the record check belong to
"Build my outreach list."; this is the gate before the campaign, in this order:

1. A free address (gmail.com, outlook.com, hotmail.com, yahoo.com, icloud.com): refuse in 1 line. Cold email
   leaves from its own sending domain.
2. The domain has no NS record (`dig +short NS <domain>`, Windows `nslookup -type=NS <domain>`, and no
   nameserver comes back): say "<domain> is not registered yet. Buy it first, then tell me the address again."
   Write no row, and stop.
3. The domain shows up anywhere in `squad/` or `.claude/squad-roots.md` outside `squad/cold-list.csv` and the
   `sending address` row (a booking link, the voice sample, the founder's own site): say "<domain> is the
   domain your clients already know. Cold email leaves from a second domain bought only for it. Name that
   address, or say not yet." Write no row, and stop.

## The connector

Loaded when tools ending in `list_accounts`, `create_campaign`, `update_campaign`,
`add_leads_to_campaign_or_list_bulk`, `get_campaign` and `list_leads` are on the list. Read the live list
every run. Missing: print this, word for word, and stop.

```
Your campaign needs the Instantly connector, and it isn't connected yet. It runs on Instantly's API, which comes with Growth ($47 a month). 3 steps:
1. In Instantly: Settings, Integrations, API Keys, Create API Key, scope All. Copy it.
2. In Claude, click Customize, then Connectors, then +, then Add custom connector.
3. Name it Instantly. URL: https://mcp.instantly.ai/mcp/<your API key>. Click Add. That URL works like a password: never share it.
Then quit Claude Code, open it again in this folder, and say "<the line you said>" again.
```

Never print the key or the URL with the key in it.

## The build: `create_campaign`

| Field | Value |
|---|---|
| `name` | `Cold · <WHO line 1> · <today>` |
| `sequences` | 1 sequence, 3 steps, `type` "email", 1 variant each, off `references/the-messages.md` |
| step delays | step 1 `delay` 3, step 2 `delay` 5, step 3 `delay` 0 |
| subjects | email 1's subject on step 1, `""` on steps 2 and 3 |
| `body` | HTML, 1 `<div>` a line, `<div><br /></div>` for a blank line |
| `email_list` | [the sending address] |
| `daily_limit` | 30 |
| `stop_on_reply` | true |
| `text_only` | true |
| `open_tracking` | false |
| `link_tracking` | false |
| `campaign_schedule` | Monday to Friday, 09:00 to 17:00, in the list town's time zone |

**The delays.** In Instantly the delay on a step is the wait before the NEXT step. 3, 5, 0 lands email 1 on
about day 1, email 2 on day 4 and email 3 on day 9; a wait that ends on a weekend sends on Monday. The connector's own field note reads "before this step"; it is wrong, and 0, 3, 5 sends
email 2 on day 1.

The schedule, in this shape:

```
{"schedules":[{"name":"Weekdays","timing":{"from":"09:00","to":"17:00"},"days":{"1":true,"2":true,"3":true,"4":true,"5":true},"timezone":"America/Chicago"}]}
```

`timezone` is the town's on the `cold list` row, as a name like `America/Chicago`. Refused: the nearest one Instantly accepts.

A change from the Sunday read goes in through `update_campaign` on the same `id`, with all 3 steps and the
same delays.

## The leads: `add_leads_to_campaign_or_list_bulk`

Off `squad/cold-list.csv`, written by "Build my outreach list.", header
`Email,Company name,Website,Phone,Reviews,City,Zip code,Batch`.

- `campaign_id` the campaign's id, `skip_if_in_workspace` true. Never `list_id`: leads in a list send nothing.
- 1 lead a row: `email`, `company_name`, `website`, `phone`, `first_name` = `Owner` when the row has
  one, and `custom_variables`
  `{"Reviews": <Reviews>, "City": <City>, "Batch": <Batch>, "Note": <Note>, "Rating": <Rating>}`.
- A row with no `Note` (a list written before the column existed, or a blank): `Note` is written as
  `You have <Reviews> Google reviews in <City>.`, so `{{Note}}` never merges empty.
- `Batch` is what lets "Read my batch." count each batch in people.

## The read-back

`get_campaign`, then 1 screen, off what it returns and off the add call's reply for the 2 lead counts, never
off what was sent:

```
Campaign: <name>
Status: <Draft | Active | Paused | Completed>
Sender: <email_list off get_campaign, or (none attached) when the reply carries none>
Emails: 3, with a wait of 3 days, then 5 days
30 a day · stop on reply · text only
Monday to Friday, 9 to 5, <time zone>
Leads added: <n>, skipped: <n> (already in your workspace)
Built, not launched.
```

Status 0 is Draft, 1 Active, 2 Paused, 3 Completed. The last line prints only on a Draft; an Active campaign
ends on "Added to your running campaign."

The first build adds 2 lines:

```
You press Launch in Instantly yourself, the first time "Is my mailbox ready?" says Ready.
Instantly's own bounce auto-pause only starts after a campaign has sent 200 emails. Until then, "Read my batch." on Sunday is your brake.
```

## "Is my mailbox ready?"

Off `list_accounts` for the sending address. Ready = 14 or more whole days since `timestamp_warmup_start`,
and `stat_warmup_score` above 90. Both, because Instantly's own rule is both: a new mailbox can read 100 on
day 1. `warmup_status` not 1 means warmup is off: Not yet, and "Turn warmup on for <address> in Instantly."

```
Not yet.
Warmup: <n> days (needs 14). Score: <n> (needs above 90).
```

`1 day` when the count is 1.

```
Ready.
Warmup: <n> days (needs 14). Score: <n> (needs above 90).
```

Ready, and the campaign still reads Draft, adds the Launch block: the Launch line and the yes:

```
Press Launch on <campaign name> in Instantly yourself.
When a reply says yes:
1. /execution-genesis-demo <Company name>, <Website> off that row of squad/cold-list.csv, or his Instagram link when you sell content.
2. Record a Loom of the demo, under 2 minutes, your face on, and give /execution-genesis-demo the link.
3. /execution-genesis-close. THE MESSAGE is rewritten for him, with the Loom and your booking link.
4. Fill anything still in square brackets, like his first name, off his reply. Then send THE MESSAGE yourself, as your reply in that same Instantly thread.
The call runs off squad/sales.md.
Next, on Sunday once it sends: Read my batch.
```

## A warmup file

A `.csv` the founder hands over, 1 row a day of warmup, with a `Warmup day` column and a `Health score`
column. Read it only, no Instantly call. The last row decides: `Warmup day` 14 or more, and `Health score`
above 90. Both. Print the same Ready or Not yet screen off those 2 numbers, then the Launch block when a
`cold campaign` row exists, with the campaign name off that row.

## What never happens here

- `activate_campaign` and `campaigns_bulk_activate` are refused, at any size and on any wording.
- No write to the mailbox: not its warmup, not its daily limit, not its status.
- No lead is deleted. A lead who said stop stays in the workspace, and that keeps them out of every later batch.
- The only writes to Instantly are `create_campaign`, `update_campaign` and `add_leads_to_campaign_or_list_bulk`.
