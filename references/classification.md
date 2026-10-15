# Classification guide

Use only the metadata allowed by `SKILL.md`. Sender, subject, date, category/labels, and unsubscribe headers are evidence; do not open a message body to resolve uncertainty. When uncertain, preserve the message and list it as excluded or unclear.

## Preserve by default

Exclude these from cleanup unless the user explicitly approves a numbered item that specifically includes them:

- Receipts, orders, invoices, billing, payments, renewals, refunds, and delivery/shipping notices.
- Account access, verification codes, password changes, security alerts, fraud notices, and service-status incidents.
- Collaboration notifications and messages that appear to be direct correspondence from a person.
- Direct recruiter or hiring-manager messages.
- Any category, sender, or topic listed in the user's private `config.yaml`, including job-alert digests when requested.

Treat subjects containing terms such as `invoice`, `receipt`, `order`, `billing`, `payment`, `shipping`, `delivery`, `security`, `password`, `verification`, `login`, `account`, or `service alert` as risk indicators. Do not include those messages in a cleanup item by default; list them in the report's risk-exclusions section. This is a conservative subject-based screen, not a judgment that every such message is truly transactional.

## Candidate signals

- Gmail `category:promotions` is a promotional signal, not automatic permission to act.
- In Gmail Updates or equivalent provider categories, include only clear marketing signals such as offers, discounts, coupons, commercial newsletters, job-alert digests (unless preserved), event marketing, and product announcements.
- A `List-Unsubscribe` header alone is not enough to classify mail as commercial. Use the sender, subject, category, date, and configured preservation rules.
- Do not infer a message is safe to clean solely because it is old, unread, bulk-sent, or has an unsubscribe header.
- Never include Spam as a cleanup target unless the user explicitly asks. Exclude messages already in Trash from candidate counts and execution selections.

## Unsubscribe

A `List-Unsubscribe` header is not evidence that mail is safe to clean. Unsubscribe candidates, header checks, and execution follow [the unsubscribe guide](unsubscribe.md).
