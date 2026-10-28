# Screenshot Guide

Each tested scenario in the main README gets its own folder here, named to match the table (e.g. `TC01-incident-created`). Inside each folder:

- `01-submission.png` - the form or record being created
- `02-action.png` - the step that proves the logic fired (status change, notification, Slack message, record created)
- `03-result.png` - the end state (record closed, email in Outbox, Slack confirmation)
- `notes.md` - one or two lines: what you did, what you expected, what happened

Keep filenames numbered in the order the test actually happened.

For email evidence, a screenshot of the record in System Mailboxes > Outbox is sufficient. For Slack evidence, include one screenshot of the alert in the Slack channel with the incident number visible, next to the incident record it came from.
