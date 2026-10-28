# Architecture

SafeGuard is a single-scoped application in ServiceNow Studio. Each business process (incident, near miss, corrective action, each request type) has its own table and its own flow, triggered on record creation or update, rather than one monolithic flow covering everything.

## Notification layer

**S1 Send Safety Notification** is a reusable subflow called by every handler flow with a recipient, subject, and message body, covering 6 distinct notification scenarios: serious incident, corrective action assigned, investigation assigned, training expired, high-risk near miss, and corrective action completed.

**S2 Close Overdue Records** is a reusable subflow for marking lapsed records overdue, called from the daily scheduled check.

## Scheduled automation

- **F2 Daily Overdue Check** — runs daily at 8am.
- **F4 Training Compliance Monitor** — runs weekly, sending 60-day and 30-day warnings and flagging expiry.
- **F5 Monthly Safety Report** — compiles and sends a monthly summary to leadership.

## Slack integration

## Slack integration

When an incident is rated high or critical, the incident flow posts an alert to a dedicated Slack channel through an Incoming Webhook, so safety managers are notified where they already work. The webhook URL is stored in a system property, not in the flow. Email notifications still go out alongside the Slack alert.

Interactive Slack Approve/Reject buttons for PPE requests were attempted but not completed, so they are not part of this build. PPE approvals are handled inside the Management Portal.

## AI Assistant

Built on Google Gemini, with all API access kept server-side.

- **SafeGuard Gemini AI** — the REST Message record holding the connection and API key. Never exposed client-side.
- **SafeGuardAIService** — a Script Include defining the system prompt, role-based rules (so the employee and manager assistants behave differently from the same underlying service), a temperature of 0.2 for consistent, low-variance responses, and response cleaning before anything reaches the widget.
- **SG AI Assistant Button** — a floating widget on the Employee Portal, offering Report, Request, Emergency, and Guidance actions.
- **SG Manager AI Assistant** — a floating widget on the Management Portal, able to query live SafeGuard tables in addition to giving guidance.
- **SafeGuard Form AI Assistant** — a floating "Need help with this form?" widget present on individual record forms.

Scoped application restrictions encountered while building the Script Include: `addActiveQuery`, `addMonths`, and `getFields` are blocked in this application scope and had to be worked around.

## Portal layer

Two separate Service Portal experiences read from the same tables:

- **Employee Portal** (`safeguard_employee`) — navy-to-teal branding, hero banner with three action buttons, a QR code widget, recent reports, FAQ, time-based greeting, a tabbed My Reports page, and a navigation bar widget with dropdown menus.
- **Management Portal** (`safeguard_management`) — KPI summary cards, recent incidents, overdue actions, a card widget linking to every module plus the dashboard, sub-menu card navigation per module (e.g. All / Open / Overdue / Create New), and in-portal approve/reject for PPE, Risk, Inspection, and Consultation requests.

## Safety Map

A dedicated map page plots Incidents (red), Near Misses (yellow), and Risk Assessments (blue), with role-based filtering. Coordinates for the 8 physical locations are hardcoded, since the internal room-level location names used in SafeGuard's data (e.g. specific department areas) cannot be geocoded by an address lookup. Surfaced in navigation as a Safety Locations Map module, order 900.

## QR codes

Nine department QR codes, one per department, each linking to a quick-report page (`sg_quick_report?department=<department>`) that opens pre-filled for that department, with emergency numbers 999 and 111 displayed on the page.
