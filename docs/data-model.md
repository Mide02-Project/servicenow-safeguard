# Data Model

## Core tables

| Table | Purpose |
|---|---|
| Safety Incident | Incidents, hazards, dangerous occurrences, and investigations |
| Near Miss Report | Close calls, with likelihood and severity |
| Corrective Actions | Actions raised from investigations and near misses |
| Risk Assessment | Documented workplace risks |
| Safety Inspection Request | Employee requests for inspections |
| Safety Consultation Request | Requests for safety advice |
| PPE Request | Protective equipment requests |
| Training Record | Certifications, expiry, and results |

## Reference data

- 9 departments
- 8 locations
- 3 incident types: Incident, Hazard, Dangerous Occurrence

## Decision table

**SR Risk Rating Matrix** — 20 rows, Likelihood x Severity, used across Safety Incident, Near Miss Report, and Risk Assessment so risk is calculated once, consistently, rather than re-implemented per table.

## Naming conventions

- Corrective Actions' table name carries a trailing "s".
- Real field names carry no `u_` prefix.
- PPE Request, Safety Inspection Request, and Safety Consultation Request all use a field literally named `status`.

## Relationships

- Corrective Action can originate from a Safety Incident investigation or a Near Miss Report.
- Risk Assessment, Safety Inspection Request, Safety Consultation Request, and PPE Request are independent request tables, each with its own approval path.
