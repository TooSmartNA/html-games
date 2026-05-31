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
The operations calendar. Dispatchers live here.

- Monthly, weekly, and daily calendar views
- Job assignment to crews and trucks
- Crew member availability management
- Truck/equipment availability management
- Conflict detection (double-booking prevention)
- Daily dispatch sheet generation
- Worker schedule view (what each crew member is doing each day)
- Route optimization (for local multi-stop days)
- Real-time status updates from field
- Notifications: text, email, push to crew
- Google Calendar integration for crew
- Dispatcher notes per job/day
- **Exceeds CompuMove:** Drag-and-drop dispatch board, capacity heatmap by day/week

---

### MODULE 6 — Crew & Mobile Operations
What the crew sees and uses in the field.

- Crew mobile app (phone/tablet)
- Daily job list for each crew member
- Turn-by-turn directions to job
- Digital inventory checklist at pickup
- Photo capture at pickup and delivery (condition documentation)
- Customer signature at pickup (BOL acknowledgment)
- Customer signature at delivery (completion)
- Time tracking — clock in/out per job
- Actual hours logged vs. estimated
- Packing material usage logging
- Exception reporting (damages, access issues, delays)

---

### MODULE 7 — Bill of Lading & Forms
DOT/FMCSA compliant document generation.

- Bill of Lading (BOL) auto-generated from job record
- BOL includes: estimated weight, inventory list, carton counts, special notes, valuation
- High-value inventory form
- Order for Service
- Inventory exception form (PRE items)
- Delivery receipt
- Warehouse receipt
- All forms include e-signature fields
- PDF download and email delivery
- DOT/FMCSA required fields enforced
- **Exceeds CompuMove:** Digital BOL on mobile — no paper required

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
- Crew utilization
- Truck utilization
- Actuals vs. estimates variance
- Claims rate

**Financial Reports:**
- Revenue by job type (local, LD, storage, commercial)
- Accounts receivable aging
- Commission reports
- Storage revenue
- Profit/loss per job

**Custom Report Builder:**
- Export any data set to spreadsheet
- Hundreds of data points queryable per shipment
- Saved report templates

---

### MODULE 14 — Automation & Follow-Ups
Set it and forget it workflows.

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
Platform configuration. Admin role only.

- Company profile (logo, branding, DOT/MC numbers, insurance)
- User accounts and role assignments
- **Custom Role Builder** — create new roles from scratch, name them, assign per-module permissions via a visual permission matrix (Full / Read-Only / Hidden per module)
- **Workflow Customization** — edit pipeline stages, rename them, reorder them, add or remove stages for both HHG and Commercial pipelines independently
- Branch/location management (multi-location companies)
- Notification preferences
- Rate sheet management
- Document template customization
- Audit log (who changed what and when)
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
| **Crew / Driver** | Both | Crew & Mobile view only (daily jobs, signatures, photos) |
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
