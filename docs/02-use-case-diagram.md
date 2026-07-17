# Job Application Tracker — Use Case Diagram

## Actor
- **User** (the only actor — see requirements doc, section 2)

## Use Case → Functional Requirement Traceability

| Use Case | Traces to |
|---|---|
| Register | FR1 |
| Login | FR2 |
| Create Application | FR3 |
| Edit Application | FR3 |
| Delete Application | FR3 |
| Change Application Status | FR4 |
| Add Note | FR5 |
| View Dashboard | FR6 |
| View Stats | FR7 |

Every functional requirement maps to exactly one use case, and every use
case traces back to a requirement — no orphaned features, nothing in the
requirements doc left unaccounted for. That check is the actual point of
this diagram, more than the picture itself.

## Diagram

```mermaid
flowchart LR
    actor((User))

    subgraph System["Job Application Tracker"]
        UC1(["Register"])
        UC2(["Login"])
        UC3(["Create Application"])
        UC4(["Edit Application"])
        UC5(["Delete Application"])
        UC6(["Change Application Status"])
        UC7(["Add Note"])
        UC8(["View Dashboard"])
        UC9(["View Stats"])
    end

    actor --- UC1
    actor --- UC2
    actor --- UC3
    actor --- UC4
    actor --- UC5
    actor --- UC6
    actor --- UC7
    actor --- UC8
    actor --- UC9

    UC3 -. include .-> UC2
    UC4 -. include .-> UC2
    UC5 -. include .-> UC2
    UC6 -. include .-> UC2
    UC7 -. include .-> UC2
    UC8 -. include .-> UC2
    UC9 -. include .-> UC2
```

## Note on the `<<include>>` relationships
Every use case except Register and Login includes Login — meaning none of
them can happen without an authenticated session first. This isn't just
decoration: it's a direct preview of the backend architecture decision
we'll make soon (a global auth guard on every route except `/auth/register`
and `/auth/login`), and of the frontend routing decision (a route guard /
protected-route wrapper around every page except the login screen). The
diagram is already telling us something about the implementation.
