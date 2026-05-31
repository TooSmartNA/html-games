# Moving Software — Master Blueprint
**Project Codename:** TBD  
**Goal:** Build a full-service moving company platform that matches and exceeds CompuMove 8  
**Status:** Pre-development — feature planning phase

---

## What We're Building

A complete, cloud-based moving company management platform covering every touchpoint of the business — from the first inbound lead to the final invoice, warehouse receipt, and reporting. Built modular so features can be developed one at a time and connected together.

---

## Module Map (Build Order TBD)

### MODULE 1 — CRM & Lead Management
The front door of the business. Every job starts here.

- Inbound lead capture (web form, phone, email, third-party lead sources)
- Lead pipeline view (kanban or list) with configurable status stages
- Lead source tracking (where did this lead come from?)
- Contact & account profiles (household vs. commercial)
- Full communication history log per lead/customer (calls, emails, notes)
- Automated follow-up sequences (email/SMS drip campaigns)
- Follow-up reminders and task assignments
- Duplicate detection
- Lost lead reasons tracking
- Re-engagement workflows for cold leads
- **Exceeds CompuMove:** AI-assisted lead scoring, automated review requests post-move

#### Lead Assignment Workflow
1. All inbound leads land in the **HHG Coordinator's queue** first — unassigned
2. Coordinator reviews and **assigns each lead to a salesperson**
3. Salesperson is notified and the lead appears in their personal pipeline
4. Coordinator retains **full visibility** of every lead regardless of who owns it — pipeline stage, last activity, estimate status, next follow-up
5. Salesperson has a **personal view** showing only their assigned leads
6. As the salesperson progresses the lead (notes added, estimate sent, follow-up scheduled), the status updates **automatically** in the coordinator's view in real time
7. Coordinator can **reassign** a lead to a different salesperson at any time
8. Coordinator can add notes or tasks to any lead even if owned by a salesperson

#### What Coordinators See
- All leads across all salespeople in one master pipeline view
- Filter by salesperson, stage, source, move date, lead age
- Activity feed per lead: every call logged, email sent, estimate generated, stage change
- Alert flags: leads with no activity in X days, estimates sent but no response, overdue follow-ups

#### What Salespeople See
- Only their own assigned leads
- Their personal pipeline (same kanban/list but scoped to them)
- Full detail on each of their leads: customer info, history, estimate tool, communication log
- Cannot see other salespeople's leads or totals

---

### MODULE 2 — Estimating
The core sales tool. Must be fast, accurate, and usable in the field.

- Room-by-room inventory builder (furniture + box counts)
- Cube/weight estimation engine
- Local hourly rate estimating
- Long distance weight-based estimating
- Binding vs. non-binding estimate types
- Estimate history — full change log from first contact through job completion
- Mobile-friendly estimating (tablet/phone for in-home surveys)
- Virtual survey support (video call or photo upload)
- Multiple estimate versions per job
- Estimate PDF generation with company branding
- Digital signature on estimates (legally binding under ESIGN Act)
- Automatic conversion from estimate → quote → job
- **Exceeds CompuMove:** AI item recognition from photos, real-time weight calculation

#### Estimate Ownership & Visibility
- Salespeople build and send estimates for their assigned leads only
- When an estimate is sent, the lead stage **automatically advances** to "Estimate Sent" — no manual update needed
- Coordinator sees all estimates across all salespeople: sent date, version, value, customer response status
- Coordinator can review, edit, or approve an estimate before it goes out (optional approval gate — configurable per company)
- Estimate activity (opened, signed, declined) is logged automatically and visible to both the salesperson and coordinator

---

### MODULE 2A — Customer Accounts
Every customer — household or commercial — has a persistent account profile that lives beyond any single job. This is the full 360° view of the customer relationship.

#### Account Types
- **Household (HHG)** — individual or family; linked to HHG business line
- **Commercial** — company account with multiple contacts; linked to Commercial business line
- A customer can have both HHG and Commercial interactions under one account if applicable

#### Customer Profile — What It Shows
- **Contact info:** name(s), phone, email, address(es), preferred contact method
- **Account tags:** Recurring, VIP, Corporate, Military, Government, Storage Account, etc. (customizable)
- **Assigned salesperson and coordinator**
- **File Reference Numbers** — all files (past and present) linked to this customer
- **Active Jobs** — jobs currently in progress or dispatched
- **Upcoming Jobs** — booked jobs with future dates
- **Job History** — all completed, cancelled, and invoiced jobs with dates and values
- **Storage Accounts** — dedicated storage section on every customer profile (see below)
- **Open Invoices** — unpaid invoices with amounts and aging
- **Revenue Summary:**
  - Total lifetime revenue
  - Revenue this year
  - Average job value
  - Number of moves completed
- **Communication History** — all calls logged, emails sent, notes added, across all jobs and leads
- **Documents** — all BOLs, estimates, invoices, and forms across all files in one place
- **Claims History** — any damage or loss claims ever filed

#### Customer Profile — Storage Section
Every customer profile has a dedicated storage section that is always visible (not buried in a tab) if they have any active storage. This is a first-class section because storage is ongoing and recurring.

**Per active storage account shows:**
- Vault number(s) and location in warehouse
- Vault size (e.g., 10×10, 5×10)
- **Item inventory** — the actual itemized list of what is in storage, pulled from the Storage In job event's inventory. Shown as a scrollable item list with item name, qty, and any condition notes.
- Date items entered storage
- Estimated cubic footage in storage
- Monthly billing rate and next billing date
- Running total billed to date for this storage account
- Status: Active / Pending Delivery / Closed

**Actions directly from the storage section:**
- **Schedule Haul Out** — creates a new Haul Out job event pre-filled with the customer's stored inventory and origin (warehouse)
- **Schedule Partial Delivery** — select specific items from the inventory list to deliver; remainder stays in storage
- **Add Items to Storage** — links a new Storage In event to the existing account
- **View Full Vault Record** — links to the warehouse module detail for this vault
- **Close Storage Account** — marks account closed after final haul out; archives the inventory

**If a customer has multiple storage accounts** (e.g., from different moves at different times), each account is shown as a separate card with its own inventory, billing, and actions.

#### Recurring Customer Features
- "Book Again" button — pre-fills a new estimate/job using previous move details as a starting point
- Flag account as **Do Not Contact** or **Preferred** for marketing
- Notes pinned to the account (not tied to a specific job)
- Internal account rating (1–5 stars) visible to coordinators and sales

#### Commercial Account Extras
- Multiple contacts per account (billing contact, operations contact, etc.)
- Contract pricing attached to account (custom rate that overrides standard tariff)
- PO number tracking per job
- Multi-location management (company has offices in multiple cities)

---

### MODULE 3 — Quotes & Proposals
- Branded quote documents (PDF + web link)
- Quote expiration dates
- Accepted / declined / expired tracking
- Optional add-ons and upsells (packing services, storage, valuation coverage)
- Valuation / insurance options built into quote
- Customer e-signature on quote acceptance
- Automatic job creation on acceptance

---

### MODULE 4 — Jobs & Orders
The central record for every move. Built around a two-level hierarchy: a **File** (the customer relationship) and **Job Events** (individual service instances under that file).

#### Job File Structure

Every customer account gets a **File Reference Number** (e.g., `FILE-2026-0842`). The file is the top-level record — it persists for the life of the customer relationship. All job events, billing history, documents, and communications are attached to the file.

Under each file, any number of **Job Events** can be created independently:

| Event Type | Description | Billing Type |
|-----------|-------------|-------------|
| **Move** | Standard pickup and delivery | One-time |
| **Packing** | Pack-only service, no transport | One-time |
| **Storage In** | Items placed into warehouse storage | Triggers recurring billing |
| **Storage Recurring** | Monthly storage charge | Recurring (auto-generated) |
| **Haul Out** | Retrieval and delivery from storage | One-time |
| **Partial Delivery** | Deliver portion of stored items | One-time |
| **Return** | Return items to origin | One-time |
| **Commercial Move** | Multi-day or project-based commercial | One-time or milestone |
| **Additional Services** | Debris removal, returns, etc. | One-time |

**Example lifecycle for one file:**
1. `FILE-2026-0842` created from a booked lead
2. Event 1 — Move (JOB-0842-01): crew dispatched, completed, invoiced
3. Event 2 — Storage In (STO-0842-01): items vaulted, recurring billing starts
4. Event 3 — Storage Recurring (REC-0842-01 through REC-0842-06): auto-generated monthly invoices
5. Event 4 — Haul Out (JOB-0842-02): crew dispatched to deliver from storage, invoiced separately

Each job event has its own:
- Crew and truck assignment
- Dispatch entry and schedule slot
- BOL / delivery receipt
- Invoice
- Status lifecycle

#### Master Jobs View
- Searchable by: file reference number, customer name, job event ID, origin/destination address, move date, crew member, truck, salesperson, coordinator
- Filterable by: status, event type, business line (HHG/Commercial), date range, assigned crew, billing type
- Shows both the file-level summary and individual event rows (expandable)
- Saved search templates for common views (e.g., "Today's dispatched jobs", "Open storage accounts", "Uninvoiced completed jobs")

#### Other Job Record Features
- Job types: Local, Long Distance, International, Commercial, Military, Government (GSA)
- Special instructions and access notes (elevator, stairs, parking, etc.)
- Itemized inventory attached to each move event
- Carton/packing material tracking
- Valuation coverage selection per event
- Notes and internal comments (shared across the file)
- Full status history with timestamps per event
- Claims management (damage/loss claims linked to a specific event)
- Actuals vs. estimates comparison per event

---

### MODULE 5 — Scheduling & Dispatch
The operations hub. Dispatchers and coordinators live here. Designed for speed, accuracy, and flexibility.

#### Dispatch Board — Views
- **Month view** — full calendar grid showing all days; each day shows a summary chip (job count, capacity status). Click any day to drill into the day detail. Color-coded capacity heatmap across the month (green = available, yellow = busy, red = full/overbooked)
- **Week view** — 7-day strip with job cards per day; crew roster and fleet panels on the sides
- **Day view** — full detail for a single day; time-slotted layout showing job windows, crew assignments, and truck assignments
- Switch freely between views; selected day persists across view changes
- Each job event card shows: customer, address, time window, men required/filled, truck type, current assignment status
- **Drag-and-drop** crew members from the crew roster panel onto job cards to assign them
- **Dropdown assignment** on each job card as an alternative to drag-and-drop
- Color-coded by job type (Local, LD, Commercial), status, and business line (HHG/Commercial)
- Conflict detection — warns if a crew member or truck is double-booked
- Capacity heatmap by day showing how many men and trucks are committed vs. available
- Dispatcher notes per job per day

#### Date Change Request Workflow
Coordinators cannot directly change a job's date once it has been dispatched — they submit a request that goes through the dispatcher.

1. Coordinator opens a job and clicks **Request Date Change** — enters the requested new date and a reason
2. Dispatcher receives an **alert** on the dispatch board and in their task queue immediately
3. Dispatcher reviews the request against the new date's capacity and crew availability
4. Dispatcher can:
   - **Approve** — date updates, crew/truck re-assigned if needed, coordinator and customer notified
   - **Propose Alternative** — dispatcher suggests a different date, coordinator gets notified to accept or counter
   - **Decline** — with a reason; coordinator is notified
5. Full request history (who requested, what date, outcome) is logged on the job record
6. Customer notification of confirmed date change is sent automatically on approval

#### Job Resource Requirements
Each job event has dispatcher-controlled resource fields:
- **Number of men** required (set by coordinator/dispatcher, used for BOL and dispatch ticket)
- **Estimated hours** for the job (drives billing estimate and crew schedule)
- **Truck type** required: 26ft box, 16ft box, cargo van, flatbed, etc.
- **Number of trucks** required
- These fields feed directly into BOL and dispatch ticket generation — no separate data entry

#### Crew Roster Panel
- Persistent side panel on the dispatch board showing all crew members
- Each crew member card shows: name, role (driver, helper, lead), today's assignment status (available, assigned, off, unavailable)
- Drag a crew member card directly onto a job to assign them
- Filter roster by: available today, role type, HHG vs. commercial certified
- Click a crew member to see their full week schedule

#### Truck & Equipment Board
- Separate view for truck availability across the fleet
- Each truck shows: type, size, current assignment, next available slot
- Assign trucks to jobs by drag-and-drop or dropdown, same as crew

#### Document Generation from Dispatch
- Once a job is fully assigned (crew + truck + hours confirmed), dispatcher can generate:
  - **Dispatch Ticket** — internal document: job details, crew names, truck, time window, origin/destination, special instructions
  - **Bill of Lading** — customer-facing: auto-populated from job record + dispatch details (crew count, truck, estimated weight, inventory summary)
- Both documents reflect exactly what was entered in dispatch — no re-keying

#### Other Dispatch Features
- Daily dispatch sheet — printable/exportable summary of all jobs for the day
- Worker schedule view — per crew member, what they're doing each day of the week
- Route optimization suggestions for local multi-stop days
- Real-time field status updates visible on the board (crew clocked in, en route, at origin, loading, at destination, complete)
- Push notifications to crew when job details change or new assignments are made
- Google Calendar integration for crew members
- **Exceeds CompuMove:** Full drag-and-drop board, resource requirement fields drive document generation automatically

---

### MODULE 5A — Crew Management
Manage all crew members, their roles, team assignments, and availability. Accessed by dispatchers, coordinators, and admins. A separate tab within the dispatch/operations section.

#### Crew Member Profiles
- Add / edit / deactivate crew members
- Per-member fields: name, phone, email, role (Lead, Driver, Helper, Warehouse), certifications, hire date, notes
- Profile photo
- Active / inactive / terminated status
- Current team assignment(s) — a crew member can belong to multiple teams

#### Teams
- Admin and dispatchers can create named teams (e.g., "Local Team A", "Local Team B", "LD Team 1", "Commercial Crew", "Warehouse")
- Teams are not fixed — crew members can be moved between teams at any time
- Default team types (configurable):
  - **Local** — assigned to local HHG and commercial jobs
  - **Long Distance (LD)** — drivers and helpers certified for interstate runs
  - **Commercial** — commercial move specialists
  - **Warehouse** — vault and storage operations only
  - Custom teams can be created by admin
- Team view on the dispatch board — filter the crew roster panel by team
- A crew member can be flagged as multi-team (e.g., a driver who runs both local and LD)

#### Availability & Scheduling
- Set recurring availability per crew member (e.g., Mon–Fri, available 7am–5pm)
- Mark individual days as: Available, Unavailable, PTO, Sick, Off
- Availability feeds directly into the dispatch board — unavailable crew don't appear as assignable
- Dispatch board shows each crew member's current day status in real time

#### Pay Rates & Commissions
Pay rates are set and managed by Admin only. They are used exclusively for internal job costing and actuals calculation — this is not a payroll processing system.

**Rate Hierarchy (highest priority wins):**
1. **Individual rate** — set directly on a crew member's profile; overrides everything
2. **Team/category default rate** — set on a team (e.g., all Local helpers default to $18/hr); applies to any member without an individual rate
3. **Role default rate** — set on a role type (e.g., all Leads default to $22/hr); fallback if no team rate is set

This means you can set a company-wide default for each role, override it per team, and further override it per individual — with no limit on customization.

**Pay Rate Types per crew member:**
- **Hourly** — standard rate per hour worked (pulled from timesheet clock-in/out)
- **Flat per job** — fixed amount per job event regardless of hours
- **Hourly + flat bonus** — hourly rate plus a fixed bonus per completed job

**Driver Commission (additional layer, optional per driver):**
- **Flat commission per job** — fixed dollar amount when the driver completes a job event
- **Percentage of job revenue** — percentage of the job's billed value (e.g., 5% of invoice)
- **Per-mile rate** — for LD drivers, a rate per mile driven (pulled from job origin/destination distance)
- **Combination** — e.g., hourly + per-mile, or flat + commission percentage
- Commission settings are per-driver and can be set independently from the base hourly rate

**Vehicle/Truck Cost Rates:**
- Each vehicle in the fleet has an assigned **cost-per-hour** or **cost-per-mile** rate (set in Fleet Management)
- Used for job costing only — not billed to customer directly unless added as an accessorial

#### Automatic Job Actuals Calculation
When a job event is completed and timesheets are submitted, the system auto-calculates the **actual cost** of the job:

```
Job Actual Cost =
  Σ (crew member hours × their effective hourly rate)
  + Σ (crew member commissions earned)
  + Σ (truck hours or miles × vehicle cost rate)
  + materials used (packing supplies at cost)
```

This gives dispatchers and managers a real **profit/loss per job event** and per file:
- Estimated revenue (from invoice) vs. actual labor + vehicle cost
- Margin per job visible in reporting
- Actuals are finalized once all timesheets for the job are approved
- Timesheet discrepancies (crew clocked more hours than estimated) are flagged for dispatcher review before actuals are locked

---

### MODULE 5B — Fleet Management
Manage all vehicles and equipment. Accessed by dispatchers, coordinators, admins, and the maintenance team.

#### Vehicle Profiles
- Add / edit / retire vehicles
- Per-vehicle fields: unit number, nickname, type (26ft box, 16ft box, cargo van, flatbed, sprinter), make, model, year, VIN, license plate, DOT number, registration expiry, insurance expiry
- Current status (see statuses below)
- Assigned home location / branch (for multi-location companies)
- Notes field

#### Vehicle Statuses
- **Active** — available for dispatch assignment
- **Assigned** — currently on a job (auto-set when assigned in dispatch)
- **In Maintenance** — being serviced; not available for dispatch; visible to maintenance team
- **Out of Service** — major issue; not available; flagged for maintenance
- **Reserved** — held for a specific upcoming job
- **Retired** — removed from active fleet; kept in records

Dispatch board only shows Active and Reserved vehicles as assignable. All other statuses are blocked from assignment with a visible reason.

#### Maintenance Tab
A dedicated view for the maintenance team (and admins) — separate from the dispatch board.

- List of all vehicles currently In Maintenance or Out of Service
- Per-vehicle maintenance record:
  - Issue description and date reported
  - Who reported it (crew member, dispatcher, or admin)
  - Current repair status: Reported → In Progress → Awaiting Parts → Complete
  - Assigned mechanic / shop (internal or external)
  - Estimated return-to-service date
  - Repair notes and history log
- Maintenance team can update repair status and add notes
- When status is set to Complete, dispatcher is notified and vehicle status returns to Active
- Alerts: vehicles with registration or insurance expiring within 30 days
- Any crew member can **report a vehicle issue** from the field — flagged to dispatcher and maintenance team immediately
- **Exceeds CompuMove:** Full maintenance workflow with repair status tracking and expiry alerts

---

### MODULE 6 — Crew & Mobile Operations
A separate, minimal-access portal for crew members. Accessed via the same web app on a phone or tablet — no separate native app required. Crew members log in and see only what they need for their workday.

#### Crew Portal — What Crew Members See
Crew access is intentionally limited:
- **Today's Jobs** — only the job events they are assigned to for the current day, in time-order
- Each job card shows: customer name, address (tap to open maps), time window, crew lead, truck, special instructions
- **Live job status** — if a coordinator or dispatcher updates a job (time change, address change, cancellation), the crew member sees it immediately with a notification
- No access to other jobs, other crew members' schedules, financial data, or any management features

#### Clock-In / Timesheet System
- **Clock In** button appears when crew member is within the start window of a scheduled job
- Clock in is per-job — tracks start and end time for each individual job event
- Crew can clock out at completion; lead can mark job as complete which triggers all crew clocking out
- Running timer visible while clocked in — crew can see their live hours
- End-of-day timesheet summary — total hours worked, jobs completed
- Timesheets flow to the back office automatically — no paper submission needed
- Dispatcher/coordinator can see live clock-in status on the dispatch board in real time

#### GPS Tracking (Phase 2)
- Optional GPS check-in at clock-in to verify crew is on-site (geofence against job address)
- Live crew location visible to dispatcher during job — useful for ETAs and routing
- Automatic travel time logging between jobs
- Designed as an opt-in feature per company; crew is notified when tracking is active

#### Field Actions (on assigned jobs)
- Photo capture at pickup — condition documentation before loading
- Photo capture at delivery — condition documentation after unloading
- Customer signature capture at pickup (BOL acknowledgment)
- Customer signature capture at delivery (job completion)
- Exception reporting — crew can flag damages, access issues, or delays with photo + note
- Packing material usage log — record actual boxes/materials used

#### Crew Notifications
- Push notification when assigned to a new job
- Push notification when job details change (time, address, crew size)
- Push notification when job is cancelled or rescheduled
- Notification when it is time to clock in (X minutes before job start)

---

### MODULE 7 — Bill of Lading & Forms
DOT/FMCSA compliant document generation. All documents are auto-populated from the job record and dispatch assignment — no re-keying of data.

#### Document Types
- **Bill of Lading (BOL)** — generated from job record + dispatch details: crew names, truck, estimated weight, inventory summary, carton counts, special notes, valuation, origin/destination, time window
- **Dispatch Ticket** — internal crew document: all job details, assigned crew members, truck, time window, special instructions, contact info. Generated when dispatch assignment is confirmed.
- **Order for Service**
- **High-Value Inventory Form**
- **Inventory Exception Form (PRE items)**
- **Delivery Receipt**
- **Warehouse Receipt**
- **Storage Agreement** (for storage-in accounts)

#### Generation Rules
- BOL and Dispatch Ticket are generated together when a dispatcher confirms crew + truck assignment
- If dispatch details change after generation, documents can be regenerated — version history is kept
- All forms include e-signature fields for customer and crew lead
- PDF download and email delivery to customer
- DOT/FMCSA required fields are enforced — system will not generate a BOL with missing required data
- **Exceeds CompuMove:** Digital BOL and dispatch ticket on mobile — crew receives dispatch ticket on their portal automatically; no paper required

---

### MODULE 8 — Rate Sheets & Tariffs
The pricing engine. Drives estimates, billing, and settlement.

- Local tariffs (hourly rates by crew size, truck size, market)
- Intrastate tariffs
- Interstate tariffs (CZAR-LITE / household goods weight-based)
- 400NG tariff integration (van line interstate)
- GSA-500A government/military tariff
- Custom contract pricing (commercial accounts, corporate relocation)
- Fuel surcharge management
- Accessorial charges (long carry, stairs, elevator, shuttle, storage-in-transit)
- Minimum charges
- Seasonal rate adjustments
- Rate sheet versioning (keep history when rates change)

---

### MODULE 9 — Billing & Invoicing
Where the money comes in. Billing is event-level — each job event under a file generates its own invoice, but all invoices are visible at the file level for a complete account view.

#### Billing Types
- **One-time** — generated on completion of a move, haul-out, or service event
- **Recurring** — auto-generated on a monthly cycle for permanent storage accounts; continues until storage is closed
- **Milestone** — for commercial/multi-day projects, invoiced at defined project milestones

#### Features
- Invoice generation per job event (not per file — each event bills separately)
- File-level billing summary — see all invoices across all events for one customer
- Actuals billing (final weight, hours, materials vs. estimated)
- Recurring storage invoices auto-generated on billing cycle date; admin can pause, adjust rate, or cancel
- Partial payments and payment schedules tracked per invoice
- Commission calculation per salesperson/event
- Revenue distribution (for van line agents — split billing)
- Accounts receivable tracking — filterable by file, event type, business line, aging bucket
- Overdue invoice alerts and follow-up reminders
- Invoice PDF with company branding
- QuickBooks integration (export or sync)
- **Exceeds CompuMove:** Automatic recurring billing engine, full AR view across all event types per file

---

### MODULE 10 — Warehouse & Storage Management
Full vault and item-level storage tracking.

- Vault inventory — vault number, size, contents, customer
- Item-level storage (loose storage, rack storage)
- Vault location tracking (row, section, bay)
- Full and empty vault tracking
- Check-in / check-out workflow
- Warehouse receiving protocol (inbound shipment receiving checklist)
- Condition documentation at receiving (photos, notes)
- Long-term storage vs. storage-in-transit (SIT) tracking
- SIT billing (daily/monthly rate)
- Delivery order management (pull from storage for delivery)
- Storage account history retained indefinitely
- Inventory audit tools
- **Exceeds CompuMove:** Barcode/QR scanning for vaults and items, warehouse map visual

---

### MODULE 11 — Commercial Moving
Separate workflows for commercial clients.

- Commercial account profiles (company, contacts, locations)
- Office move planning tools (floor plan notes, workstation inventory)
- Multi-day job support
- Project-based billing (milestones vs. single invoice)
- IT equipment handling protocols
- Commercial packing services tracking
- Facility access and security note fields
- Recurring commercial client management

---

### MODULE 12 — Long Distance & Interstate
- Weight ticket management (origin and destination weighmaster tickets)
- Actual weight billing vs. estimated weight
- Linehaul rate calculation
- Driver settlement / carrier pay
- Delivery spread date tracking (first/last available delivery date)
- Shipment status tracking (en route, at destination warehouse, out for delivery)
- Agent network management (origin/destination agents)
- Van line integration hooks (Allied, Mayflower, UniGroup, etc.)

---

### MODULE 13 — Reporting & Metrics
The intelligence layer. Over 250 report types targeted.

**Sales Reports:**
- Leads by source
- Conversion rate by salesperson
- Closed revenue by period
- Lost lead analysis
- Average job value

**Operations Reports:**
- Jobs per day/week/month
- Crew utilization (hours worked vs. available by crew member and team)
- Truck utilization (hours/miles per vehicle)
- Actuals vs. estimates variance (hours, crew size, materials)
- Claims rate
- Timesheet summary by crew member and period
- Crew hours by job type (local, LD, commercial, warehouse)

**Financial Reports:**
- Revenue by job type (local, LD, storage, commercial)
- Accounts receivable aging
- Commission reports by driver/salesperson
- Storage revenue
- **Profit/loss per job event** — revenue vs. actual labor + vehicle + materials cost
- **Profit/loss per file** — rolled up across all events for a customer
- **Labor cost by crew member** — hours × rate, total cost per period
- **Labor cost by team** — aggregate cost per team per period
- Margin analysis by job type, business line, and salesperson

**Custom Report Builder:**
- Export any data set to spreadsheet
- Hundreds of data points queryable per shipment
- Saved report templates

---

### MODULE 13A — Internal Task System
The communication and accountability backbone of the platform. Every role has a task queue. Tasks can be created manually or triggered automatically by system events. This is how the team stays coordinated across every step of the workflow without relying on texts, emails, or verbal handoffs.

#### What a Task Is
A task is an actionable item assigned to a specific user or role with:
- Title and description
- Assigned to: specific user or role (e.g., "all Local Dispatchers")
- Priority: Urgent / High / Normal / Low
- Due date / due time
- Linked record: job file, lead, invoice, crew member, vehicle, etc.
- Status: Open → In Progress → Complete → Dismissed
- Created by: user or System (auto-generated)

#### Task Inbox
Every user sees their personal task queue on login — sorted by priority and due date. Tasks appear in a persistent notification badge on the sidebar. Completing a task can trigger the next task in a workflow automatically.

#### Manual Tasks
Any user (within their permission level) can create a task and assign it to another user or role. Used for: follow-ups, reminders, approvals, internal handoffs.

#### Automatic Task Rules (Admin-Configured)
Admin builds trigger → action rules:

| Trigger Event | Example Auto-Task Created |
|--------------|--------------------------|
| New lead assigned to salesperson | Task: "Contact lead within 2 hours" → assigned to that salesperson |
| Estimate sent, no response in 3 days | Task: "Follow up on estimate EST-XXXX" → assigned to salesperson |
| Job booked | Task: "Confirm crew and truck assignment" → assigned to Dispatcher |
| Job dispatched (crew assigned) | Task: "Generate BOL and dispatch ticket" → assigned to Coordinator |
| BOL generated | Task: "Review and approve BOL before job date" → assigned to Coordinator |
| Job completed in field | Task: "Send post-move review request" → assigned to Salesperson |
| Job completed in field | Task: "Generate and send invoice" → assigned to Billing |
| Invoice overdue 7 days | Task: "Follow up on overdue invoice INV-XXXX" → assigned to Billing |
| Storage account created | Task: "Confirm vault assignment and billing start date" → assigned to Warehouse |
| Crew member reports vehicle issue | Task: "Vehicle issue reported — review and update status" → assigned to Maintenance |
| Date change request submitted | Task: "Date change requested for JOB-XXXX — approve or propose alternative" → assigned to Dispatcher |
| Date change approved | Task: "Notify customer of confirmed date change" → assigned to Coordinator |

#### Rule Builder (Admin Only)
- Select trigger event from a dropdown of all system events
- Select task template (title, description, priority, due window — e.g., "within 2 hours" or "1 day before job date")
- Select assignee: specific user, role, or the user who triggered the event
- Link to record: auto-link to the relevant job, lead, invoice, etc.
- Rules can be enabled/disabled without deleting them
- Rules are scoped per business line (HHG rules, Commercial rules, or both)

#### Task Visibility
- Users see only their own tasks
- Coordinators see their own tasks + tasks assigned to their team
- Dispatchers see their own tasks + all dispatch-related tasks across the board
- Admins and Owners see all tasks across all roles
- Tasks linked to a record also appear on that record's Activity tab

---

### MODULE 14 — Automation & Follow-Ups
Set it and forget it workflows. Customer-facing only — email and SMS sequences triggered by job events. For internal team tasks, see Module 13A.

- Lead response automation (instant reply to new inbound lead)
- Estimate follow-up sequence (Day 1, Day 3, Day 7 if not booked)
- Booking confirmation email/SMS
- Pre-move reminder (48 hours, 24 hours before move day)
- Post-move review request (Google, Yelp, etc.)
- Storage billing reminders
- Overdue payment reminders
- Birthday/anniversary touches for past customers
- Re-engagement campaigns for past customers
- Configurable trigger/action workflow builder

---

### MODULE 15 — Customer Portal
Self-service for the customer.

- Customer login to view their move details
- Download BOL, estimate, invoice
- Track shipment status
- Sign documents electronically
- Make payments online
- Submit claims
- Update delivery address/contact info
- Request storage delivery

---

### MODULE 16 — Integrations & API
Built for the future.

**Native Integrations (Phase 1):**
- QuickBooks Online / Desktop
- Google Calendar
- Google Maps (routing + distance)
- Stripe (payments)
- Twilio (SMS automation)
- SendGrid / Mailgun (email)

**Lead Source Integrations:**
- HireAHelper
- MovingHelp
- Moving.com
- Updater
- Custom webhook for any lead source

**Future / API Layer:**
- Public REST API for customer-facing integrations
- Webhook support (push events to external systems)
- van line system integrations
- DOT/FMCSA compliance data feeds
- Zapier / Make.com connector

---

### MODULE 17 — Admin & Settings
Platform configuration. Admin role only. Philosophy: **everything has a sensible default, everything is overridable.** Admins should never need to touch code — all operational rules are configured here.

#### Company & Branding
- Company profile: name, logo, DOT/MC numbers, insurance, address, contact info
- Document templates: BOL header, invoice branding, estimate letterhead

#### User & Role Management
- User accounts and role assignments
- **Custom Role Builder** — visual permission matrix (Full / Read-Only / Hidden per module), business line scope, data scope
- **Workflow Customization** — pipeline stages per business line (add, rename, reorder, remove)

#### Truck Type Configuration
Admins define the full fleet type library. Each truck type has:
- Name (e.g., "16ft Box Truck", "26ft Box Truck", "53ft Semi Trailer", "Cargo Van", "Sprinter Van")
- **Cubic footage capacity** — used by the estimating engine to calculate truck requirements
- **Pricing model** (per truck type, switchable):
  - **Per Day** — flat daily rate for the truck regardless of hours
  - **Truck + Driver Hourly** — combined hourly rate covering the truck and its driver together (common for local moves); driver is not billed separately from crew when this model is used
- Cost per mile (for LD job costing, separate from local pricing)
- Minimum crew requirement for this truck type (overrides global default)
- **Active / Available** — whether this truck type appears in the estimator and dispatch
- **Priority** — when auto-allocating trucks in the estimator, higher-priority types are preferred. Admins can drag to reorder priority.

**Default truck types shipped with the system (all editable):**

| Type | Capacity | Min Crew | Default Pricing |
|------|----------|----------|----------------|
| Cargo Van | 200 cu ft | 1 driver | Per Day |
| Sprinter Van | 350 cu ft | 1 driver | Per Day |
| 16ft Box Truck | 800 cu ft | 1 driver + 1 helper | Per Day or Truck+Driver Hourly |
| 26ft Box Truck | 1,500 cu ft | 1 driver + 1 helper | Per Day or Truck+Driver Hourly |
| 53ft Semi Trailer | 3,000 cu ft | 1 driver + 2 helpers | Per Day |

- Admins can add custom truck types at any time (e.g., "16ft Liftgate", "Flatbed 40ft")
- Admins can **disable** truck types their company doesn't own — disabled types never appear in the estimator or dispatch board
- Companies with only large trucks (e.g., 26ft and up) simply disable the smaller types

#### Truck Assignment in Estimating — Auto vs. Manual
- **Auto mode (default):** estimating engine allocates trucks based on total cubic footage and the company's active truck types in priority order
- **Manual override:** salesperson or coordinator can switch to manual mode on any estimate and specify exact truck types and quantities — overrides the auto-allocation entirely
- Both modes update crew minimums and pricing in real time
- Manual override is noted on the estimate so coordinators know it was not auto-calculated

#### Job Staffing Rules (Admin-Configurable Defaults)
Rules that auto-populate crew requirements when a job is created. All can be overridden per job by a dispatcher.

- **Minimum crew per truck** — e.g., every truck must have 1 driver + 1 helper. Set globally, overridable per truck type.
- **Supervisor requirement** — toggle on/off globally. When on, every job automatically requires 1 supervisor billed at supervisor rate. Can be marked "not required" on individual jobs.
- **Supervisor counts as driver** (default: on) — when enabled, the supervisor fills one of the truck driver slots and does not add to headcount. Total people on the job stays the same; one person is simply billed at the supervisor rate. When disabled, supervisor is an additional person above the calculated crew count. Togglable per estimate and per job.
- **Supervisor pay rate** — set separately from standard crew rates; applies automatically when supervisor is on a job
- **Minimum men per job** — regardless of truck, a job always needs at least N men (default: 2)
- **Hours per working day assumption** — used in estimating (default: 8 hours). Adjustable.
- **Estimating difficulty divisors** — the ÷N formula per difficulty level (Easy/Moderate/Hard/Very Hard) used to calculate man hours from cubic footage. All four values are editable.
- **Truck capacity thresholds** — cubic footage ranges that trigger each truck type recommendation in the estimator. Editable.

#### Estimating Rules Engine (Admin-Configurable)
The estimating tool is built on a set of rules that admins can configure to match their company's operations. All rules have defaults and can be changed without touching code.

**Built-in configurable rules:**
- Difficulty divisors (Easy/Moderate/Hard/Very Hard) — the ÷N formula per difficulty level
- Hours per working day assumption
- Minimum men per job (floor on crew count regardless of formula result)
- Minimum crew per truck type
- Supervisor required by default (on/off)
- Supervisor counts as driver (on/off) — whether supervisor fills a driver slot or is additional headcount
- Supervisor pay rate
- Truck pricing model per type (per day or truck+driver hourly)
- Active truck types (which types appear in the estimator)
- Truck priority order for auto-allocation

**Future: Custom Rule Builder**
Admins will be able to create entirely new estimating rules beyond the built-in set. Examples:
- "Jobs over 2,000 cu ft always require a lead crew member at lead rate"
- "Any job with stairs automatically adds 10% to man hours"
- "Commercial jobs always require a minimum of 4 men"
- "LD jobs always require 2 drivers"
These rules apply automatically during estimation and are visible on the estimate so salespeople understand why a figure was set.

#### Billing & Rate Defaults
- Default hourly rate by role (Lead, Driver, Helper, Supervisor, Warehouse) — fallback if no individual or team rate is set
- Default truck cost rates per type
- Default accessorial charges (stairs, long carry, elevator, shuttle)
- Storage rate defaults by vault size

#### Automation & Task Rule Builder
- Task trigger rules (see Module 13A)
- Customer-facing email/SMS automation sequences (see Module 14)

#### System
- Branch/location management (multi-location companies)
- Notification preferences per role
- Audit log (who changed what, when, from what value to what value)
- Data import tools (migrate from CompuMove or spreadsheets)
- Backup and export

---

## Role-Based Access Control (RBAC)

Every user is assigned a role. Roles control which modules appear in the sidebar, which actions are available, and what data is visible. Roles are fully customizable by Admin.

### Default System Roles

These ship as defaults but can be edited, renamed, or replaced by the Admin.

| Role | Business Line | Description |
|------|--------------|-------------|
| **Admin** | Both | Full access to everything — all modules, all data, system config, role management |
| **Owner / Manager** | Both | Full operational access + reporting across HHG and Commercial; no system config |
| **HHG Coordinator** | HHG | Full HHG CRM, all leads/estimates across salespeople, HHG Jobs, Scheduling, BOL & Forms |
| **HHG Sales / Estimator** | HHG | HHG CRM (own leads only), Estimating (own leads only), Quotes (own leads only) |
| **Commercial Coordinator** | Commercial | Full Commercial CRM, all commercial leads/estimates, Commercial Jobs, Scheduling |
| **Commercial Sales / Estimator** | Commercial | Commercial CRM (own leads only), Estimating and Quotes (own leads only) |
| **Local Dispatch** | Both | Jobs (local), Scheduling, Crew & Mobile, BOL & Forms |
| **LD Dispatch** | Both | Jobs (long distance), Scheduling, Crew & Mobile, BOL & Forms, Long Distance module |
| **Billing** | Both | Billing & Invoicing, Rate Sheets, financial Reporting only |
| **Warehouse** | Both | Warehouse & Storage only |
| **Crew / Driver** | Both | Crew & Mobile view only (daily jobs, clock-in, signatures, photos, vehicle issue reporting) |
| **Maintenance** | Both | Fleet Management — maintenance tab only (vehicle repair status, notes, return-to-service updates). No access to jobs, crew, or financial data. |
| **Customer** | Both | Customer Portal only |

### Custom Role Builder (Admin Only)
- Admin can create entirely new roles with any name
- Per-module permission is set via a visual matrix: **Full / Read-Only / Hidden**
- Business line scope can be set per role: **HHG only / Commercial only / Both**
- Data scope can be set: **Own records only / All records in their business line / All records**
- Changes to a role apply immediately to all users assigned that role

### Permission Levels Per Module

- **Full** — read, write, create, delete
- **Read-Only** — view only, no edits
- **Hidden** — module does not appear in navigation at all

### HHG vs. Commercial Separation

The platform has two distinct business lines that operate in parallel:

**Separation rules:**
- When a job/lead is created, it is designated **HHG** or **Commercial** — this cannot be changed after creation
- HHG roles see only HHG pipelines, dashboards, and jobs
- Commercial roles see only Commercial pipelines, dashboards, and jobs
- A user can be assigned a role that spans both (e.g., Admin, Owner, Dispatcher, Billing) — they see both
- Each business line has its own **dashboard**, **CRM pipeline**, and **reporting views**

**Shared resources (visible to both):**
- Crew & Drivers — scheduling and dispatch pulls from one shared workforce pool
- Trucks & Equipment — shared fleet, visible to both dispatch roles
- Warehouse & Storage — shared facility
- Billing & Invoicing — single AR view but filterable by business line

**Workflow customization:**
- HHG pipeline stages and Commercial pipeline stages are configured **independently**
- Admin can add, remove, rename, and reorder stages for each business line separately
- Automation rules and follow-up sequences are also configured per business line

### Key Rules
- Sidebar navigation renders dynamically based on role + business line scope
- All data reads and writes are scoped server-side — UI hiding alone is not the security boundary
- Admin is the only role that can create/edit roles, users, and workflows
- Audit log captures every action with user, role, timestamp, and record regardless of role

---

## Features That Exceed CompuMove 8

| Area | CompuMove 8 | Our Target |
|------|------------|------------|
| Estimating | Room-by-room, desktop/tablet | + AI item recognition from photos |
| BOL | Paper + PDF | Fully digital mobile BOL, no paper |
| Dispatch | Calendar + reports | Drag-and-drop board + capacity heatmap |
| Automation | Basic follow-ups | Full workflow builder, multi-channel |
| Warehouse | Vault tracking | + Barcode/QR scanning + visual map |
| Reporting | 250+ preset reports | + Custom report builder + live dashboards |
| Customer | No portal | Full customer self-service portal |
| Payments | Basic billing | Invoice generation, AR tracking, payment status logging |
| Mobile | Tablet estimating | Full crew mobile app with photos + signatures |
| API | Closed system | Open REST API + webhooks |

---

## Build Order Recommendation

Build in this sequence — each module depends on the one before it:

1. **Auth + Admin** (user accounts, company setup) — foundation
2. **CRM + Leads** — first thing any user touches
3. **Estimating** — converts leads to jobs
4. **Jobs + Rate Engine** — core record + pricing
5. **Scheduling + Dispatch** — operations
6. **BOL + Forms** — generated at dispatch, required before job goes live
7. **Billing + Invoicing** — money in
8. **Warehouse + Storage** — storage clients
9. **Reporting** — intelligence layer
10. **Automation** — efficiency layer
11. **Customer Portal** — customer-facing
12. **Integrations + API** — ecosystem

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Next.js (React) |
| Backend | Next.js API routes (full-stack) |
| Database | PostgreSQL (via Supabase) |
| Auth | Supabase Auth |
| Hosting | Vercel (app) + Supabase (DB + storage) |
| Mobile | Responsive web — same Next.js app, no separate native app |
| Payments | Invoice-based only — no payment processing |
| SMS | Twilio |
| Email | SendGrid / Mailgun |

---

## What We're NOT Building (Yet)

- Full accounting / general ledger (use QuickBooks integration instead)
- International / customs clearance workflows (Phase 2)
- Fleet maintenance tracking (Phase 2)
- Employee HR / payroll (use integration instead)

---

*Document created: 2026-05-30*  
*Next step: Decide tech stack and start Module 1 (Auth + Admin)*
