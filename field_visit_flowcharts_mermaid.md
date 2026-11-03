# Field Visit module: flowcharts (Mermaid)

Paste any block into mermaid.live, Notion, GitHub, Confluence or draw.io (Arrange > Insert > Advanced > Mermaid).

## Chart 1: Visit flow (plan to approval)

```mermaid
flowchart TD
  S1(["START<br/>A field visit is needed"]) --> S2["Schedule the visit<br/>Manager / Team Lead: anyone<br/>Employee: own visits"]
  S2 --> S3{"Visit type?"}
  S3 -->|Sales| T1["Sales visit<br/>linked to a Prospect<br/>or Opportunity"]
  S3 -->|Exploration| T2["Company Exploration<br/>IT parks and companies"]
  S3 -->|Exhibition| T3["Exhibition / Trade Show<br/>halls and exhibitors"]
  S3 -->|HR| T4["HR visit<br/>Interview or<br/>Recruitment Drive"]
  T1 --> S4
  T2 --> S4
  T3 --> S4
  T4 --> S4
  S4["Saved as Scheduled<br/>Employee is notified"]
  S4 --> D1["Employee checks in<br/>GPS and time captured"]
  D1 --> D2{"Late, off-site<br/>or manual check-in?"}
  D2 -->|Yes| D3["Flag shown to approvers<br/>Team Lead notified"]
  D2 -->|No| D4
  D3 --> D4["Visit work<br/>Sales: meeting notes<br/>Exploration: parks and companies<br/>Exhibition: exhibitors and stalls<br/>HR: candidates and resumes"]
  D4 --> R1["Employee checks out and submits report<br/>Outcome, notes, next action, photos"]
  R1 --> R2["Status: Pending Approval<br/>Follow-up task created"]
  R2 --> R3{"Team Lead<br/>approves?"}
  R3 -->|Yes| R4{"Manager<br/>approves?"}
  R3 -->|Returned with remarks| R5["Employee corrects<br/>and resubmits"]
  R4 -->|Returned with remarks| R5
  R5 --> R2
  R4 -->|Yes| R6(["Visit Completed"])
  R6 --> A1["Sales: update Prospect /<br/>Opportunity stage in CRM"]
  R6 --> A2["Exploration / Exhibition:<br/>add interested companies<br/>as Prospects"]
  R6 --> A3["HR: add candidates<br/>to candidate pool"]
  A1 --> M1
  A2 --> M1
  A3 --> M1
  M1[["Management reports and CSV exports<br/>completion, conversion, cost per visit,<br/>exhibitors found, candidates selected"]]
  R2 -.->|"report submitted"| X1(["Expenses: see chart 2"])
  S4 -.-> X2(["Changes and misses: see chart 3"])

  classDef emp fill:#e3eefc,stroke:#1b6fd1,color:#154b8f;
  classDef lead fill:#ece6fa,stroke:#6b46c1,color:#4b2f93;
  classDef mgr fill:#fcefd3,stroke:#b4720b,color:#7d4f06;
  classDef sys fill:#eef1f5,stroke:#6c7b8b,color:#3e4b5a;
  classDef dec fill:#fff6dc,stroke:#a86a08,color:#5c3d03;
  classDef endok fill:#dcf5e7,stroke:#178a57,color:#0f5f3b;
  classDef ref fill:#ffffff,stroke:#9aa8b8,color:#46566a,stroke-dasharray:4 3;
  class S2,D1,D4,R1,R5 emp;
  class S4,R2,D3,A1,A2,A3,T1,T2,T3,T4 sys;
  class R3 lead;
  class R4 mgr;
  class S3,D2 dec;
  class S1,R6 endok;
  class X1,X2 ref;
```

## Chart 2: Expense flow (internal and external)

```mermaid
flowchart TD
  E0(["START<br/>Visit report submitted"]) --> E1["Employee adds an expense claim<br/>one or more lines"]
  E1 --> E2{"Expense type<br/>for each line?"}
  E2 -->|"INTERNAL<br/>provided by the company"| E3["Company car, bus or shuttle,<br/>booked tickets or stay, company card<br/>Reference and cost estimate<br/>No receipt. Not reimbursed."]
  E2 -->|"EXTERNAL<br/>paid by the employee"| E4["Cab, travel, meals, parking, mileage<br/>Receipt needed above Rs 200<br/>Daily category limit checked"]
  E3 --> E5
  E4 --> E5["Claim submitted<br/>Team Lead reviews"]
  E5 --> E6["Manager reviews<br/>Can reduce external amounts"]
  E6 -->|Returned or rejected| E7["Employee edits<br/>and resubmits"]
  E7 --> E5
  E6 -->|Approved| E8{"Any external<br/>amount to pay?"}
  E8 -->|Yes| E9["Accounts records payment<br/>Date, method, UTR reference"]
  E9 --> E10(["Claim Reimbursed<br/>Employee notified"])
  E8 -->|"No, internal lines only"| E11(["Claim Closed<br/>no payout"])
  E10 --> E12[["Reports: reimbursed amount,<br/>company-provided cost,<br/>cost per visit"]]
  E11 --> E12

  classDef emp fill:#e3eefc,stroke:#1b6fd1,color:#154b8f;
  classDef lead fill:#ece6fa,stroke:#6b46c1,color:#4b2f93;
  classDef mgr fill:#fcefd3,stroke:#b4720b,color:#7d4f06;
  classDef acc fill:#dcf2e6,stroke:#178a57,color:#0f5f3b;
  classDef sys fill:#eef1f5,stroke:#6c7b8b,color:#3e4b5a;
  classDef dec fill:#fff6dc,stroke:#a86a08,color:#5c3d03;
  classDef endok fill:#dcf5e7,stroke:#178a57,color:#0f5f3b;
  class E1,E7 emp;
  class E5 lead;
  class E6 mgr;
  class E9 acc;
  class E3,E4 sys;
  class E2,E8 dec;
  class E0,E10,E11 endok;
```

## Chart 3: Reschedule, missed and cancelled visits

```mermaid
flowchart TD
  V["Visit is Scheduled"] --> Q{"What happens?"}
  Q -->|"Employee cannot attend"| X1["Employee requests a new date<br/>with a reason"]
  Q -->|"Date passes, no check-in"| X5["System marks the visit Missed<br/>Employee is notified"]
  Q -->|"Manager or Team Lead acts"| X6["Reassign to another employee<br/>or change date and time directly"]
  Q -->|"Visit no longer needed"| X7["Manager or Team Lead cancels<br/>reason is required"]
  X5 --> X8["Employee adds a reason<br/>and can ask for a new date"]
  X8 --> X1
  X1 --> X2{"Team Lead or Manager<br/>approves?"}
  X2 -->|Yes| X3["Date changed<br/>Employee notified"]
  X2 -->|No| X4["Request rejected<br/>Visit stays as planned"]
  X6 --> X3
  X3 --> V2(["Visit back to Scheduled<br/>continues in chart 1"])
  X7 --> X9(["Visit Cancelled"])

  classDef emp fill:#e3eefc,stroke:#1b6fd1,color:#154b8f;
  classDef mgr fill:#fcefd3,stroke:#b4720b,color:#7d4f06;
  classDef sys fill:#eef1f5,stroke:#6c7b8b,color:#3e4b5a;
  classDef dec fill:#fff6dc,stroke:#a86a08,color:#5c3d03;
  classDef endok fill:#dcf5e7,stroke:#178a57,color:#0f5f3b;
  classDef bad fill:#fde8eb,stroke:#c53046,color:#8d2434;
  class X1,X8 emp;
  class X6,X7 mgr;
  class X5,X3,X4,V sys;
  class Q,X2 dec;
  class V2 endok;
  class X9 bad;
```

