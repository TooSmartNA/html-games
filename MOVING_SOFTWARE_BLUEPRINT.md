# Moving Software — Master Blueprint
**Project Codename:** MovePro  
**Goal:** Build a full-service moving company platform that matches and exceeds CompuMove 8  
**Status:** Active prototype development — feature discovery phase  
**Prototype repo:** `github.com/TooSmartNA/moving-software` (Next.js, private)  
**Blueprint repo:** `github.com/TooSmartNA/html-games` (MOVING_SOFTWARE_BLUEPRINT.md)

---

## What We're Building

A complete, cloud-based moving company management platform covering every touchpoint of the business — from the first inbound lead to the final invoice, warehouse receipt, and reporting. Built modular so features can be developed one at a time and connected together.

---

## Prototype Status

The prototype is a visual/interactive frontend built in Next.js with fake data. No real backend yet. It is used as a feature discovery tool — screens reveal new requirements which feed back into this blueprint before being refined in the prototype.

**Screens built (prototype):**

| Screen | Route | Status |
|--------|-------|--------|
| Dashboard | `/` | ✅ Built — KPI cards (all linked), recent jobs/leads, alerts |
| CRM Pipeline | `/crm` | ✅ Built — pipeline kanban + task-driven view with urgency system; both cards link to lead detail |
| Lead Detail | `/crm/[id]` | ✅ Built — Overview (move details, salesperson assignment), Attachments (file list, upload from PC, BOL placeholder), Activity log |
| Estimating | `/estimating` | ✅ Built — flat item list, truck allocation engine, pricing model toggle, admin rate config, supervisor-as-driver rule |
| Jobs List | `/jobs` | ✅ Built — list with type/status badges, links to detail |
| Job Detail | `/jobs/[id]` | ✅ Built — 5 tabs: Overview, Inventory, Documents, Activity; **Billing tab** shows full actuals review (crew timesheets with clock-in/out, flagged overtime, truck, materials, estimated vs actual comparison table, Generate Invoice button) |
| Scheduling & Dispatch | `/dispatch` | ✅ Built — month/week/day views, drag-and-drop crew assignment, truck dropdown, unassign via X, date change modal, **dispatcher men count override with +/− controls and "Adjusted" flag** |
| Crew & Fleet Management | `/crew` | ✅ Built — Crew Members tab (add/edit/remove, availability toggle, absence log with types/dates, restriction tags); Fleet tab (add/edit/remove, inline status change with note, maintenance surfaced first) |
| Billing & Invoicing | `/billing` | ✅ Built — 4 tabs: Pending Review (**3 billing paths**: Bill Estimate / Bill Actual & Send / Edit Invoice with editable line items), All Invoices (filterable, expandable rows, Mark Paid), AR (aging buckets + by-customer), Recurring Billing |
| Customer Accounts | `/customers` | ✅ Built — list with tags, revenue, ratings |
| Customer Profile | `/customers/[id]` | ✅ Built — stats row, pinned note, Jobs / Storage / Invoices / Communications tabs |
| BOL & Forms | `/bol` | ✅ Built — document list with type/status badges |
| BOL Viewer | `/bol/[id]` | ✅ Built — full DOT-formatted document with print/download/send |

**Deferred for later in prototype:**
- Role preview toggle — switch between role views (Dispatcher, Coordinator, etc.) to see sidebar and data scope change

**Workflow:** Brain dump → blueprint first → prototype built → prototype reveals new needs → back to blueprint

---

---

## Module Map (Build Order TBD)

### MODULE 0 — Dashboard
The landing screen after login. Gives each user a real-time snapshot of what needs attention today. Content is role-scoped — each role sees only the KPIs and alerts relevant to them.

#### KPI Cards (role-dependent)
- Open Leads (links to CRM)
- Jobs Today (links to Dispatch)
- Jobs This Month (links to Jobs list)
- Open Invoices / AR value (links to Billing)
- Storage Units occupied/total (links to Warehouse)
- Revenue This Month (links to Reporting)

#### Recent Activity
- Recent Jobs — last 5 jobs with customer, ID, type, date, status; each row links to job detail
- Recent Leads — last 5 leads with name, source, value, pipeline stage; links to CRM

#### Alerts & Reminders
- Overdue invoices
- Estimates with no response past X days
- Completed jobs needing review request
- Other auto-generated alerts from the task system
- Each alert is clickable and links to the relevant record

#### Role Scoping
- Salesperson sees: their leads, their estimates, their jobs
- Dispatcher sees: today's dispatch board, unassigned/partial jobs, crew availability
- Coordinator sees: all leads, all jobs, overdue follow-ups
- Admin/Owner sees: full KPI set with revenue and margin data

---

### MODULE 1 — CRM & Lead Management
The front door of the business. Every job starts here.

- Inbound lead capture (web form, phone, email, third-party lead sources)
- Lead source tracking (where did this lead come from?)
- Contact & account profiles (household vs. commercial)
- Full communication history log per lead/customer (calls, emails, notes)
- Automated follow-up sequences (email/SMS drip campaigns)
- Follow-up reminders and task assignments
- Duplicate detection
- Lost lead reasons tracking
- Re-engagement workflows for cold leads
- **Exceeds CompuMove:** AI-assisted lead scoring, automated review requests post-move

#### CRM Views — Pipeline vs. Task-Driven
The CRM has two distinct views. Admin sets the company default; individual users can toggle between them.

**Pipeline View (Kanban)**
- Horizontal kanban board — one column per stage (New Lead, Contacted, Estimate Sent, Follow-Up, Quoted, Booked)
- Each lead is a card showing customer, origin/destination, move date, value, quick-action buttons
- Best for visualizing the shape of the pipeline and spotting bottlenecks by stage
- Stages are configurable per business line (HHG vs. Commercial) by Admin

**Task-Driven View**
- Lead-first layout — each lead is a row or card with its **active task displayed prominently**
- The next required action (the task) drives the UI — pipeline stage is secondary information
- Tasks are auto-generated by system events (see below) and appear on the lead with due date and urgency
- Overdue tasks are flagged red; due today are amber; upcoming are neutral
- Sort/filter by: overdue first, due date, salesperson, lead stage, value, source
- Salesperson sees only their leads; coordinator sees all
- Clicking a task marks it complete and triggers the next auto-task in the sequence

**Auto-generated task sequences (admin-configurable):**

| Trigger | Task Created | Assigned To | Due |
|---------|-------------|-------------|-----|
| New lead received | "Assign to salesperson" | HHG Coordinator | Same day |
| Lead assigned to salesperson | "Make first contact" | Salesperson | Within 2 hrs |
| First contact made | "Schedule estimate or send online estimate" | Salesperson | Within 24 hrs |
| Estimate sent | "Follow up — did they receive it?" | Salesperson | +1 day |
| No response after estimate | "Follow up — check interest" | Salesperson | +3 days |
| No response after 2nd follow-up | "Final follow-up or mark lost" | Salesperson | +7 days |
| Quote accepted / lead booked | "Create job record and confirm move date" | Coordinator | Same day |
| Lead marked lost | "Log lost reason" | Salesperson | Same day |

- All task due windows are admin-configurable
- Tasks can be dismissed, snoozed, or completed manually
- Completing a task may auto-create the next one in the sequence
- Admin can add, remove, or modify any task rule in the Task Rule Builder (Module 13A)

**Admin setting:** Default CRM view (Pipeline / Task-Driven) — set per company, overridable per user role

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

#### Lead Detail Page
Clicking any lead card (in either pipeline or task view) opens the full lead file.

**Header:**
- Contact name, lead ID, hot flag, pipeline stage badge
- Contact info strip (phone, email, origin → destination, move date)
- Active task banner — amber strip showing the current task, due date, and a Complete button (always visible, impossible to miss)
- Open Estimator button (links to estimating tool pre-loaded for this lead)
- Mark Booked button

**Tabs:**
- **Overview** — origin/destination addresses with access notes, move date + flexibility, estimated value, services requested, customer notes; salesperson assignment dropdown (change directly from this page); coordinator, source, created date
- **Attachments** — all files associated with this lead/job: estimates, BOL (once generated), signed paperwork, any uploaded documents; Upload File button to attach from PC; BOL placeholder card shown until lead is booked and dispatched
- **Activity** — full chronological log of all actions (notes, emails, status changes, assignments); note input to log calls or updates

**Design principle:** Lead detail is the salesperson's primary workspace — everything they need to progress the lead is on this one page without navigating away.

---

### MODULE 2 — Estimating
The core sales tool. Must be fast, accurate, and usable in the field.

#### Inventory Builder
- **Flat item list** (not room-by-room) — all items in a single searchable list, organized by category for browsing
- Preset item library with 60+ common household and commercial items, each with pre-set cubic footage
- Category filter (Living Room, Bedroom, Dining Room, Kitchen, Garage/Outdoor, Boxes, Misc)
- Custom item entry: add any item with a name, custom cubic footage, and note
- Qty +/− per item; inline note field per item
- Simple **Rooms** count field in the header (optional, for reference only — not structural)
- Running total cubic footage updates live as items are added

#### Calculation Engine
- **Cubic footage → truck allocation** — auto-allocates truck types based on total cube and company's active fleet (admin-configurable truck types with capacities)
- Manual truck override — salesperson/coordinator can switch to manual mode and specify exact truck types and quantities
- **Man-hours formula:** total cube ÷ difficulty divisor = total man-hours needed
  - Difficulty levels: Easy (÷45), Moderate (÷38), Hard (÷32), Very Hard (÷28) — all admin-editable
- **Crew calculation:** man-hours ÷ (targetDays × hoursPerDay) = men needed; raised to minimum if truck staffing rules require more
- **Schedule toggle:** 1, 2, or 3 days — adjusts crew count and hours/man/day in real time
- Optimization tip shown when a different day count would be more efficient

#### Pricing & Billing
- Crew rate: $/hr per crew member
- Supervisor rate: $/hr (separate from crew; supervisor can count as driver — configurable)
- Truck pricing: per day OR truck+driver hourly (per truck type, admin-configurable)
- All rates are admin-configurable defaults; changes on an individual estimate affect that estimate only
- Estimate breakdown shows: crew (with hrs ea.), supervisor, each truck type with pricing model label

#### Other Features
- Binding vs. non-binding estimate types
- Estimate history — full change log from first contact through job completion
- Mobile-friendly (responsive web — same estimating tool on tablet/phone)
- Virtual survey support (video call or photo upload)
- Multiple estimate versions per job
- Estimate PDF generation with company branding
- Digital signature on estimates (legally binding under ESIGN Act)
- Automatic conversion from estimate → quote → job
- **Exceeds CompuMove:** Real-time cube-based calculation, configurable rules engine, admin rate management

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
The customer profile has a dedicated Storage tab. If the customer has active storage, it is surfaced prominently. The profile shows a **summary view only** — full item-level detail lives in the Warehouse & Storage module to keep the profile clean and uncluttered.

**Per active storage account, the summary card shows:**
- Vault number and warehouse location (row/section)
- Vault size
- Status badge (Active / Pending Delivery / Closed)
- In storage since date and source job reference
- Monthly rate, billed to date, next billing date
- **3-stat summary:** total items count, total cubic feet, billed to date
- No item-level breakdown — that lives in the Warehouse module

**Quick actions on each storage card:**
- **Schedule Haul Out** — primary action, creates a Haul Out job event
- **Partial Delivery** — initiate delivery of selected items
- **View Full Vault →** — navigates to the Warehouse & Storage module for full item inventory, condition notes, and vault management

**If a customer has multiple storage accounts**, each appears as a separate card.

**Design decision:** Item-level inventory is intentionally NOT shown on the customer profile — it would muddy the overview. The warehouse module is the right place for that depth.

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
- **Number of men** — originally set by coordinator/estimator based on the job estimate. Dispatcher can **override this up or down** directly on the dispatch board at any time. When the dispatcher's count differs from the original estimate, a visible flag ("Adjusted" tag) appears on the job card so coordinators and managers can see the change at a glance.
- **Estimated hours** for the job (drives billing estimate and crew schedule)
- **Truck type** required: 26ft box, 16ft box, cargo van, flatbed, etc.
- **Number of trucks** required
- These fields feed directly into BOL and dispatch ticket generation — no separate data entry

**Dispatcher override philosophy:** Dispatchers have the most accurate real-world context — traffic, crew availability, job complexity on the day. They must have full authority to adjust any resource requirement without needing approval. Any adjustment is logged on the job record with timestamp and who changed it.

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

#### Time-Off & Absence Management
Pre-scheduled and unplanned unavailability tracked per crew member. All absence records block that crew member from dispatch assignment for the affected dates automatically.

**Absence Types:**
- **PTO (Paid Time Off)** — pre-scheduled; set by coordinator or admin with a date range; crew member appears blocked on dispatch for those dates
- **Call Off** — unplanned same-day or short-notice absence; logged by dispatcher or coordinator when crew calls out; notes field for context
- **No Show** — crew did not show and did not call; flagged separately for HR tracking
- **Injury / Medical Leave** — date range with an optional estimated return date; can be open-ended until cleared
- **Suspension** — administrative; blocks dispatch until lifted by admin
- **Other** — general unavailability with custom label and date range

**Restriction Tags (separate from absence — crew may be present but limited):**
- **Light Duty** — crew member is available but cannot perform heavy lifting or certain tasks; flagged on dispatch board so dispatcher knows
- **No Driving** — available for labor but cannot drive a truck (e.g., license issue, medical restriction)
- **Certification Lapsed** — e.g., CDL expired, DOT physical overdue; blocks from being assigned as driver until resolved; alert sent to admin
- **Probationary** — flag for new or returned crew; no special restrictions but visible to dispatchers
- Custom tags can be added by admin

**Behavior on Dispatch Board:**
- Crew members with active absences do not appear in the draggable roster for blocked dates
- Crew members with restriction tags appear in the roster but with a visible warning icon — dispatcher sees the restriction before assigning
- Hovering/clicking the warning icon shows what the restriction is

**Absence Log:**
- Per crew member profile: full history of all absences and restrictions with dates, type, who logged it, and notes
- Running totals: PTO used, call-offs this year, etc. (for internal reference — not payroll)

**Notifications:**
- When PTO is approved/logged: crew member notified; any already-scheduled jobs on those dates are flagged for dispatcher review
- When a crew member calls off: dispatcher and coordinator get an immediate alert; jobs scheduled for that day are flagged as needing replacement

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

#### Document List View
- All documents across all jobs listed in one place, filterable by type, status, date, customer
- Status badges: Draft, Sent to Crew, Signed, Completed, Pending Signature
- Actions per document: View, Download PDF, Send to Customer
- Draft documents show a prominent Send action

#### Document Viewer
- Full rendered document view with all auto-populated fields
- Toolbar: Print, Download PDF, Send to Customer
- Document sections: carrier/shipper info, origin/destination addresses, crew/equipment details, inventory summary table, valuation coverage, estimated charges breakdown, signature lines
- Special instructions highlighted (orange) for crew visibility
- Status indicator at the bottom (draft/signed/completed)
- Back navigation to the document list and linked job reference

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

#### Actuals Review & Invoice Approval Flow
After a job event is marked complete in the field, the billing team reviews the actuals before generating the final invoice. This prevents invoicing based on estimates when real numbers are available.

**What feeds the actuals:**
- **Labor:** crew timesheet clock-in/out per person × their pay rate. System calculates total hours per person and total labor cost. If any crew member clocked more hours than the job estimate, those lines are flagged.
- **Trucks:** hours the truck was on the job (derived from crew clock-in/out window) × truck cost rate
- **Materials:** packing supplies logged by crew during the job (boxes used, wardrobe boxes, etc.)

**Actuals display on the Job Billing tab:**
- Side-by-side comparison: Estimated vs. Actual per line item (labor, truck, materials)
- Variance column: over/under vs. estimate, colored red if over, green if under
- Each crew member's timesheet shown individually: name, clock-in, clock-out, hours, rate, total
- Timesheet flagged if hours significantly exceed estimate (dispatcher must review before billing approves)
- Total actual cost vs. estimated — the difference is the job margin impact

**Invoice generation workflow (not "approval of actuals" — actuals are facts):**
1. Job marked complete in field → auto-task created for billing team
2. Job appears in billing module's **Pending Review** queue
3. Billing opens the entry → reviews actuals (timesheets, truck, materials) vs. original estimate
4. If actuals have flagged overtime or unexpected costs: note the reason, then proceed
5. Three paths from here:
   - **Bill Estimate** — invoice created using the original estimated amount, not actuals. Used when the customer was quoted a fixed price and that's what they'll pay regardless of what the job cost.
   - **Bill Actual & Send** — invoice created from actuals as-is and sent immediately, no editing
   - **Edit Invoice** — opens editable invoice pre-filled from actuals; billing can adjust line amounts, remove lines, add custom lines, add notes, then send. Total updates live. Shows variance vs actuals if adjusted.
6. Invoice sent to customer; job drops from Pending queue
7. Timesheets lock after invoice is sent — no changes without admin override

**Key distinction:** The billing team is reviewing the actuals to *understand* the job cost before sending. They are not "approving" the actuals — those are what they are. The action is generating and sending the invoice, with or without adjustments.

#### Billing Module — Four Views
The billing module is organized into four tabs:

- **Pending Review** — completed jobs awaiting invoice. Each card shows customer, job type, estimated total, actual total, and variance at a glance. Three billing paths per card:
  - **Bill Estimate** — invoice sent for the original estimated amount, regardless of actuals. Used for fixed-price jobs where customer was quoted a set price.
  - **Bill Actual & Send** — invoice created from actuals as-is and sent immediately, no editing
  - **Edit Invoice** — opens an inline panel with three sub-tabs:
    - *Actuals:* read-only crew timesheets (clock-in/out, hours, rate, cost), equipment, materials
    - *Bill Estimate:* read-only original estimate breakdown with Send button
    - *Edit Invoice:* editable invoice pre-filled from actuals; adjust amounts, remove lines, add custom lines, add notes; live total; shows variance vs actuals if adjusted; Send button
  - After sending via any path, job drops from Pending queue and appears in All Invoices
- **All Invoices** — full invoice ledger. Filterable by status (Draft/Sent/Partial/Overdue/Paid), business line (HHG/Commercial), billing type (One-time/Recurring/Milestone), and search. Each row expandable: shows file/job reference, salesperson, partial payment input, balance. Mark Paid button updates in real time.
- **Accounts Receivable** — aging bucket summary cards (Current / 1–30 / 31–60 / 61–90 days) with totals; outstanding AR grouped by customer sorted by balance showing oldest invoice and worst aging bucket.
- **Recurring Billing** — active storage billing accounts with monthly rate, next billing date, and actions: Adjust Rate, Pause, Resume, Cancel.

#### Other Billing Features
- Recurring storage invoices auto-generated on billing cycle date; admin can pause, adjust rate, or cancel
- Partial payments and payment schedules tracked per invoice
- Commission calculation per salesperson/event
- Revenue distribution (for van line agents — split billing)
- Overdue invoice alerts and follow-up reminders (auto-task to billing team)
- Invoice PDF with company branding
- QuickBooks integration (export or sync)
- **Exceeds CompuMove:** Pending review queue with full actuals breakdown before invoicing; automatic recurring billing engine; full AR aging view

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

#### Theme & Brand Customization (Admin Only)
The platform's visual appearance is customizable per company so it can match their brand. All theming is done through the Admin panel — no code required.

**Layout Templates (pick one as the base):**
- **Professional Dark Sidebar** — dark navy sidebar, clean light content area (default; the premium SaaS look)
- **Full Light** — all-light, minimal feel
- **Full Dark** — dark throughout, high contrast
- More templates can be added over time

**Brand Color Customization:**
- Primary accent color — used for active states, buttons, links, highlights (pick from palette or enter hex/brand code)
- Sidebar background color — default is deep navy; can be changed to match brand (e.g., company's dark green, charcoal, etc.)
- Sidebar text/icon color — auto-calculated for contrast, or manually set

**Color Palette Options (presets):**
- Navy Blue (default)
- Charcoal
- Forest Green
- Deep Burgundy
- Slate Gray
- Midnight Black
- Custom (hex input)

**Company Logo:**
- Upload company logo — appears in the sidebar header and on all generated documents (BOL, estimates, invoices)
- Light and dark variants of the logo can be uploaded separately

**Document Branding:**
- BOL, estimates, invoices, and dispatch tickets use the company name, logo, and primary color for headers
- Footer text configurable (DOT/MC number, address, contact info)

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

### UX Principle for Limited-Role Views
The moving industry workforce is often not tech-native. For users with limited roles (Crew, Dispatcher, Salesperson, Warehouse), the UI must be **immediately obvious** — they should never have to think about what to do next.

**Design rules for limited-role views:**
- The most important action for the day is **above the fold and impossible to miss** — not buried in menus
- Task-driven interfaces are preferred over pipeline/dashboard views for operational roles
- Crew portal: one screen, their jobs for today, giant clock-in button — nothing else
- Dispatcher: unassigned and partial jobs flagged red/amber at the top, drag-and-drop is the primary interaction
- Salesperson: overdue tasks shown first in red, action buttons are clear and labeled (not icon-only)
- Warehouse: current jobs requiring their attention listed in order of urgency
- All limited-role views use larger touch targets, high-contrast status indicators, and minimal navigation
- When something is overdue or requires immediate action, it should feel urgent — not just a subtle color change
- Error states and missing information (e.g., unassigned crew on a job) are prominent warnings, not footnotes
- Avoid jargon in field-facing interfaces — "Clock In" not "Submit Time Entry", "Job Complete" not "Mark Event as Fulfilled"

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
- Employee HR / payroll (use integration instead)
- Native mobile apps (iOS/Android) — mobile is covered by responsive web

**Note:** Fleet maintenance tracking was initially listed here but is now included in Module 5B — it was determined to be core operational functionality, not a Phase 2 item.

---

## Build Order Recommendation

Build in this sequence — each module depends on the one before it:

1. **Auth + Admin** (user accounts, roles, company setup, fleet config, staffing rules) — foundation
2. **CRM + Leads + Customer Accounts** — first touchpoint; customer accounts link to all future modules
3. **Estimating** — converts leads to jobs; requires rate config from Admin
4. **Jobs + Rate Engine** — core record + pricing; requires customer accounts
5. **Scheduling + Dispatch** — operations; requires jobs and crew management
6. **BOL + Forms** — generated at dispatch; requires dispatch details
7. **Billing + Invoicing** — money in; requires completed jobs
8. **Warehouse + Storage** — storage clients; requires jobs for Storage In events
9. **Reporting** — intelligence layer; requires data from all above
10. **Internal Task System** — threads through all roles and modules
11. **Automation** — customer-facing email/SMS; requires jobs and leads
12. **Customer Portal** — customer-facing self-service
13. **Integrations + API** — ecosystem connections

---

*Document created: 2026-05-30*  
*Last audited: 2026-05-30 (third pass) — prototype and blueprint fully synced*
