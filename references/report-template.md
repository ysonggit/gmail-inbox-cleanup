# Inbox cleanup assessment — YYYY-MM-DD

- **Generated:** YYYY-MM-DD HH:MM:SS with timezone
- **Account:** `<configured account>`
- **Provider:** `<Gmail / Outlook / other>`
- **Assessment:** read-only; no messages changed
- **Private candidate snapshot:** `<local file under reports/ containing item-to-message IDs and account; never publish>`
- **Cutoff:** `<exact generation timestamp>`; for Gmail API search use `before:<Unix seconds>` when supported; otherwise record the cutoff limitation

## Proposed actions

### 1. `<short category>`
- **Query:** `<exact provider query, including before: cutoff>`
- **Matched:** `<N>` messages in `<M>` conversations/threads
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

| Sender | Messages | RFC 8058 headers | Suggested handling |
|---|---:|---|---|
| `<sender>` | `<N>` | `<both present / missing / unsupported>` | `<numbered approval item / manual review>` |

## Approval instructions

Reply with exact item numbers and actions, for example `approve 1,3`. No changes have been made. Broad or ambiguous approval is not enough.

## Execution and verification log

- **Approved item numbers:** `<none until approval>`
- **Prior message state:** `<private snapshot of labels, Inbox/Trash location, and read state for recovery>`
- **Pre-execution counts:** `<counts; stop and re-report if any differ by >10%>`
- **Actions completed:** `<message and conversation counts by item>`
- **Failures/skipped items:** `<details>`
- **Verification:** `<Inbox query results>`
- **Recovery:** Find messages by `<cleanup/YYYY-MM-DD>`; restore archived mail to Inbox or restore Trash mail within the recovery window. Trash was not emptied.
- **Storage:** `<not freed by archive/Trash; only report a refreshed provider storage meter>`
