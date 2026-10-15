# Inbox cleanup assessment — YYYY-MM-DD

- **Generated:** YYYY-MM-DD HH:MM:SS with timezone
- **Account:** `<configured account>`
- **Provider:** `<Gmail / Outlook / other>`
- **Assessment:** read-only; no messages changed
- **Private candidate snapshot:** `<local file under reports/ containing item-to-message IDs and account; never publish>`
- **Cutoff:** `<exact generation timestamp>`; for Gmail API search use `before:<Unix seconds>` when supported; otherwise record the cutoff limitation
- **Scanned window:** `<recent stage: ~250 newest threads per category, dates covered>`; `<older mail: senders followed by sender-scoped metadata-only queries>`; other older mail not scanned

## Proposed actions

### 1. `<short category>`
- **Query:** `<exact provider query, including before: cutoff>`
- **Matched:** `<N>` messages in `<M>` conversations/threads (after risk exclusions; exactly the IDs that will be acted on)
- **Main senders:** `<sender — count>`
- **Sample subjects:** (3–5, or all available when fewer; mask sensitive identifiers/codes)
  - `<subject>`
  - `<subject>`
  - `<subject>`
- **Suggested action:** `<archive / move to Trash / unsubscribe / keep>`
- **Reason and exclusions:** `<classification basis and any limits>`

<!-- Repeat for each separately approvable item. -->

## Excluded risk mail

| Risk indicator | Messages | Examples (subjects only) | Why excluded |
|---|---:|---|---|
| `<invoice / receipt / security / etc.>` | `<N>` | `<subject>` | `<reason>` |

## Frequent senders

| Rank | Sender | Messages | Suggested filter (proposal only) |
|---:|---|---:|---|
| 1 | `<sender>` | `<N>` | `<provider-neutral condition and suggested destination/action>` |

<!-- Include up to 20 senders. Do not create the suggested filters. -->

## Unsubscribe review

Mode: `<off / list / provider>`. See the unsubscribe guide.

| # | Sender | Messages | Headers | Handling |
|---|---|---:|---|---|
| `<3.1>` | `<sender>` | `<N>` | `<one-click / mailto-only / none / headers unavailable>` | `<provider control / manual: Manage subscriptions / filter suggestion>` |

<!-- In provider mode, note that the provider may send an unsubscribe email for mailto-only senders. -->

## Approval instructions

Reply with exact item numbers and actions, for example `approve 1,3`. No changes have been made. Broad or ambiguous approval is not enough.

## Execution and verification log

- **Approved item numbers:** `<none until approval>`
- **Snapshot:** `<private file with item IDs and unread state>`
- **Pre-execution ID check:** `<approved IDs still present / dropped; stop and re-report if >10% dropped>`
- **Actions completed:** `<message and conversation counts by item; operation used: bulk / per-thread / per-ID>`
- **Unsubscribe:** `<sender: requested / not available / failed>`
- **Failures/skipped items:** `<details; IDs retried after transient errors>`
- **Verification:** `<Inbox query results>`
- **Recovery:** Find messages by `<cleanup/YYYY-MM-DD>`; restore archived mail to Inbox or restore Trash mail within the recovery window. Trash was not emptied.
- **Storage:** `<not freed by archive/Trash; only report a refreshed provider storage meter>`
