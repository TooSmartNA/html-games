# Moving Software — Master Blueprint
**Project Codename:** MovePro  
**Goal:** Build a full-service moving company platform that matches and exceeds CompuMove 8  
**Status:** Active prototype development — feature discovery phase  
**Prototype repo:** `github.com/TooSmartNA/moving-software` (Next.js, private)  
**Blueprint repo:** `github.com/TooSmartNA/html-games` (MOVING_SOFTWARE_BLUEPRINT.md)

---

## What We're Building

A complete, cloud-based moving company management platform covering every touchpoint of the business — from the first inbound lead to the final invoice, warehouse receipt, and reporting. Built modular so features can be developed one at a time and connected together.

## Business Context

**Product type:** B2B SaaS — sold to moving companies  
**Target market:** Mid-to-large moving companies (HHG, commercial, long distance, or mixed)  
**Pricing target:** ~$10,000/month per client — enterprise positioning, white-glove onboarding, full white-label  
**Competitive benchmark:** Exceeds CompuMove 8 (the current industry standard desktop software) in every category  
**Launch strategy:** Stress-test with the owner's own moving company first as Tenant #1. Validate the product in a real operational environment before selling to external clients.  
**Build approach:** Owner directs all product decisions. Developer (Claude Code) makes all technical implementation decisions. Owner does not write code manually — builds via AI-assisted development.  
**Developer skill level:** Owner is a domain expert (moving industry) and strong product thinker, but a beginner at software development. All technical explanations should be clear and jargon-free. When there is one logical right answer technically, just implement it — don't ask.

## Product Philosophy — The Market Opportunity

90%+ of moving companies are operating on outdated systems. More advanced software exists — that's not the gap. The real gap is **adoption resistance**. These companies have built their workflows over years and are afraid that switching to something new will break what's already working and disrupt the people running it day to day.

This is where MovePro has a unique and specific advantage:

**The strategy is not to force change — it's to bridge to it.**

MovePro is designed to be customizable enough that a company can keep their core processes largely intact while gaining the modern tools they've been missing. The customization is not about overwhelming them with options — it's about giving them enough control that the transition feels safe rather than threatening.

- Pipeline stages are editable — they can match what the company already calls things
- Task rules are configurable — their existing follow-up process maps directly in
- Rate sheets follow their existing pricing model — no forced restructuring
- Roles and permissions match their existing org structure — no one loses authority
- Business lines (HHG/Commercial) can be used separately or together — fits how they're already organized

The result: a client can look at MovePro and see their own business reflected back at them, just running on better infrastructure. That's the sales advantage. They're not being asked to abandon how they work — they're being shown a version of how they already work that doesn't require spreadsheets, whiteboards, and tribal knowledge to hold together.

**Design principle that follows from this:** Every feature should have sensible defaults that work out of the box, and enough configuration to accommodate how a specific company already operates. We do not over-engineer customization for its own sake — we customize where it lowers the barrier to adoption. Simplicity wins interest. Flexibility closes deals.

---

## Prototype Status

The prototype is a visual/interactive frontend built in Next.js with fake data. No real backend yet. It is used as a feature discovery tool — screens reveal new requirements which feed back into this blueprint before being refined in the prototype.

**Screens built (prototype):**

| Screen | Route | Status |
|--------|-------|--------|
| Dashboard | `/` | ✅ Built — KPI cards (all linked), recent jobs/leads, alerts |
| CRM Pipeline | `/crm` | ✅ Built — **fully live state**: create new leads (slide-in form with name, phone, email, origin, destination, move date, estimated rooms, source, salesperson, starting stage, notes, Hot Lead toggle), advance any lead through stages via "→ Next Stage" button or stage dropdown on each card; pipeline value/counts update live; persisted to localStorage so detail-page edits reflect on return |
| Lead Detail | `/crm/[id]` | ✅ Built — **fully functional**: reads lead from localStorage (works for newly created leads too); clickable stage badge dropdown; active task banner with Complete button (auto-advances stage, logs to activity); Mark Booked button → View Jobs link; salesperson dropdown persists; Hot Lead toggle; estimated value editable inline; post note → activity feed with timestamp; all changes sync back to localStorage |
| Estimating | `/estimating` | ✅ Built — flat item list, truck allocation engine, pricing model toggle, admin rate config, supervisor-as-driver rule; **Generate Quote button** saves estimate to quotes module |
| Quotes & Proposals | `/quotes` | ✅ Built — quote lifecycle (Draft → Sent → Viewed → Accepted/Declined/Expired), expandable line items table, send/duplicate/convert-to-job actions, Templates tab; receives pre-filled drafts from Estimator via Generate Quote |
| Jobs List | `/jobs` | ✅ Built — list with type/status badges, links to detail |
| Job Detail | `/jobs/[id]` | ✅ Built — **6 tabs**: Overview, Inventory, Documents, **Timesheets** (crew-facing: clock in/out with no rates or billing), **Billing** (management: full clock records with rates, actuals vs estimate, Generate Invoice), Activity; both Timesheets and Billing share the same live clock state |
| Scheduling & Dispatch | `/dispatch` | ✅ Built — month/week/day views, drag-and-drop crew assignment, truck dropdown, unassign via X, date change modal, **dispatcher men count override with +/− controls and "Adjusted" flag** |
| Crew & Fleet Management | `/crew` | ✅ Built — Crew Members tab (add/edit/remove, availability toggle, absence log with types/dates, restriction tags); Fleet tab (add/edit/remove, inline status change with note, maintenance surfaced first) |
| Billing & Invoicing | `/billing` | ✅ Built — 4 tabs: Pending Review (**3 billing paths**: Bill Estimate / Bill Actual & Send / Edit Invoice with editable line items), All Invoices (filterable, expandable rows, Mark Paid), AR (aging buckets + by-customer), Recurring Billing |
| Claims | `/claims` | ✅ Built — coverage-aware flows (Released Value auto-calculates settlement; FVP requires manual assessment), per-item settlement math, Coverage Options tab with all 4 types + custom tier support |
| Rate Sheets & Tariffs | `/rates` | ✅ Built — local crew rates (editable inline by crew size), truck rates (per day + hourly), CZAR-LITE interstate grid (click any cell to edit), fuel surcharge with rate history and auto-apply toggle, custom contract pricing per account |
| Long Distance | `/longdistance` | ✅ Built — shipment tracker with status filter and expandable detail (billing, agents, action buttons), agent network with contact cards and ratings, interactive CZAR-LITE pricing calculator with accessorial charge reference |
| Customer Accounts | `/customers` | ✅ Built — list with tags, revenue, ratings |
| Customer Profile | `/customers/[id]` | ✅ Built — stats row, pinned note, Jobs / Storage / Invoices / Communications tabs |
| Warehouse & Storage | `/warehouse` | ✅ Built — 5 tabs: Incoming Shipments (**live scheduling form**: shipment name, customer, warehouse, vault, arrival type toggle specific/spread, receiving staff, contents, instructions; adds to Expected group instantly), Vault Directory, Delivery Orders, Capacity & Metrics, Manage Warehouses |
| Reporting | `/reporting` | ✅ Built — Explorer tab (cascading filters, live stat cards), Sales, Operations, Financial, Custom Report Builder tabs |
| Tasks | `/tasks` | ✅ Built — Open/Completed tabs, urgency grouping (Overdue/Today/Upcoming), inline edit panel (priority, assignee, due date, notes, undo complete), Auto Rules tab |
| Automation | `/automation` | ✅ Built — sequence list with status, expandable step timeline, pause/resume toggle, edit step inline, add step, new sequence form |
| Customer Portal | `/portal` | ✅ Built — no sidebar (customer-facing), active move tracker, job progress bar, document/storage/billing/support tabs |
| Integrations & API | `/integrations` | ✅ Built — Connected tab (status + reconnect), Browse All by category, Lead Sources (field mapping), API & Webhooks (key gen/revoke with scopes, webhook endpoints with event subscriptions), Activity Log |
| Admin & Settings | `/admin` | ✅ Built — Company, Theme & Branding, Users & Roles (permission matrix), Truck Types, Pipelines, Task Rules tabs |
| Recycle Bin | `/admin/recycle-bin` | ✅ Built — role-based visibility, Restore (animated), permanent delete (requires typing DELETE), linked record warnings, expiry countdown |
| BOL & Forms | `/bol` | ✅ Built — document list with type/status badges |
| BOL Viewer | `/bol/[id]` | ✅ Built — full DOT-formatted document with print/download/send |
| Role Preview Toggle | TopNav (global) | ✅ Built — dropdown in every page's TopNav; switches sidebar to show only modules the selected role can access; amber banner shows active preview role with Exit button |

**All planned prototype screens are now complete. No deferred items remaining.**

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

#### New Lead Intake
When a new lead comes in (phone call, web form, third-party source), the coordinator or salesperson creates it via the **New Lead** form. Fields collected at intake:

- **Contact Name** (required) — individual or company
- **Phone** and **Email**
- **Origin** and **Destination** city (required) — the two pieces of info needed to understand the job
- **Estimated Move Date**
- **Estimated Rooms of Furniture** — a quick room count for initial ballpark; not a dollar value at this stage (the dollar estimate comes from the Estimating tool after inventory is built)
- **Lead Source** — Website, HireAHelper, Moving.com, MovingHelp, Thumbtack, Angi, Referral, Phone Call, Other
- **Salesperson assignment** — assign immediately or leave Unassigned for coordinator to assign
- **Starting stage** — usually New Lead, but can be dropped into any stage if already contacted
- **Notes** — any initial context from the call
- **Hot Lead flag** — priority flag visible on the kanban card

#### Pipeline Stage Advancement
Each kanban card has two stage controls at the bottom:
- **Primary button** — "→ [Next Stage]" advances one step forward instantly
- **Chevron dropdown** — jump to any specific stage directly (useful for leads that progress quickly or skip stages)

When a stage changes: the task label and urgency update automatically to match the new stage's expected next action. Stage changes also persist to localStorage so the detail page reflects them and vice versa.

**Task view:** Each lead row has a "Done →" button that advances the lead to the next stage and moves it down the priority list.

#### Lead Detail Page
Clicking any lead card (in either pipeline or task view) opens the full lead file. **All fields are interactive** — changes persist immediately and reflect back on the pipeline card.

**Header controls:**
- Contact name, lead ID
- **Hot Lead toggle** — click the flame badge to toggle on/off
- **Stage dropdown** — click the stage badge to open a dropdown and jump to any stage directly; logs the change to activity
- Contact info strip (phone, email, origin → destination, move date)
- **Open Estimator** — links to the estimating tool
- **Mark Booked** button — jumps to Booked stage; becomes "View Jobs →" link once booked

**Active task banner:**
- Amber strip at the top — shows the current task for the active stage, due date, and a Complete button
- Clicking Complete: marks the task done, auto-advances to the next stage, logs "Task completed: [name]" to the activity feed
- Banner updates color/icon based on urgency (amber = today, red = overdue, green = done)
- Shows "Moving to [next stage]…" briefly during the transition

**Quick stage advance:**
- Below the task banner, a "Next stage: → [Stage Name]" shortcut for jumping forward without going through the task flow

**Tabs:**
- **Overview** — origin/destination addresses with access notes, move date + flexibility, **estimated rooms** (editable inline — click value to edit), services requested, customer notes; salesperson assignment dropdown; coordinator, source, created date
- **Attachments** — all files: estimates, BOL (once generated), signed paperwork, uploads; BOL placeholder shown until booked
- **Activity** — full chronological log; note input field (post with Enter or button); all stage changes, task completions, and salesperson changes auto-logged with timestamp

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
#### Generate Quote — Direct Estimator Output
- **Generate Quote button** in the estimator header — enabled as soon as any inventory is added
- One click saves the full estimate breakdown (labor, supervisor, truck allocation, fuel surcharge %) and navigates to the Quotes module
- The Quotes module receives the data and automatically creates a Draft quote pre-filled with all line items — no re-entry required
- The draft is opened and expanded for immediate review; salesperson adjusts notes, expiry date, and any custom add-ons, then sends
- This is the primary path from estimate → quote → job booking

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
Formal quote documents sent to customers after the estimate is built. The Estimator feeds directly into the Quotes module — one click creates a draft quote pre-filled with all line items.

#### Quote Lifecycle
```
Draft → Sent → Viewed → Accepted → Job Created
                      ↘ Declined
                      ↘ Expired (auto after expiry date)
```
- Each status is tracked with timestamps (sent date, viewed date, response date)
- Expired quotes can be duplicated and resent with a new expiry date
- Accepted quotes link to the created job file

#### Estimator → Quote Tie-In
- **Generate Quote button** on the Estimator — active once any inventory is added (disabled when empty)
- Clicking it saves the full estimate breakdown (labor, supervisor, truck, fuel surcharge) to a handoff payload and navigates to `/quotes`
- The Quotes page detects the pending estimate on load, creates a pre-filled Draft quote, and expands it for immediate review
- The quote line items match the estimator output exactly: crew labor, supervisor, truck type(s), fuel surcharge applied as a percentage line
- Salesperson reviews the draft, adjusts notes, and sends — no re-entry of figures needed

#### Quote Line Items
- Labor (crew size × hours × rate)
- Supervisor (hours × supervisor rate)
- Truck(s) (per day or hourly per type)
- Fuel surcharge (% applied to labor + truck subtotal)
- Custom lines (add-ons, packing services, valuation premiums, etc.)
- Live total updates as lines are edited

#### Quote Actions
- **Send** — marks as Sent, logs timestamp, customer receives quote via email
- **Resend** — re-sends with updated timestamp for viewed tracking
- **Mark Accepted** — marks quote Accepted, triggers Convert to Job action
- **Convert to Job** — creates job file from the accepted quote
- **Duplicate** — creates a new Draft copy (useful for expiring/declined quotes or similar jobs)
- **Edit** — edit any line item, notes, or expiry date while in Draft
- **Delete** — soft delete (undo toast → Recycle Bin)

#### Templates
- Pre-configured quote structures for common job types (Standard Local Move, Large Home, Long Distance Standard, Commercial Office Move, Corporate Relocation)
- Each template pre-fills the line items; salesperson adjusts quantities and rates for the specific job
- Templates are admin-configurable — add, edit, remove
- Usage count tracked per template to surface the most-used ones

#### Other Features
- Quote expiration dates — configurable default (e.g., 14 days from sent date); admin-editable per quote
- Optional add-ons and upsells built into quote (packing services, storage, valuation coverage)
- Customer e-signature on quote acceptance
- Quote PDF generation with company branding
- Quote viewed tracking — system logs when the customer opens the quote link
- Automatic job creation on acceptance
- Pipeline value tracking — total value of Sent + Viewed quotes as a pipeline metric

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

#### Job Detail — Tabs
The job detail page is organized into six tabs, each serving a distinct audience:

| Tab | Audience | What it shows |
|-----|----------|---------------|
| **Overview** | All roles | Customer, addresses, crew/truck assignment, services, special instructions |
| **Inventory** | All roles | Room-by-room item list with quantities |
| **Documents** | All roles | BOL, estimate, order for service — view and download |
| **Timesheets** | Crew + Management | Clock-in/out interface — crew-facing, **no pay rates or billing totals** |
| **Billing** | Management only | Full clock records with rates, actuals vs. estimate, Generate Invoice |
| **Activity** | All roles | Full chronological log of all events on the job |

#### Timesheets Tab — Crew-Facing Clock System
The Timesheets tab is purpose-built for crew members in the field. It shows everything they need to clock their time and nothing they should not see.

**What it shows (crew access):**
- Job context strip: job ID, customer, date/time window, origin → destination, truck — confirm you're on the right job
- One card per assigned crew member: name, role (Lead/Helper/Driver), Lead tag where applicable
- Clock In time column, Clock Out time column, Elapsed/Total Hours column
- **Large Clock In button (green)** — easy to tap on a phone or tablet
- Live elapsed timer while clocked in (hours : minutes : seconds)
- **Clock Out button (red)** when active — freezes the record on click
- Hours shown when done (no rate, no dollar amount anywhere on this tab)
- Summary footer: crew count, total hours across all members, View Timesheet button

**What it intentionally omits:**
- Pay rates per crew member
- Labor cost calculations
- Actuals vs. estimate comparison
- Invoice generation
- Billing totals of any kind

**Permission design:** In production, the Crew/Driver role would only have access to this tab — the Billing tab is Hidden from their permission matrix. This is set in Admin → Users & Roles.

#### Billing Tab — Management Actuals View
The Billing tab reads from the exact same clock records as the Timesheets tab — one shared state, two different lenses.

**Additional data the Billing view adds:**
- Pay rate per crew member (pulled from crew master data by name — not manually entered)
- Labor cost per person (hours × their specific rate)
- Running labor subtotal updating live while anyone is active
- Overrun flag (amber) when a crew member clocks more than the estimated hours + 15-min buffer
- Actuals vs. Estimate comparison table (Labor / Truck / Materials with Estimated, Actual, Variance columns)
- Generate Invoice button (locked until all crew clocked out)
- Printable timesheet document with full detail including rates and subtotals

**Rate source:** Each crew member's rate is looked up by name from the crew master data (same rates shown in Crew & Fleet Management). If a rate changes in crew management, it flows through here automatically — no rate tables to maintain separately on the job record.

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
The pricing engine. Drives estimates, billing, and settlement. All rates are admin-editable defaults — changes apply immediately to new estimates. Existing saved estimates are not affected.

#### Local Rates Tab
- **Crew hourly rates by crew size** — 2-person, 3-person, 4-person, 5-person, 6-person; each rate editable inline (click pencil → type → Enter to save)
- **Minimum hours** — configurable floor; affects minimum charge calculation
- **Minimum charge** — derived from minimum hours × base rate; displayed on rate sheet
- **Truck rates** — per day rate and hourly rate per truck type (Cargo Van, Sprinter Van, 16ft, 26ft, 53ft); each editable inline
- Changes here sync with the Estimating module's default rates

#### Interstate / Long Distance Tab
- **CZAR-LITE style weight × distance grid** — 7 weight bands (Under 2,000 lbs through 16,001+ lbs) × 5 distance bands (< 500 mi through 2,001+ mi)
- Each cell shows a rate per 100 lbs (per cwt); click any cell to edit inline
- Rates feed the Long Distance Pricing Calculator
- **Additional LD accessorial charges** table (Long Carry, Elevator, Piano/Organ, Shuttle Service, Packing, SIT, etc.) — reference display, editable in Admin

#### Fuel Surcharge Tab
- Current fuel surcharge percentage — prominently displayed
- **Update Rate** button — inline edit with Save/Cancel
- **Auto-apply toggle** — when on, surcharge is automatically added to all invoices; when off, must be applied manually per invoice
- **Rate history log** — every rate change recorded with date, new rate, and delta (+/−) vs. prior rate; color-coded trend indicator

#### Custom Contracts Tab
- Per-account pricing that overrides standard rates (e.g., flat hourly for a corporate client, custom sq ft rate for a commercial storage account)
- Each contract shows: account name, contract type, rate, notes, expiry date
- Add / Edit / Remove contracts
- Contract rates are linked to the customer's account — automatically applied when invoicing that customer

#### Future
- 400NG tariff integration (van line interstate)
- GSA-500A government/military tariff
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
Full vault and item-level storage tracking across one or multiple warehouse locations.

#### Multi-Warehouse Management
- **Multiple warehouse locations** — each with its own name, address, capacity, rows/sections/bays layout
- Add, edit, or retire warehouse locations from Admin
- Each vault is assigned to a specific warehouse location
- Dispatch and customer views show which warehouse a customer's items are in
- Reporting can be filtered or grouped by warehouse location
- Companies with one warehouse see the same UI — the warehouse selector simply has one option

#### Vault & Storage
- Vault inventory — vault number, size, contents, customer
- Item-level storage (loose storage, rack storage)
- Vault location tracking (row, section, bay) within each warehouse
- Full and empty vault tracking per warehouse
- Check-in / check-out workflow
- Long-term storage vs. storage-in-transit (SIT) tracking
- SIT billing (daily/monthly rate)
- Delivery order management (pull from storage for delivery)
- Storage account history retained indefinitely
- Inventory audit tools
- **Exceeds CompuMove:** Barcode/QR scanning for vaults and items, warehouse map visual

#### Storage Tracking Metrics — Customizable Per Warehouse
Different storage types require different tracking units. Each warehouse can be configured to track any combination of the following:

**Tracking Unit Types (admin-configurable per warehouse):**
- **Vaults** — numbered vault units of defined sizes (10×10, 5×10, 10×20, etc.). Standard for household goods. Tracks: vault count, capacity in cu ft, occupied vs empty vs reserved.
- **Square Footage** — raw floor space in sq ft. Common for commercial projects, overflow storage, and large-item staging. Tracks: total sq ft, allocated sq ft, available sq ft.
- **Spaces / Bays** — numbered bays or parking spaces in the warehouse. Used for oversized items, vehicles, equipment. Tracks: total spaces, occupied spaces, available.
- **Pallet Positions** — for warehouses that also do commercial/logistics storage. Tracks pallet in/out.
- **Custom metric** — admin can define any named unit with a capacity number (e.g., "Container Slots," "Rack Sections")

Multiple metrics can be active simultaneously in the same warehouse (e.g., a warehouse that has both vaults and open floor space tracks both).

#### Built Vault Inventory & Capacity Planning
Key operational insight: how many physical vaults exist (built but possibly empty), and are more needed?

**Current Vault Inventory Status:**
- **Built & Occupied** — vault exists, customer items inside, billing active
- **Built & Empty** — vault exists physically but has no current occupant (revenue opportunity)
- **Built & Reserved** — vault exists, no items yet, but reserved for an upcoming job
- **Under Construction** — vault being built, not yet available
- **Retired / Removed** — vault removed from floor plan

Admin can see at a glance: how many physical vaults the warehouse has, how many are generating revenue, how many are sitting empty.

**Capacity Projection (Demand Forecasting):**
The system projects how many vaults will be needed over upcoming periods based on:
- Confirmed upcoming storage-in jobs (already booked)
- Historical storage intake rate (how many new storage accounts opened per month, trailing 6–12 months)
- Current storage account churn rate (how many close per month)
- Seasonal adjustment (configurable — e.g., summer months historically have 20% higher intake)

**Projection output (per warehouse, per period):**
- Current occupied: X vaults
- Reserved (incoming booked): +Y vaults
- Projected new demand (next 30/60/90 days): +Z vaults (based on historical rate)
- Projected churn (storage accounts likely to close): −W vaults
- **Net projected need at end of period:** X + Y + Z − W
- Compared against total built vault count → shows surplus or shortage
- If projected need approaches or exceeds capacity: alert generated for warehouse manager

**Threshold alerts (admin-configurable):**
- "Warn when projected occupancy exceeds 80% within 60 days"
- "Alert when empty vaults drop below 3"
- These alerts generate tasks for the warehouse manager

**Exceeds CompuMove:** Multi-metric storage tracking, built vault inventory status, demand forecasting with configurable projection windows and thresholds.

#### Incoming Shipments — 3rd Party Receiving
Track all expected inbound deliveries before they arrive. This covers shipments coming from customers, carriers, van lines, or any 3rd party — not just MovePro crew moves.

**Scheduling a New Incoming Shipment:**
The "Schedule Incoming" button on the Incoming Shipments tab opens an inline form (no separate page). Fields:
- **Shipment name / reference** (required) — e.g., "Johnson Estate — POD from Allied Van Lines"
- **Customer name** (required) and **file reference**
- **Shipper / carrier** — who is delivering (van line, FedEx Freight, customer self-drop, etc.)
- **Warehouse location** — dropdown of active warehouse locations
- **Target vault / staging area**
- **Arrival type toggle:**
  - *Specific Date + Time* — exact date picker + time window field (e.g., "10:00 AM – 12:00 PM")
  - *Date Window / Spread* — earliest and latest date pickers for when the exact day isn't confirmed
- **Receiving staff** — who is responsible for processing it on arrival
- **Contents description** — brief summary of what's expected
- **Special instructions** — fragile, oversized, liftgate required, temperature-sensitive, etc.

On submit: the shipment appears immediately at the top of the Expected group, fully expandable with the standard receiving workflow (Mark Arrived → Process Receiving → Generate Receiving Report).

**Scheduled Incoming Shipments:**
- Each incoming shipment has:
  - **Shipment name / reference** (e.g., "Johnson Estate — POD from Allied Van Lines")
  - **Shipper / origin** (3rd party company or individual)
  - **Expected arrival:** specific date+time, OR a spread of dates (e.g., "arriving between Jun 12–15")
  - **Target vault / staging area**
  - **Warehouse location** (if multi-warehouse)
  - **Contents description** — brief summary of what's expected
  - **Special instructions** — fragile, oversized, requires liftgate, temperature-sensitive, etc.
  - **Associated customer / file reference** (links to the customer it's being stored for)
  - **Assigned receiving staff** — who is responsible for processing it when it arrives

**Arrival Status:**
- Expected → Arrived → Received & Processed → Discrepancy Flagged
- When marked "Arrived," the receiving workflow is triggered automatically

#### Receiving Workflow
When a shipment arrives (whether a scheduled incoming or an unscheduled drop-off):

1. Receiving staff opens the incoming shipment record (or creates one on the spot for unscheduled)
2. **Condition check at receiving:**
   - Photo capture of items/boxes at arrival (required for liability)
   - Condition noted per item or per box: Good / Minor Damage / Significant Damage / Missing
   - Any discrepancies between expected and actual contents flagged immediately
3. **Receiving Report generated** — document containing:
   - Shipper, arrival date/time, receiving staff name
   - Items received vs. expected (quantity, condition)
   - Photos
   - Any discrepancies or notes
   - Signature field (driver/delivery person sign at receiving)
4. Report stored on the customer's file and linked to the vault record
5. **Automated alerts** sent on receiving completion (configurable per company — see below)

#### Receiving Alerts — Customizable
Admin configures who gets notified when specific receiving events happen:

| Event | Configurable Alert Recipients |
|-------|-------------------------------|
| Shipment arrives as scheduled | Assigned coordinator, customer (optional) |
| Receiving report completed | Assigned coordinator, billing team |
| Discrepancy found at receiving | Coordinator + manager, claims team |
| Items received with damage | Coordinator + manager, claims team immediately |
| Unscheduled shipment received | Warehouse manager + coordinator |
| Shipment overdue (past expected date) | Assigned coordinator + manager |

- Alert channels: in-app task, email, SMS (configurable per alert type)
- Customer notification on arrival is optional — toggle per customer or per shipment
- Alert rules are managed in Admin & Settings → Automation

---

### MODULE 10A — Claims Management
Handles all damage and loss claims from initial filing through settlement. The claims flow is determined by the valuation coverage the customer selected at booking — this must be clearly recorded on the BOL and job record so the correct process is followed.

#### Valuation Coverage Types
Valuation coverage defines the carrier's liability and drives the entire claims process. Each company can configure their own coverage options in Admin — the following are the defaults shipped with the system.

**Default Coverage Options (all configurable by Admin):**

| Coverage Type | Default Rate | Carrier Liability | Customer Cost |
|--------------|-------------|------------------|--------------|
| **Released Value — Basic** | $0.10/lb per article | Carrier pays max $0.10 × item weight | Free |
| **Released Value — Standard** | $0.60/lb per article (FMCSA minimum) | Carrier pays max $0.60 × item weight | Free |
| **Full Value Protection** | Declared shipment value | Carrier responsible for repair, replacement at current market value, or cash settlement | Premium charged (configurable, e.g., $0.60 per $100 of declared value) |
| **Third-Party / Customer's Own Insurance** | N/A — handled by customer's insurer | Carrier liability is released; customer's insurer handles claim | Customer arranges separately |

- The customer selects their coverage option at time of estimate/booking
- Their selection is locked to the job and printed clearly on every BOL and estimate
- If no selection is made, the system defaults to Released Value — Standard (FMCSA minimum)
- A different default can be configured by Admin (some companies default to Full Value Protection)

**Admin Customization of Coverage Options:**
- Add custom coverage tiers (e.g., a company's proprietary enhanced coverage at a custom rate)
- Edit the per-lb rate, premium pricing, and liability description for each tier
- Mark any tier as inactive to remove it from customer selection
- Set the company default (what customers get if they don't actively choose)
- Coverage option names and descriptions are editable to match the company's language

#### Claim Intake
- Claims can be filed by: customer (via portal), salesperson on behalf of customer, or claims department directly
- Required at intake: job ID, customer, date of move, description of damage/loss, items affected, coverage type on file
- System automatically pulls the coverage type from the job record — cannot be changed after the fact
- Photos can be attached at intake (required for full value protection claims)
- Crew exception reports from field (filed during move) are automatically linked to the job and flagged for claims review

#### Claims Flow by Coverage Type

**Released Value Flow ($0.10/lb or $0.60/lb):**
1. Claim filed — damage/loss described and items listed
2. Claims team verifies item was listed on inventory/BOL
3. Claims team records weight of damaged/lost item(s) (from inventory or estimate)
4. Settlement calculated automatically: weight × coverage rate (e.g., 15 lbs × $0.60 = $9.00)
5. Settlement offer sent to customer
6. Customer accepts or disputes
7. If accepted: settlement issued (check, credit, or deduction from balance)
8. If disputed: escalate to manager review

**Full Value Protection Flow:**
1. Claim filed — damage/loss described with photos
2. Claims team verifies declared shipment value on BOL
3. Claims team assesses: repair cost vs. replacement value vs. cash settlement
4. May require: third-party appraiser, repair estimate, replacement cost research
5. Settlement offer: whichever is lowest of (repair cost / replacement at depreciated value / declared value proportion)
6. Customer accepts or disputes
7. If accepted: settlement issued
8. If disputed: formal dispute process, may involve mediator

**Third-Party Insurance:**
1. Claim filed — system records it but routes customer to their own insurer
2. Company provides BOL, inventory list, and any documentation requested
3. No carrier settlement — claim handled externally
4. Status tracked in system for record-keeping

#### Claims Record — What It Contains
- Claim ID, linked job ID, file reference, customer
- Coverage type (pulled from job — immutable after job date)
- Date of move, date claim filed, days since move
- Claim status: Filed → Under Review → Settlement Offered → Accepted / Disputed → Closed
- Claimant contact info
- Damaged/lost items: item name, weight, estimated value, photos
- Calculated settlement amount (auto-calculated for released value; manual entry for full value)
- Notes and communication log (internal + customer-facing)
- Documents: original BOL, inventory list, photos, appraisals, settlement letter
- Assigned to: which claims team member is handling it
- Resolution: settlement amount paid, date closed, method (check/credit/deduction)

#### Claims Dashboard
- Open claims queue — sorted by status and filing date
- Overdue alerts (claims not responded to within X days — configurable SLA)
- Claim volume by coverage type
- Average settlement amount by coverage type
- Claims rate (claims per 100 jobs) — tracked for quality control
- Total claims liability outstanding

#### Claims Team Role
- **Claims** role in RBAC: access to all jobs (read-only), full claims module access, can request BOL and inventory from any job, cannot edit job records directly
- Claims manager can override settlement amounts and close disputes
- All settlement decisions logged with who approved and when

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
Dedicated module for interstate and long-haul shipments. Covers the full lifecycle from booking through delivery, with agent coordination and weight-based pricing tools.

#### Shipments Tab
- All LD shipments listed with: customer, file reference, origin → destination, weight, status, estimated delivery, total charge
- **Status filter** — filter by any status stage (Booking Confirmed, Pickup Scheduled, Loaded, In Transit, At Destination Warehouse, Out for Delivery, Delivered, On Hold)
- **Status icons** — truck for In Transit, checkmark for Delivered, alert for On Hold, clock for all pending stages
- **Expandable detail** per shipment:
  - Left panel: pickup date, first/last available, estimated delivery, weight, estimated cu ft, driver, truck
  - Right panel: base rate, fuel surcharge, total charge (itemized); origin and destination agents; notes
  - Action buttons: Update Status, View File, Contact Agent, View BOL
- **KPI cards** at top: Active Shipments, In Transit Now, Total Weight (lbs), Revenue (all shipments)

#### Shipment Status Lifecycle
```
Booking Confirmed → Pickup Scheduled → Loaded → In Transit
→ At Destination Warehouse → Out for Delivery → Delivered
(or → On Hold at any stage)
```

#### Agent Network Tab
- Directory of all origin, destination, and transit agents
- Per agent: company name, primary contact, phone, email, city/state, type (Origin / Destination / Both), active shipment count, star rating
- Contact and Edit actions per agent
- Add Agent button

#### Pricing Calculator Tab
- Interactive weight + distance → cost calculator
- Inputs: shipment weight (lbs), distance (miles), fuel surcharge (%)
- Looks up the correct CZAR-LITE rate band from Rate Sheets module
- Output: base rate, fuel surcharge amount, total estimate; with rate band and per-cwt rate displayed
- **Standard Accessorial Charges** reference table alongside the calculator (Long Carry, Elevator, Piano, Shuttle, SIT, Full Value Protection, etc.)

#### Future
- Weight ticket management (origin and destination weighmaster tickets)
- Actual weight billing vs. estimated weight
- Driver settlement / carrier pay (LD driver commission per mile)
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
Connects MovePro to external tools. Organized into five areas: connected integrations, integration directory, lead source management, API key + webhook management, and activity logging.

#### Connected Tab
- All currently connected integrations displayed with status badges (Connected / Error / Not Connected)
- Expandable per integration: last sync time, connected since date, Sync Now, Configure, and Disconnect actions
- **Error state**: amber banner with error message and Reconnect button (e.g., OAuth token expired)
- **Header stat cards**: Connected count, Needs Attention count, Active API Keys, Active Webhooks

#### Browse All Tab
- Full integration catalog organized by category:
  - **Accounting**: QuickBooks Online, QuickBooks Desktop
  - **Communication**: Twilio, SendGrid, Mailgun
  - **Maps & Routing**: Google Maps
  - **Calendar**: Google Calendar
  - **Payment**: Stripe, Square
  - **Van Lines**: Allied Van Lines, Mayflower, UniGroup
  - **Automation**: Zapier, Make (Integromat)
- Connect / Reconnect / Disconnect actions per integration

#### Lead Sources Tab
- Dedicated management for lead source integrations (separate from native integrations because they require field mapping)
- **Active sources**: HireAHelper, MovingHelp — show today's lead count, monthly lead count, last sync time
- **Available sources**: Moving.com, Thumbtack, Angi — enable + configure
- Per source: Enable/Disable toggle, API key management, **field mapping** (source field → MovePro field, e.g., `customer_name` → Contact Name, `move_date` → Move Date)
- Leads from connected sources are automatically imported into CRM & Leads with mapping applied
- Add Source button for custom lead sources

#### API & Webhooks Tab
**API Keys:**
- Generate new API keys with a name and scope selection (jobs:read, jobs:write, customers:read, invoices:read, portal:read, portal:write, etc.)
- View / hide key (eye toggle), copy to clipboard, revoke
- Each key shows: created date, last used, active scopes
- Revoked keys remain in list with visual distinction

**Webhook Endpoints:**
- Add endpoints with URL + event subscriptions
- **Supported events**: job.created, job.updated, job.completed, job.cancelled, lead.created, lead.booked, invoice.sent, invoice.paid, customer.created, crew.assigned, estimate.sent, etc.
- Per endpoint: status (Active / Failing / Paused), success rate %, last triggered
- Expand: Send Test, View Logs, Pause/Resume
- Delete endpoint

**API Reference panel**: base URL, links to Docs, Changelog, Postman Collection, OpenAPI Spec

#### Activity Log Tab
- Live feed of all integration events: integration name, event type, status (success/error/info), timestamp, detail line
- Covers: invoice syncs, SMS deliveries, lead imports, payment webhooks, distance calculations, OAuth failures

#### Error Handling
- Any integration in error state surfaces in both the Connected tab and a banner at the top of the page
- Error message explains the cause (e.g., "OAuth token expired — reconnect required")
- One-click Reconnect re-initiates the OAuth flow or API handshake

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
- Data import tools (migrate from CompuMove or spreadsheets) — see full section below
- Backup and export — see full section below

#### Data Import, Export & Migration

**Philosophy:** A client should never feel locked in. Easy import lowers the barrier to switching to MovePro. Easy export builds trust that their data is always theirs. Both are sales advantages.

---

**Import — Onboarding a New Client's Historical Data**

When a moving company switches to MovePro, they bring years of existing data. The import system lets them bring that data in rather than starting from zero. This is part of white-glove onboarding.

**What can be imported:**

| Data Type | Format | Notes |
|-----------|--------|-------|
| Customers / contacts | CSV | Name, phone, email, address, account type |
| Job history | CSV | Past jobs with dates, origin, destination, type, status, value |
| Crew members | CSV | Name, role, team, phone, pay rate |
| Vehicles / fleet | CSV | Unit, type, make, year, license plate |
| Storage accounts / vaults | CSV | Vault info, customer link, rate, start date |
| Rate sheets | CSV or manual entry | Local rates, truck rates |
| Outstanding invoices / AR | CSV | Open invoices being carried over |

**Import flow (admin-only):**
1. Platform owner or client's Admin uploads a CSV in the import tool
2. System shows a column mapping screen — drag to match their column headers to MovePro fields
3. Preview of first 10 rows before confirming
4. Import runs; errors are flagged row-by-row (duplicate detected, missing required field, etc.)
5. Import log saved showing what was created, what was skipped, and why

**CompuMove migration:**
CompuMove is the primary system MovePro clients are migrating from. CompuMove allows data export in various formats. The import tool will include a "CompuMove import" preset that pre-maps the known CompuMove export columns to MovePro fields automatically — reducing manual mapping for the most common migration path.

**Other systems:**
Generic CSV import handles data from any system (spreadsheets, MoveitPro, SmartMoving, etc.) via the manual column mapping screen.

---

**Export — Data Portability**

Clients can export their own data at any time without needing to contact support. This is a trust feature — clients know they're never trapped.

**What can be exported:**

| Data Type | Format |
|-----------|--------|
| All customers | CSV |
| All jobs (full history) | CSV |
| All invoices | CSV + PDF (individual) |
| All crew timesheets | CSV |
| All BOLs and documents | ZIP of PDFs |
| Full account data export | CSV bundle (all tables) |

**Export access:**
- Company Admins can export all data for their company at any time
- Individual module exports available from within each module (e.g., export from the Reporting page)
- Full account data export available in Admin & Settings → Data
- Platform owner can trigger exports on behalf of a company (for offboarding)

---

**Offboarding / Account Closure**

When a client ends their contract:
1. Platform owner triggers a full data export (CSV bundle + PDF documents as ZIP)
2. Export is delivered to the client's Admin via email download link (Supabase Storage, time-limited URL)
3. Account is set to `suspended` — data is retained for 90 days before permanent deletion
4. Client is notified of the 90-day retention window
5. Client can request permanent deletion before 90 days if required for compliance

Financial records (invoices, payments) are retained for 7 years minimum regardless of account status, consistent with standard business record-keeping requirements.

#### Deleted Records & Data Recovery System
The moving industry is highly dependent on records. An accidental deletion can cause operational, legal, and billing problems. Nothing in this platform is permanently deleted without a deliberate multi-step admin process. The goal: make recovery easy, make permanent deletion hard.

**Inline Undo Toast — First Line of Defense:**
Before anything reaches the Recycle Bin, the user gets an immediate "Undo" opportunity right where they are.

1. User clicks any Delete/Remove/Disconnect/Revoke button anywhere in the app
2. The item disappears from the UI immediately (fast, feels responsive)
3. A **toast notification** appears at the bottom of the screen: *"[Item name] deleted. Undo"* with a 5-second countdown bar
4. If the user clicks **Undo** → item reappears instantly, no Recycle Bin involved
5. If the toast expires (5 seconds) → item moves silently to the Recycle Bin (for soft-delete actions) or the action is finalized (for non-delete actions like disconnect/revoke)
6. For soft-delete actions: the toast also shows a "View in Recycle Bin" link; for non-delete actions (integrations disconnect, API key revoke, webhook delete): the "View bin" link is omitted since these don't go to the Recycle Bin

**Scope — undo toast applies to all destructive actions, not just deletes:**
- Deleting records (crew members, vehicles, leads, quotes, contracts, etc.) → Recycle Bin path
- **Disconnecting an integration** → immediate undo restores the connection with full state (status, last sync, connected-since date)
- **Revoking an API key** → immediate undo restores the key to active
- **Deleting a webhook endpoint** → immediate undo re-adds the endpoint
- Pipeline stage removals, automation sequence steps, invoice line items, document attachments, and more

The key principle: **no destructive action in the app should be irreversible within 5 seconds.** The undo toast is the safety net before more formal recovery mechanisms (Recycle Bin, version history) are needed.

**Soft Delete — Everything Goes to the Recycle Bin After Undo Expires:**
- After the 5-second undo window closes, any deleted record (job, lead, invoice, customer, BOL, crew member, vehicle, document, etc.) moves to the **Recycle Bin**, not permanent deletion
- The Recycle Bin is accessible by Admin and Managers from Admin & Settings
- Deleted records remain fully intact — all linked data, history, and documents are preserved
- Records in the Recycle Bin are not visible in normal app views but are still queryable

**Recycle Bin — Role-Based Visibility:**
The Recycle Bin respects the same permission and data-scope rules as the rest of the platform. What you can see in the Recycle Bin mirrors what you could see before it was deleted.

| Role | What they see in the Recycle Bin |
|------|----------------------------------|
| **Admin** | All deleted records across all roles, all business lines, all users |
| **Owner / Manager** | All deleted records across both business lines; cannot permanently delete |
| **HHG Coordinator** | Records deleted by them or deleted within HHG scope they have access to |
| **Commercial Coordinator** | Records deleted by them or within Commercial scope |
| **Salesperson / Estimator** | Only records they personally deleted (their own leads, their own estimates) |
| **Dispatcher** | Records they deleted within dispatch scope (jobs, crew assignments) |
| **Billing** | Records they deleted within billing scope (invoices, payment records) |
| **Warehouse** | Records they deleted within warehouse scope (vault records, storage accounts) |
| **Crew / Driver** | No access to the Recycle Bin |

- Restore permission mirrors delete permission — if you could delete it, you can restore it
- Permanent delete is Admin only regardless of who deleted the record
- Admin can see the full history including what any user deleted and when

**Recycle Bin Features:**
- Filterable by record type (Jobs, Leads, Invoices, Customers, Documents, Crew, Vehicles, etc.)
- Searchable by name, ID, customer, date deleted
- Shows: record name/ID, record type, deleted by (user), deleted on (date/time), reason (if provided)
- **Restore** button — one click restores the record exactly as it was, including all linked data, back to its original location in the app
- Restored records show a "Restored from trash on [date]" note in their activity log
- **Permanent Delete** — available to Admin only, requires typing "DELETE" to confirm, and shows a warning listing all linked records that will also be permanently removed

**Retention Policy:**
- Soft-deleted records are retained in the Recycle Bin for **90 days** by default (configurable by Admin: 30/60/90/365 days or indefinite)
- After the retention window, records are flagged for permanent deletion and Admin receives an alert before it happens
- Financial records (invoices, payments, commission records) follow a longer retention — minimum 7 years regardless of deletion, consistent with business record-keeping requirements

**Audit Trail — Separate from Recycle Bin:**
- Every edit, status change, field update, and deletion is logged in the Audit Log with: who, what changed, from what value, to what value, timestamp
- Audit Log is immutable — it cannot be edited or deleted even by Admin
- Accessible in Admin & Settings → Audit Log
- Filterable by user, record type, action type, date range
- This provides a full history of every change ever made to any record, even if the record itself is deleted

**Version History on Key Records:**
- Job records, BOLs, estimates, and invoices keep a version history — every saved edit creates a snapshot
- Users can view previous versions and restore any field to a prior value
- Particularly important for BOLs and invoices where the final sent version must be preserved exactly

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

---

## Architecture at a Glance

*This section is written for a senior developer reviewing the project for the first time. It covers the full stack, why each piece was chosen, and how the layers connect. No deep dives — just enough to confirm the architecture makes sense before implementation begins.*

### The Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| **Frontend** | Next.js 15 (App Router), TypeScript, Tailwind CSS v4, shadcn/ui | Full-stack React framework — handles both the UI and the API layer in one codebase and one deployment. App Router enables React Server Components for fast initial loads. TypeScript enforces type safety across a complex domain model. |
| **Backend** | Next.js API Routes + Server Actions | Co-located with the frontend, no separate backend service to manage. Server Actions handle form mutations directly. API Routes handle integrations, webhooks, and anything needing explicit HTTP endpoints. |
| **Database** | PostgreSQL via Supabase | Managed Postgres — battle-tested relational DB for complex relational data (jobs → files → invoices → payments → crew). Supabase adds auth, storage, and realtime on top without adding infrastructure complexity. |
| **Auth** | Supabase Auth | JWT-based auth with custom claims (company_id, role_id injected at sign-in). Sessions managed server-side. One auth system handles both internal users and customer portal users (different claim scopes). |
| **File Storage** | Supabase Storage | Same platform as the DB — no separate S3 bucket to manage. Company-scoped buckets with RLS-matched access policies. CDN delivery for documents and generated PDFs. |
| **PDF Generation** | @react-pdf/renderer (react-pdf) | Server-side PDF generation in a Next.js API route using the same React component model as the UI. Generated PDFs are uploaded to Supabase Storage immediately; clients always download from the stored URL. |
| **Background Jobs** | Vercel Cron + Supabase pg_cron | Two types of background work require two tools — see breakdown below. |
| **Realtime** | Supabase Realtime | WebSocket subscriptions for live dispatch board updates (crew clocked in, job status changes). Supabase Realtime publishes Postgres change events directly to subscribed clients — no separate pub/sub infrastructure. |
| **Email** | SendGrid | Transactional and marketing email. Failover to Mailgun if needed. |
| **SMS** | Twilio | Automation sequences and job alerts. |
| **Hosting** | Vercel | Zero-config Next.js deployment, edge network, built-in cron job scheduling. |
| **Payments** | Stripe | Online invoice payment via the customer portal. ACH and card. |

---

### How the Layers Connect

```
Browser / Mobile
      ↓
Next.js App (Vercel)
  ├── React Server Components  → fetch data server-side, render HTML
  ├── Server Actions           → form mutations, no extra API round-trip
  └── API Routes               → webhooks, integrations, PDF generation

Supabase
  ├── PostgreSQL               → primary data store
  │     └── Row Level Security → company isolation enforced at DB layer
  ├── Auth                     → JWT issuance, session management
  ├── Storage                  → files, PDFs, photos
  └── Realtime                 → change subscriptions (dispatch board)

Background Layer
  ├── Vercel Cron              → time-based scheduled jobs
  └── Supabase pg_cron         → DB-native recurring jobs
```

---

### Background Jobs — Which Tool Does What and Why

Two tools handle background work because they solve different problems:

**Vercel Cron** — runs a Next.js serverless function on a schedule. Used when the job needs to call external services (Twilio, SendGrid, Stripe, QuickBooks) or run complex application logic.

| Job | Schedule | Notes |
|-----|----------|-------|
| Automation sequence processor | Every 15 min | Checks pending sends, delivers via Twilio/SendGrid |
| Invoice overdue checker | Daily 8am | Marks invoices overdue, creates billing tasks |
| Lead follow-up reminder | Daily 8am | Checks lead inactivity, creates sales tasks |
| Integration syncs | Per integration | HireAHelper every 5 min, QuickBooks every 4 hrs |
| Webhook delivery | Event-triggered | Posts to customer webhook endpoints on data events |

**Supabase pg_cron** — runs SQL directly inside Postgres. Used when the job is purely data manipulation with no external calls — faster and simpler than a round-trip through the API layer.

| Job | Schedule | Notes |
|-----|----------|-------|
| Recurring invoice generation | 1st of month | INSERT invoice rows for active storage accounts |
| Recycle bin cleanup | Daily midnight | DELETE records past expires_at, pre-alert admin |
| Capacity projection | Daily 6am | Recalculate 30/60/90-day vault demand metrics |

---

### Multi-Tenancy Pattern

Single database, strict isolation via `company_id` on every table + Supabase Row Level Security.

```sql
-- Example RLS policy (applied to every table)
CREATE POLICY "company_isolation" ON leads
  FOR ALL USING (company_id = (auth.jwt() ->> 'company_id')::uuid);
```

This means: even if there is a bug in the application layer, the database will not return another company's rows. Company isolation is enforced at the storage engine level, not the application level.

---

### RBAC Pattern

Two-layer enforcement:

1. **Company isolation** — RLS (database level, strict)
2. **Internal permissions** — Next.js middleware (application level, practical)

```
Request arrives at API route
  → Supabase verifies JWT (valid session?)
  → Middleware checks company_id claim (right company?)
  → Middleware checks role permissions (allowed module + action?)
  → Handler runs query (RLS double-checks company scope)
  → Response
```

Internal roles (who can see Billing vs. who can see Dispatch) are stored as a JSONB permissions object in the `roles` table and checked in middleware. This is intentionally pragmatic — employees are trusted, so server-side middleware checks are sufficient for V1. RLS is reserved for the security boundary that actually matters: cross-company isolation.

---

### Key Architectural Decisions — Summary for Reviewer

| Decision | Choice | Alternatives considered |
|----------|--------|------------------------|
| Framework | Next.js (full-stack) | Separate React frontend + Node/Express API |
| Database | Supabase (managed Postgres) | PlanetScale, Neon, self-hosted Postgres |
| Multi-tenancy | Shared DB + company_id + RLS | Separate DB per tenant, schema-per-tenant |
| Auth | Supabase Auth | NextAuth, Clerk, Auth0 |
| File storage | Supabase Storage | AWS S3 + CloudFront |
| PDF | react-pdf (server-side) | Puppeteer headless Chrome, PDFKit |
| Background jobs | Vercel Cron + pg_cron | Inngest, BullMQ, Railway cron |
| Realtime | Supabase Realtime | Pusher, Ably, self-hosted WebSocket server |

*The overriding principle: minimize the number of services. Supabase consolidates DB + auth + storage + realtime into one platform and one billing relationship. This reduces operational complexity significantly for a small team.*

---

## Technical Architecture Decisions

This section answers the "how" questions that must be decided before backend development begins. These decisions are made; they do not need to be revisited unless the product direction changes significantly.

### Developer Philosophy

The owner directs **what** to build (product decisions, workflows, business rules). The developer (Claude Code) makes all **technical implementation decisions** — which library, which database pattern, how to structure a query, which service to use. If there is one logical right answer given the stack, it is used without asking. Only genuinely product-impacting tradeoffs are surfaced for owner input.

---

### White-Labeling

**Decision: Yes — full white-label support.**

Each client company can make the platform feel like their own branded software, not a generic SaaS tool. This is expected at the $10k/month price point and is already partially architected through the Theme & Branding admin module.

**What white-labeling covers:**

- **Logo** — company logo appears in the sidebar header and on all generated documents (BOL, estimates, invoices). Light and dark variants uploadable. Stored in Supabase Storage.
- **Colors** — primary accent color, sidebar color, button color — all configurable via the Theme & Branding tab in Admin. Stored in `companies.settings` as JSONB.
- **Custom domain** — each company can have the platform served at their own domain or subdomain (e.g., `dispatch.tampabaymovers.com`) instead of `app.movepro.io`. Implemented via Vercel's custom domain API — a domain is added programmatically to the Vercel project when a company is onboarded.
- **Customer portal subdomain** — the customer-facing portal is served at a separate subdomain (e.g., `portal.tampabaymovers.com`). Same mechanism.
- **Document branding** — all PDFs (BOL, estimate, invoice, timesheet) use the company's logo, colors, name, DOT/MC numbers, and contact info in the header and footer.

**What white-labeling does NOT cover in V1:**
- Completely custom CSS/design systems — the layout structure stays consistent
- Removing "Powered by MovePro" from documents (this can be toggled per plan tier later)

**Technical implementation:**
- `companies.settings` stores theme config: `{ primaryColor, sidebarColor, logoUrl, logoUrlDark }`
- At runtime, the Next.js layout reads the authenticated user's company settings and injects CSS custom properties
- Custom domains are added to Vercel via the Vercel API during manual onboarding; DNS instructions are provided to the client
- No per-company deployments — one codebase, one deployment, domains routed to the same app

---

### Client Onboarding

**Decision: Manual onboarding for V1. Self-serve as Phase 2.**

At $10k/month, deals are large enough to warrant white-glove onboarding. The platform owner (you) manually provisions each new client company. There is no public-facing signup flow in V1.

**Manual onboarding process:**
1. Contract signed
2. Platform owner uses the **Internal Platform Admin** (see below) to create the new company record
3. System seeds the company with default configuration: roles, pipeline stages (HHG and Commercial), truck types, task rules, and rate sheet defaults
4. Platform owner creates the client's first Admin user account — credentials sent to client
5. Client's Admin logs in, customizes branding, adds their team, configures their specific rates and settings
6. Platform owner adds the client's custom domain to Vercel (5-minute step)

**Seed data on company creation:**
New companies are provisioned with sensible defaults so they can be operational quickly:
- Default roles (Admin, HHG Coordinator, Dispatcher, Billing, Crew/Driver, etc.)
- HHG and Commercial pipeline stages
- Standard truck types (Cargo Van, Sprinter, 16ft, 26ft, 53ft)
- Default task rules (12 standard trigger → task rules)
- Default rate sheet (local crew rates, CZAR-LITE grid, standard fuel surcharge)

All defaults are editable by the client's Admin immediately after login.

**Historical data migration:** After the account is provisioned, the platform owner assists with importing the client's existing data (customers, job history, crew, fleet, outstanding invoices) via the CSV import tool in Admin. CompuMove exports map automatically. See the Data Import & Migration section in Module 17 for full detail.

**Phase 2 — Self-Serve Signup:**
When the business scales beyond what manual onboarding can handle, a public-facing signup flow will be added:
- Marketing website with pricing page
- Stripe checkout for subscription purchase
- Automated company provisioning on successful payment
- Guided onboarding wizard (business name, DOT/MC, first user, business line selection)

This is not built in V1. The architecture supports it — adding self-serve is adding a signup page and an automated version of the manual provisioning step.

---

### Subscription Billing & Access Control

**Decision: Billing is external. Access is controlled by a single field the billing system updates.**

MovePro does not manage client billing internally. Client invoicing and payment collection happens outside the app — via Stripe, a CRM, or however the platform owner handles contracts. The app only needs to know one thing: is this company's subscription active or not?

**How it works:**

The `companies` table has a `subscription_status` field:
```
active    → full access
trial     → full access, banner showing trial expiry date
suspended → login blocked, "subscription inactive" screen shown
```

An external billing system (Stripe subscriptions, manual update, or a simple internal dashboard) updates this field via a secure webhook endpoint:
```
POST /api/platform/subscription-update
{ company_id, status, trial_ends_at }
Bearer: PLATFORM_SECRET_KEY
```

This endpoint is not accessible to clients — it is called only by the platform owner's billing system or manually by the platform owner.

**What clients experience:**
- Active: no indication of billing in the app at all — they just use it
- Trial: a subtle banner showing days remaining; otherwise full access
- Suspended: on next login, a full-screen "Your subscription is inactive — contact support" page. No data is deleted. Access resumes the moment status is set back to `active`.

**Platform owner's billing view:**
The Internal Platform Admin (see below) shows all companies with their current `subscription_status`, trial end date, and contract start date. The platform owner can manually toggle status from here without touching the database directly.

**Phase 2 — Stripe integration:**
When self-serve billing is added, Stripe webhooks (`customer.subscription.updated`, `invoice.payment_failed`, etc.) will hit the subscription-update endpoint automatically. The manual override will remain as a fallback.

---

### Internal Platform Admin

A separate, protected admin layer that only the platform owner (you) can access. This is NOT the company-level Admin & Settings — this is your dashboard to manage all client companies.

**Access:** A special `platform_admin` flag on specific user accounts. Protected by a separate auth check; not accessible to any client user regardless of their role.

**What it shows:**
- List of all companies with: name, plan, subscription status, user count, date created, last active
- Per-company detail: users, storage usage, job count, integration status
- Actions: create new company (provisioning), toggle subscription status, add custom domain, view company as admin (impersonation for support purposes)
- Subscription status update form (manual override without needing to touch Supabase directly)

**What it is NOT:**
- Not a billing dashboard — payment processing and invoicing happens in your external system
- Not visible to any client — completely separate from the in-app admin that clients use

---

### Multi-Tenancy Model

**Decision: Full multi-tenant SaaS from day one.**

MovePro will be built as a platform that multiple moving companies can use simultaneously. The initial deployment will be a single company (the owner's company) used as a stress-test and production validation. When ready to onboard additional companies, the architecture is already in place — no refactoring needed.

**Implementation:**
- Every data table includes a `company_id` foreign key
- All database queries are automatically scoped to the authenticated user's `company_id`
- Supabase Row Level Security (RLS) enforces this at the database level — a user from Company A cannot read, write, or even detect the existence of Company B's data, regardless of what the application layer does
- Company onboarding creates a new row in the `companies` table and seeds the company's default roles, pipeline stages, truck types, and task rules
- Each company gets its own isolated data environment within the shared database

**Launch approach:** Deploy with one `company_id`. When Company 2 signs up, they get a new `company_id` and their data is completely separate. No code changes required.

---

### Security Model

**Two layers, different levels of strictness:**

#### Layer 1 — Company Isolation (External Security) — STRICT
This is the most critical security layer. A user from one moving company must never be able to see another company's data under any circumstances.

- Enforced by **Supabase Row Level Security (RLS)** at the database level
- Every SELECT, INSERT, UPDATE, DELETE query is automatically filtered by `company_id = auth.jwt() -> 'company_id'`
- This cannot be bypassed from the application layer — it's enforced by the database itself
- Even if there is a bug in the Next.js code, the database will not return another company's rows

#### Layer 2 — Internal Role Permissions (Employee Access) — MODERATE
Controls what employees within a company can see and do. Less critical (employees are trusted) but still enforced.

- Enforced by **Next.js API middleware** — every API route checks the authenticated user's role and permissions before processing
- The RBAC permission matrix (Full / Read-Only / Hidden per module) is stored in the `roles` table and checked on every request
- Sensitive modules (Billing, Rate Sheets, Admin, Recycle Bin) get explicit server-side checks even if the UI already hides them
- For V1: internal RBAC is enforced at the API layer. Row-level employee scoping (e.g., a salesperson can only see their own leads) is enforced in the query logic, not as RLS. This is sufficient for V1 and can be tightened in V2 if needed.

#### Authentication
- **Supabase Auth** handles login, sessions, password reset, and JWTs
- JWT includes `company_id` and `role_id` as custom claims — available server-side without an extra DB lookup
- Sessions expire after 24 hours of inactivity; users re-authenticate automatically via refresh tokens
- All API routes require a valid session token; unauthenticated requests are rejected
- Customer portal users have a separate, limited JWT that only grants access to their own portal data

---

### Database Schema

Full table definitions. All tables include `created_at TIMESTAMPTZ DEFAULT now()` and `updated_at` where records are mutable. All IDs are UUIDs.

#### Tenancy & Users

**`companies`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| name | text | Company display name |
| slug | text UNIQUE | URL-safe identifier |
| dot_number | text | |
| mc_number | text | |
| address | text | |
| phone | text | |
| email | text | |
| logo_url | text | Supabase Storage URL |
| subscription_status | text | active / trial / suspended |
| trial_ends_at | timestamptz | Null if not on trial |
| custom_domain | text | e.g. dispatch.tampabaymovers.com — added to Vercel on onboarding |
| portal_domain | text | e.g. portal.tampabaymovers.com |
| settings | jsonb | `{ primaryColor, sidebarColor, logoUrl, logoUrlDark, defaultBusinessLine }` |
| contract_start | date | When client signed — for platform owner reference |

**`users`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | Matches Supabase Auth user ID |
| company_id | uuid FK → companies | |
| role_id | uuid FK → roles | |
| name | text | |
| email | text | |
| phone | text | |
| active | boolean | |
| platform_admin | boolean | Default false. True only for platform owner accounts. Grants access to Internal Platform Admin. Never exposed to client users. |

**`roles`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK → companies | |
| name | text | e.g. "HHG Coordinator" |
| scope | text | both / hhg / commercial |
| permissions | jsonb | `{ "CRM & Leads": "full", "Billing": "hidden", ... }` |
| is_default | boolean | Assigned to new users automatically |

---

#### CRM & Sales

**`leads`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| lead_no | text | L-XXXX format |
| name | text | Contact or company name |
| phone | text | |
| email | text | |
| origin_city | text | |
| origin_state | text | |
| destination_city | text | |
| destination_state | text | |
| move_date | date | |
| estimated_rooms | integer | Room count from initial call |
| estimated_value | numeric | Added after estimate is built |
| source | text | Website / HireAHelper / Referral / etc. |
| stage | text | New Lead / Contacted / Estimate Sent / Follow-Up / Quoted / Booked |
| business_line | text | hhg / commercial |
| salesperson_id | uuid FK → users | Nullable (unassigned) |
| coordinator_id | uuid FK → users | |
| hot | boolean | |
| notes | text | |
| booked_at | timestamptz | Set when stage → Booked |

**`lead_activity`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| lead_id | uuid FK → leads | |
| company_id | uuid FK | |
| type | text | status / note / email / lead / complete |
| user_id | uuid FK → users | Null if system-generated |
| text | text | |
| created_at | timestamptz | |

**`customers`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| customer_no | text | CUST-XXXX format |
| name | text | |
| phone | text | |
| email | text | |
| type | text | hhg / commercial |
| tags | text[] | Recurring, VIP, Military, etc. |
| pinned_note | text | Shown prominently on profile |
| rating | integer | 1–5 internal rating |
| notes | text | |

---

#### Jobs & Files

**`files`** ← Top-level customer relationship container
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| file_no | text | FILE-YYYY-XXXX format |
| customer_id | uuid FK → customers | |
| lead_id | uuid FK → leads | Origin lead |
| salesperson_id | uuid FK → users | |
| coordinator_id | uuid FK → users | |
| business_line | text | hhg / commercial |

**`job_events`** ← Individual service instances under a file
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| file_id | uuid FK → files | |
| job_no | text | JOB-XXXX format |
| event_type | text | move / packing / storage_in / storage_recurring / haul_out / partial_delivery / commercial_move |
| status | text | booked / dispatched / in_progress / completed / invoiced / cancelled |
| business_line | text | hhg / commercial |
| move_date | date | |
| time_window | text | "8:00 AM – 12:00 PM" |
| origin_address | text | |
| origin_city | text | |
| origin_state | text | |
| destination_address | text | |
| destination_city | text | |
| destination_state | text | |
| estimated_hours | numeric | |
| men_required | integer | From estimate |
| men_adjusted | integer | Dispatcher override; null if not overridden |
| valuation_coverage | text | released_standard / released_basic / full_value / third_party |
| special_instructions | text | |
| notes | text | |

**`job_crew_assignments`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| job_event_id | uuid FK → job_events | |
| company_id | uuid FK | |
| crew_member_id | uuid FK → crew_members | |
| assigned_at | timestamptz | |

**`job_truck_assignments`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| job_event_id | uuid FK → job_events | |
| company_id | uuid FK | |
| vehicle_id | uuid FK → vehicles | |
| assigned_at | timestamptz | |

**`crew_timesheets`** ← Clock-in/out records per job per crew member
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| job_event_id | uuid FK → job_events | |
| company_id | uuid FK | |
| crew_member_id | uuid FK → crew_members | |
| clock_in | timestamptz | |
| clock_out | timestamptz | Null while active |
| hours_worked | numeric | Computed on clock-out; stored for billing |
| rate_at_time | numeric | Snapshot of crew member's rate at job time — never changes after clock-out |

---

#### Estimating & Quotes

**`estimates`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| lead_id | uuid FK → leads | |
| estimate_no | text | EST-XXXX |
| total_cf | numeric | |
| difficulty | text | easy / moderate / hard / very_hard |
| target_days | integer | |
| men_needed | integer | |
| labor_cost | numeric | |
| supervisor_cost | numeric | |
| truck_cost | numeric | |
| fuel_surcharge_pct | numeric | |
| total | numeric | |
| status | text | draft / sent / accepted / declined / expired |
| sent_at | timestamptz | |

**`estimate_lines`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| estimate_id | uuid FK → estimates | |
| name | text | Item name |
| cf | numeric | Cubic footage |
| qty | integer | |
| note | text | |
| custom | boolean | User-added vs library item |
| sort_order | integer | |

**`quotes`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| lead_id | uuid FK → leads | |
| estimate_id | uuid FK → estimates | Nullable — quotes can exist without an estimate |
| quote_no | text | Q-YYYY-XXXX |
| status | text | draft / sent / viewed / accepted / declined / expired |
| expires_at | date | |
| sent_at | timestamptz | |
| viewed_at | timestamptz | |
| accepted_at | timestamptz | |
| total | numeric | |
| notes | text | |

**`quote_lines`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| quote_id | uuid FK → quotes | |
| label | text | |
| detail | text | |
| amount | numeric | |
| sort_order | integer | |

---

#### Billing

**`invoices`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| job_event_id | uuid FK → job_events | |
| customer_id | uuid FK → customers | |
| invoice_no | text | INV-XXXX |
| billing_type | text | estimate / actual / edited |
| status | text | draft / sent / partial / paid / overdue |
| total | numeric | |
| amount_paid | numeric | Default 0 |
| due_date | date | |
| sent_at | timestamptz | |
| paid_at | timestamptz | |
| notes | text | |

**`invoice_lines`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| invoice_id | uuid FK → invoices | |
| label | text | |
| detail | text | |
| amount | numeric | |
| sort_order | integer | |
| deleted | boolean | Soft-delete for edit invoice flow |

**`payments`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| invoice_id | uuid FK → invoices | |
| company_id | uuid FK | |
| amount | numeric | |
| method | text | check / ach / card / cash |
| reference | text | Check number, transaction ID, etc. |
| paid_at | timestamptz | |
| notes | text | |

---

#### Crew & Fleet

**`crew_members`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| name | text | |
| role | text | Lead / Driver / Helper / Warehouse Lead / etc. |
| team | text | Local / Long Distance / Commercial / Warehouse |
| phone | text | |
| email | text | |
| status | text | active / inactive / terminated |
| availability | text | available / off / unavailable |
| pay_rate | numeric | Hourly rate |
| rate_type | text | hourly / flat |
| hire_date | date | |
| notes | text | |

**`crew_absences`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| crew_member_id | uuid FK → crew_members | |
| company_id | uuid FK | |
| type | text | PTO / Call Off / No Show / Injury / Suspension / Other |
| date_from | date | |
| date_to | date | Null for open-ended (injury leave) |
| notes | text | |
| logged_by_id | uuid FK → users | |

**`crew_restrictions`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| crew_member_id | uuid FK → crew_members | |
| company_id | uuid FK | |
| tag | text | Light Duty / No Driving / Certification Lapsed / Probationary |
| added_at | timestamptz | |

**`vehicles`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| unit | text | "Truck #3" |
| type | text | 26ft Box Truck / Cargo Van / etc. |
| make | text | |
| model | text | |
| year | text | |
| license_plate | text | |
| vin | text | |
| status | text | active / in_maintenance / out_of_service / reserved / retired |
| status_note | text | |

---

#### Warehouse & Storage

**`warehouses`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| name | text | |
| address | text | |
| total_vaults | integer | |
| sqft | integer | |
| active | boolean | |

**`vaults`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| warehouse_id | uuid FK → warehouses | |
| unit | text | "Vault A-07" |
| row | text | |
| section | text | |
| bay | text | |
| size | text | "10×10" |
| capacity_cf | integer | |
| used_cf | integer | |
| status | text | occupied / empty / partial / reserved |
| storage_type | text | long_term / sit / commercial |
| customer_id | uuid FK → customers | Null if empty |
| file_id | uuid FK → files | |
| since | date | |
| rate | numeric | |
| billing_cycle | text | monthly / daily |
| notes | text | |

**`vault_items`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| vault_id | uuid FK → vaults | |
| company_id | uuid FK | |
| name | text | |
| qty | integer | |
| cf | numeric | |
| condition | text | good / fair / damaged / unknown |
| notes | text | |

**`incoming_shipments`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| warehouse_id | uuid FK → warehouses | |
| name | text | Shipment reference name |
| shipper | text | |
| customer_id | uuid FK → customers | |
| file_id | uuid FK → files | |
| arrival_type | text | specific / spread |
| arrival_date | date | Null if spread |
| arrival_time | text | Null if spread |
| arrival_date_from | date | Null if specific |
| arrival_date_to | date | Null if specific |
| target_vault_id | uuid FK → vaults | |
| status | text | expected / arrived / received / discrepancy / overdue |
| assigned_to_id | uuid FK → crew_members | |
| contents | text | |
| special_instructions | text | |
| receiving_complete | boolean | |

---

#### Claims

**`claims`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| job_event_id | uuid FK → job_events | |
| customer_id | uuid FK → customers | |
| claim_no | text | CLM-XXXX |
| coverage_type | text | released_basic / released_standard / full_value / third_party |
| status | text | filed / under_review / settlement_offered / accepted / disputed / closed |
| filed_at | date | |
| notes | text | |
| settlement_amount | numeric | |
| assigned_to_id | uuid FK → users | |

**`claim_items`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| claim_id | uuid FK → claims | |
| name | text | Item name |
| weight_lbs | numeric | |
| declared_value | numeric | |
| damage_description | text | |
| settlement_amount | numeric | Auto-calculated for released value |

---

#### Documents & Files

**`documents`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| job_event_id | uuid FK → job_events | Nullable |
| lead_id | uuid FK → leads | Nullable |
| customer_id | uuid FK → customers | Nullable |
| type | text | bol / estimate / invoice / order_for_service / receiving_report / other |
| name | text | |
| status | text | draft / sent / signed / completed |
| file_url | text | Supabase Storage URL |
| version | integer | Default 1; incremented on regeneration |

**File storage:** All uploaded files, generated PDFs (BOLs, invoices, estimates), and photos are stored in **Supabase Storage** in a bucket named `company-files`, organized as `/{company_id}/{document_type}/{document_id}.pdf`. Access is controlled by Supabase Storage RLS policies matching the same `company_id` isolation as the database.

**PDF generation:** All documents (BOL, invoice, estimate, timesheet) are generated server-side using **`@react-pdf/renderer`** (react-pdf). Generation is triggered by a Next.js API route, the PDF is uploaded to Supabase Storage, and the `file_url` is saved to the `documents` table. The user always downloads from the stored URL — PDFs are never generated on-demand twice.

---

#### Automation & Tasks

**`automation_sequences`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| name | text | |
| trigger | text | new_lead / estimate_sent / job_booked / etc. |
| category | text | lead_nurture / operational / post_move |
| channel | text | email / sms / both |
| status | text | active / paused / draft |
| business_line | text | hhg / commercial / both |

**`automation_steps`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| sequence_id | uuid FK → automation_sequences | |
| company_id | uuid FK | |
| delay_hours | integer | Hours after previous step (0 = immediate) |
| channel | text | email / sms |
| subject | text | Email subject (null for SMS) |
| body | text | Message body with `{firstName}` style variables |
| sort_order | integer | |

**`automation_sends`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| step_id | uuid FK → automation_steps | |
| company_id | uuid FK | |
| lead_id | uuid FK → leads | |
| status | text | pending / sent / delivered / failed / opened |
| scheduled_at | timestamptz | |
| sent_at | timestamptz | |
| opened_at | timestamptz | |

**`tasks`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| assigned_to_id | uuid FK → users | Nullable — assigned to a role instead |
| assigned_to_role | text | Nullable — if assigned to all users with a role |
| title | text | |
| description | text | |
| priority | text | urgent / high / normal / low |
| status | text | open / in_progress / complete / dismissed |
| due_date | date | |
| linked_record_type | text | lead / job / invoice / crew_member / vehicle |
| linked_record_id | uuid | |
| created_by | text | user_id or "system" |
| notes | text | |

**`task_rules`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| trigger_event | text | new_lead_assigned / estimate_sent / job_completed / etc. |
| task_title | text | Template with `{jobNo}` style variables |
| task_description | text | |
| priority | text | |
| due_window | text | "2h" / "1d" / "3d" / "1w" |
| assignee_role | text | Which role the task is assigned to |
| business_line | text | hhg / commercial / both |
| active | boolean | |

---

#### Integrations & API

**`integrations`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| key | text | quickbooks / twilio / google_maps / stripe / etc. |
| status | text | connected / disconnected / error |
| config | jsonb | Encrypted API keys, tokens, account IDs |
| connected_at | timestamptz | |
| last_sync_at | timestamptz | |
| error_message | text | |

**`api_keys`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| name | text | |
| key_hash | text | bcrypt hash — full key shown only at creation |
| scopes | text[] | ["jobs:read", "invoices:read"] |
| active | boolean | |
| last_used_at | timestamptz | |

**`webhook_endpoints`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| url | text | |
| events | text[] | ["job.created", "invoice.paid"] |
| status | text | active / failing / paused |
| last_triggered_at | timestamptz | |
| success_rate | numeric | Rolling 30-day % |

---

#### System

**`audit_log`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| user_id | uuid FK → users | |
| action | text | create / update / delete / restore |
| record_type | text | lead / job / invoice / etc. |
| record_id | uuid | |
| changes | jsonb | `{ field: { from: x, to: y } }` |
| created_at | timestamptz | Immutable — no updates ever |

**`recycle_bin`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| deleted_by_id | uuid FK → users | |
| record_type | text | |
| record_id | uuid | Original ID of deleted record |
| record_data | jsonb | Full snapshot of the record at time of deletion |
| deleted_at | timestamptz | |
| expires_at | timestamptz | 90 days after deleted_at by default |
| restored_at | timestamptz | Null until restored |

---

### Background Jobs

These processes run on a schedule or in response to events. They cannot be triggered by a user directly.

**Implementation:** Vercel Cron Jobs for time-based jobs; Supabase database triggers + pg_cron for data-driven jobs. When we start building each module, the relevant background job is built alongside it.

| Job | Trigger | What it does |
|-----|---------|-------------|
| **Recurring invoice generation** | 1st of each month, midnight | For every active vault with `billing_cycle = monthly`, creates an invoice record and queues delivery |
| **Automation sequence processor** | Every 15 minutes | Checks `automation_sends` for items with `scheduled_at <= now()` and `status = pending`; sends via Twilio/SendGrid; updates status |
| **Invoice overdue checker** | Daily at 8am | Marks invoices past `due_date` as `overdue`; creates tasks for billing team |
| **Lead follow-up reminder** | Daily at 8am | Checks leads with no activity in X days; creates tasks per task rules |
| **Recycle bin cleanup** | Daily at midnight | Permanently deletes records where `expires_at < now()` and `restored_at IS NULL`; alerts admin before financial records are purged |
| **Webhook delivery** | On event | When a job/invoice/lead event fires, POST payload to all matching `webhook_endpoints` for that company; update success rate |
| **Integration sync** | Per integration schedule | QuickBooks sync every 4 hours; HireAHelper lead pull every 5 minutes; etc. |
| **Capacity projection** | Daily at 6am | Recalculates 30/60/90-day vault demand forecast and updates warehouse metrics |

---

### Rate Sheets Configuration Storage

Rate sheets (crew hourly rates, CZAR-LITE grid, fuel surcharge, truck rates) are stored in a `rate_configs` table as versioned JSONB blobs rather than individual rows. This makes it easy to update the entire rate sheet atomically and keep a history of changes.

**`rate_configs`**
| Column | Type | Notes |
|--------|------|-------|
| id | uuid PK | |
| company_id | uuid FK | |
| type | text | local_crew / local_trucks / czar_lite / fuel_surcharge |
| config | jsonb | Full rate structure |
| effective_date | date | When this rate version takes effect |
| created_by_id | uuid FK → users | |
| created_at | timestamptz | |

Estimates and invoices snapshot the rates at time of creation so historical records are never affected by rate changes.

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
4. **Quotes & Proposals** — output of the Estimator; requires Estimating
5. **Rate Sheets & Tariffs** — pricing engine; feeds Estimating and Billing
6. **Jobs + Rate Engine** — core record + pricing; requires customer accounts
7. **Scheduling + Dispatch** — operations; requires jobs and crew management
8. **BOL + Forms** — generated at dispatch; requires dispatch details
9. **Billing + Invoicing** — money in; requires completed jobs
10. **Claims Management** — requires jobs and valuation coverage data
11. **Warehouse + Storage** — storage clients; requires jobs for Storage In events
12. **Long Distance & Interstate** — requires Rate Sheets and Jobs
13. **Reporting** — intelligence layer; requires data from all above
14. **Internal Task System** — threads through all roles and modules
15. **Automation** — customer-facing email/SMS; requires jobs and leads
16. **Customer Portal** — customer-facing self-service
17. **Integrations + API** — ecosystem connections

---

---

## Production Build — Status & Implementation Log

**Production repo:** `github.com/TooSmartNA/movepro` (private)  
**Stack:** Next.js 16, TypeScript, Tailwind CSS v4, shadcn/ui (base-ui variant), Supabase (PostgreSQL + Auth + RLS), Vercel  
**Database:** Live Supabase project — 20 tables, full RLS, pg_cron ready  
**Tenant #1:** South Hills Movers (owner's company — stress-test environment)  
**Started:** 2026-05-31

### Foundation (Complete)

- Next.js 16 production app scaffolded at `C:\Users\Toosm\movepro`
- All 20 database tables created with RLS policies, indexes, triggers, and helper functions
- `get_company_id()` PostgreSQL function reads `company_id` from JWT — all queries auto-scoped via RLS without application-level filtering
- `is_platform_admin()` PostgreSQL function enables owner to manage all tenants invisibly
- `handle_new_user()` trigger auto-syncs `auth.users` → `public.users` on signup
- Supabase Auth with custom JWT `app_metadata` stamps (`company_id`, `platform_admin`)
- `proxy.ts` auth middleware (Next.js 16 convention) — every dashboard route is protected
- Three Supabase client modes: `client.ts` (browser), `server.ts` (Server Components/Actions), `admin.ts` (service role, bypasses RLS for platform-admin operations only)
- Deep navy sidebar + confident blue primary + Geist font — matches prototype visual design
- AppSidebar: collapsible, permission-filtered nav, 7 groups matching prototype (Sales, Operations, Finance, Storage, Specialty, Intelligence, System)
- TopNav: breadcrumb, search bar, notification button, user dropdown with sign-out
- Login page: premium centered card on dark navy background

### TypeScript Note for Reviewer

Manual type stubs live in `types/database.ts` to satisfy imports before `supabase gen types` is run against the live DB. Server Actions use `as AnyClient` casts to bypass Supabase's generic insert/update inference until generated types are in place. This is a known temporary pattern — running `npx supabase gen types typescript --project-id euyrdlxzakeppxexgero > types/database.ts` will replace all manual stubs with auto-generated, fully-typed definitions. No logic is affected.

### Modules Built (Production — real DB, real auth)

| Module | Route | Status | Notes |
|--------|-------|--------|-------|
| Dashboard | `/dashboard` | ✅ Live | KPI cards query live DB (scheduled jobs, leads, customers, outstanding AR) — all RLS-scoped |
| Customers | `/customers` | ✅ Live | Full CRUD: list with search, Add Customer sheet, soft delete + undo toast + recycle bin snapshot, inline field editing, job history, auto-save notes |
| Customer Profile | `/customers/[id]` | ✅ Live | Inline editing on all fields, job history linked, notes auto-save on blur |

### Modules Remaining (Placeholder pages exist — to be built)

CRM, Estimating, Quotes, Jobs, Dispatch, Crew & Fleet, Billing, Rate Sheets, Claims, Long Distance, Warehouse, BOL & Forms, Tasks, Reporting, Automation, Integrations, Admin & Settings, Recycle Bin, Commercial Moving

### Key Patterns Established in Production Code

- **Server Actions** for all mutations — `"use server"` functions in `actions.ts` colocated with the route
- **`revalidatePath()`** after every mutation — Next.js cache invalidation keeps the UI fresh
- **Optimistic UI + undo** — client removes the record immediately, shows a 6-second sonner toast with Undo, then commits the server delete after a 500ms delay. If Undo is clicked, `restoreCustomer()` is called and the record is re-inserted into local state.
- **Recycle bin snapshot** — every soft delete writes a full JSON snapshot of the record to the `recycle_bin` table before deleting, enabling full restore
- **`lib/supabase/query.ts`** — `row<T>()` and `rows<T>()` helpers for type-safe Supabase query results before gen types are run

---

*Document created: 2026-05-30*  
*Last audited: 2026-05-31 (sixth pass) — Production build started. Foundation complete. Customers module live with real Supabase backend. Production repo: github.com/TooSmartNA/movepro*
