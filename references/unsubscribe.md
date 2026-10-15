# Unsubscribe guide

The agent never decides on its own that an unsubscribe mechanism is safe. The mail provider does: the agent only uses the provider's own unsubscribe control, which runs the provider's sender checks and RFC 8058 handling. The agent never opens unsubscribe URLs, sends HTTP requests, or follows links itself.

## Modes (`unsubscribe` in `config.yaml`)

- `off`: skip the unsubscribe review.
- `list` (default): report candidates for the user to unsubscribe by hand. No mail or subscription is changed.
- `provider`: after numbered approval, the agent uses the provider-native unsubscribe control described below.

## Assess: header check

Check only the top 20 cleanup-candidate senders. For each, fetch the headers of one recent message (metadata/headers only, never the body) and record:

- `one-click`: an HTTPS `List-Unsubscribe` target plus `List-Unsubscribe-Post: List-Unsubscribe=One-Click`.
- `mailto-only`: only a `mailto:` target.
- `none`: no `List-Unsubscribe` header.
- `headers unavailable`: the connected surface does not return headers without the body.

If headers are only available together with the body (for example, the metadata-only view returns no headers and only a full or raw fetch does), skip the header check: do not fetch the body to get them. Record every candidate sender as `headers unavailable`; they are handled as in `list` mode, through the provider's subscription page (Gmail: **Manage subscriptions**).

Do not visit, test, or copy the URLs into the report. Senders listed as preserved in `config.yaml`, and senders whose mail falls under the classification guide's preserve rules (for example, a store that also sends receipts), are not candidates; list them as "kept" with the reason.

## Report

Put the candidates in one numbered item with sub-numbers, one per sender (`3.1`, `3.2`, ...), showing the sender, message count, header result, and how it will be handled:

- In `provider` mode: `one-click` and `mailto-only` senders are handled by the provider control. State in the item that, for `mailto-only` senders, the provider itself may send an unsubscribe email on the user's behalf.
- `none` and `headers unavailable` senders, and every sender in `list` mode: manual. Point the user to the provider's subscription page when it has one (Gmail: **Manage subscriptions** in the left menu), otherwise to a filter suggestion.

## Execute (`provider` mode only)

For each approved sender, in order of preference:

1. A connector operation that triggers the provider's unsubscribe for that sender, if one exists.
2. The provider's subscription-management page in the browser (Gmail: **Manage subscriptions**): find the exact sender and use its Unsubscribe button. This does not require opening any message.
3. The provider's unsubscribe control in the header area of one message from that sender (Gmail shows it next to the sender's name). Opening that message is allowed in Execute only, for approved senders only. Do not read, use, or click anything in the message body.

Accept the provider's own confirmation dialog for that sender. Stop and list the sender for manual handling if the provider shows no unsubscribe control, the dialog names a different sender, or the next step is an external website, a form, a sign-in, or a CAPTCHA. Never click a link in a message body, compose an email, or retry the same sender more than once.

## Verify

Log each sender as `requested`, `not available`, or `failed`. Do not report "unsubscribed": senders may take days to stop. On the next run, flag any `requested` sender that has sent new mail more than 7 days after the request date.
