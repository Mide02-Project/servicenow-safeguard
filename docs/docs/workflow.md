# SafeGuard Workflow

```mermaid
flowchart TD
    A[Employee reports Incident, Hazard,\nDangerous Occurrence, or Near Miss] --> B[F1a / F3: Risk Rating calculated\nLikelihood x Severity]
    B --> C[Acknowledgement email sent]
    B --> D{High severity or\nhigh risk?}
    D -- Yes --> E[Investigation required flagged\nManager notified]
    E --> F[F1b: Investigation status tracked]
    F --> G{Corrective action required?}
    G -- Yes --> H[Corrective Action created]
    H --> I[Assignee notified]
    I --> J[Action completed]
    J --> K[Completion notice sent]
    G -- No --> L[Closed]
    D -- No --> L

    M[Risk Assessment / Safety Inspection /\nSafety Consultation / PPE Request] --> N[Submitted via Service Catalog]
    N --> O[Manager reviews in Management Portal]
    O --> P{Approved?}
    P -- Yes, PPE --> Q[Slack Approve/Reject buttons\nupdate status directly]
    P -- Yes, other --> R[Requester notified]
    P -- No --> R

    S[F2: Daily Overdue Check, 8am] --> T[S2: Close Overdue Records\nOverdue items flagged]

    U[F4: Weekly Training Compliance Monitor] --> V[60-day and 30-day warnings,\nexpiry notices]

    W[F5: Monthly Safety Report] --> X[Summary sent to leadership]

    Y[Employee scans department QR code] --> Z[Quick report page opens,\npre-filled with department]
```

This mirrors the actual flow set built in Flow Designer: F1a and F1b split incident creation from incident updates, F3 handles Near Miss, F2/F4/F5 are scheduled, and S1/S2 are shared subflows called from every handler.
