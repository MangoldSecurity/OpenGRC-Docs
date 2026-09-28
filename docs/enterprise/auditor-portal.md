# Auditor Portal

!!! enterprise "Enterprise Feature"
    The Auditor Portal is available exclusively in OpenGRC Enterprise. [Learn more about Enterprise](https://opengrc.com).

The Auditor Portal gives an external audit firm its own secure, scoped view into a specific audit -- called an **Engagement** -- without granting them access to OpenGRC itself. From the Engagement page, you control exactly what the firm can see, invite individual auditors, exchange evidence through the same Data Request workflow used internally, and keep an append-only log of everything the firm does.

## Overview

The Auditor Portal provides:

- A dedicated `/auditor` login for external audit firm staff, separate from the main app and from My Portal
- Per-audit **Engagements**, scoped to one audit firm, with fine-grained control over what's visible (control text, implementation details, IP restrictions)
- A shared Information Request List (IRL) that both sides work from, with dual status tracking (internal progress vs. what the firm sees)
- Auditor-initiated requests, document delivery, bulk IRL import, and proposed findings
- A full, exportable, append-only access log for every action an auditor takes
- Configurable access windows, expiry warnings, and a full set of dedicated email notifications

## Setting Up

### 1. Enable the Auditor Portal

**Settings > Auditor Portal** (`/admin/auditor-portal-settings`):

**General Settings**

| Setting | Description |
|---------|-------------|
| **Enable Auditor Portal** | Toggle. While off, `/auditor` returns 404 to everyone, including auditors with a live invitation |
| **Portal Name** | Display name shown to external auditors (default "Auditor Portal") |

**Access Windows**

| Setting | Description |
|---------|-------------|
| **Invitation Expiry (days)** | How long an invitation link stays redeemable |
| **Warn Manager (days before)** | Days before an access window closes that the audit manager is warned |
| **Warn Auditor (days before)** | Days before their access window closes that the auditor is warned |

**Notifications**

| Setting | Description |
|---------|-------------|
| **Submission Digest Interval (minutes)** | Newly submitted requests are batched into one email per auditor per interval, rather than emailing on every submission |

**Access Terms**

Auditors must accept a terms-of-access screen before reaching any content. **Terms Text** holds the full text (a plain-text legal document covering purpose of access, confidentiality, retention, scope, account responsibility, logging/monitoring, duration, warranty, and changes); **Terms Revision** is a number you bump whenever the text changes materially -- doing so re-prompts every auditor on their next request, while existing acceptances stay recorded against the revision they were made under.

### 2. Mark a Vendor as an Audit Firm

An audit firm is a Vendor with an **Audit firm** toggle enabled. This lives on the vendor's **edit** page, in the Vendor Information section -- not the creation wizard. You must create the vendor first, then edit it to flag it as an audit firm.

!!! note "Not available at creation"
    The **Audit firm** toggle does not appear in the 4-step vendor creation wizard. Create the vendor normally, then open it for editing to flag it.

Enabling the toggle is implemented as a system-wide **Audit Firm** tag (visible in the same form's Tags field) rather than a separate flag -- adding or removing the tag directly has the same effect. Once flagged, the vendor record gains an **Auditors** tab (alongside the usual Overview, Applications, Implementations, Risks, Surveys, Documents, and Portal Users tabs) titled **Auditor Users**: a table of people from that firm with portal access, showing Name, Email, Active Audits, Status, and Last Login. This is separate from the vendor's ordinary **Portal Users** tab -- auditor-firm staff are a distinct user type from regular vendor portal contacts.

### 3. Set the Audit Firm on an Audit

On an audit's **edit** page:

- **Audit Firm** -- a searchable select listing only vendors tagged Audit Firm. A **Show all vendors** toggle overrides the filter if needed. Leave empty for an internal audit.
- **Auditor portal** (collapsible section) -- controls what this engagement exposes:
    - **Share control text** -- show the firm the full text of the controls behind each request
    - **Share implementation details** -- show the firm how each control is implemented
    - **IP allow-list** -- restrict connections to specific addresses/ranges for this engagement only; other engagements the same auditor holds are unaffected

Once an Audit Firm is set, an **Engagement** button appears on the audit's view page next to Edit.

## The Engagement Page

Clicking **Engagement** opens a dedicated page (titled "Engagement -- *{Firm Name}*") with four tabs.

### Information Request List

Every request on this engagement, from the audit team's side. Columns: **Firm ref**, **Request**, **Control**, **Auditor** (sharing status -- Not Shared / Open / etc.), **Version**, **Source** (Internal or Auditor -- who originated it), **Type**, **Assigned to**, and row actions **Share with auditor**, **Submit to Auditor**, **Map to control**, and **Reassign**. Unmapped rows aren't tied to a control yet; rows with Source "Auditor" came in through the firm's own Import IRL or Raise a Request actions (see below).

Clicking **Share with auditor** confirms: *"The firm will see this request on their list. Nothing you have collected against it is shared until you submit."* -- sharing and submitting are two separate steps.

### Auditors

Everyone from the firm working this audit: Name, Email, **Role** (Lead Auditor / Staff Auditor), **Access Window** (start/end date range), Status, Invitation (Accepted/Pending), Last Login. Row actions: **Edit access**, **Extend**, **Resend invite**, **Revoke**, **Detach**.

Two buttons add auditors:

- **Invite Auditor** -- sends a new invitation. Fields: **Name**, **Email**, **Role** (Lead Auditor / Staff Auditor), **Access starts** (defaults to now), **Access ends** (defaults to 30 days past the audit's end date -- completing the audit does not end access, only this date does). An email already registered to the firm keeps its existing login rather than getting a new one.
- **Attach Auditor** -- adds someone already active on another engagement at the same firm, without sending a fresh invitation.

The invitation email's link lets the auditor set a password and enroll in mandatory two-factor authentication -- 2FA is required at first login and on every login after.

### Auditor Documents

Reports, letters, and working papers the firm delivers through their side of the portal. Columns: Document, Type, From, Delivered, **Our review**, Size. Empty state: *"Nothing delivered yet -- Documents the audit firm uploads through the portal appear here."*

### Auditor Access Log

An append-only record of everything the firm has done: When, Auditor, Action, Subject, IP, with an **Export CSV** button. Logged actions include Login, Terms Accepted, and Invitation Accepted, alongside every request/document interaction. Entries are only ever removed by the retention schedule. A tenant-wide version of this log (across every engagement) is available at **Settings > Auditor Access Log**.

## Data Requests: The Dual-Status Model

A Data Request shared with an auditor tracks two parallel status tracks at once, shown side by side on the request:

| Track | Statuses |
|-------|----------|
| **Internal** | Assigned -> Responded -> Approved |
| **Auditing Company** | Shared -> Submitted -> Accepted |

A plain-language line summarizes where things stand (e.g. *"Waiting on Dr. Lee Mangold."* or *"Approved internally and ready to submit to Auditing Company."*). The internal team works the request exactly as they would any other Data Request -- collecting and approving a response -- and only once approved does **Submit to Auditor** become available to actually hand it to the firm; sharing alone (making it visible on the firm's Requests list) does not expose any collected evidence until this submit step happens.

Each request also carries two separate conversation threads:

- **Auditor messages** -- shared with the firm; visible on both sides
- **Comments** -- internal only; the audit firm never sees this thread

## The Auditor's Experience

Auditors sign in separately at `/auditor/login` -- there's no "continue with your account" bridge like other portals; it's password-only, followed by mandatory 2FA.

### Home

The landing page lists every **Engagement** the auditor is working, each as a card showing the audit name, an access-window badge (*"Your access ends [date]"*), audit type and date range, and a **View requests** link. Stat tiles per engagement: **Open**, **Submitted**, **Accepted**, **Returned**, **Population**, **Sample**. Below that, an engagement-wide **Messages about this engagement** thread lets the auditor ask the audited organization a question directly (Markdown supported, visible to both sides).

### Requests

Lists everything shared with the firm: Ref, Request, Control, Type, Status, Version, Last Activity, Due. Two header actions:

- **Raise a request** -- lets the auditor ask for something not already on the list
- **Download evidence bundle** -- exports collected evidence as a ZIP containing a `manifest.csv` (SHA-256 hash per file) and a `README.txt`, for offline review or archival; delivered via a time-limited link once the export finishes building (the auditor is emailed when it's ready)

Opening a request shows what was requested, a submission panel (*"Nothing has been submitted against this request yet"* until the internal team submits their response -- the auditor doesn't originate evidence on an existing request, only reviews and accepts or returns what comes back), and -- when the audit's sharing settings allow it -- the full **Control** text and **Implementation** details in side panels. A per-request **Messages** thread (tagged "Visible to the audited organization") sits alongside the submission panel.

### Documents

Where the firm delivers reports, management letters, and working papers via **Upload a document** -- doing so notifies the audit manager. Columns: Document, Type, Their review, Uploaded by, Size, Uploaded.

### Import IRL

Lets the firm bulk-upload their own Information Request List rather than raising requests one at a time. A 4-step wizard (Upload -> Map columns -> Review -> Import): upload a CSV or XLSX (up to 20MB / 2,000 rows), optionally enable **Update rows that are already here** (off by default -- when on, it refreshes title/description/due date on rows already present, but never touches statuses or anything already submitted), then **Read the file** to proceed to mapping. A collapsible reference shows how many control codes are in scope on the audit. Nothing is created until the final Import step is confirmed.

### Proposed Findings

Lets a **Lead Auditor** propose a finding via **Propose a finding**. Columns: Ref, Finding, Severity, Their decision, Proposed. A proposed finding *"stays out of the organization's register until they accept it"* -- it's a suggestion the internal team must act on, not a direct write to the audit's findings.

### Account

The avatar menu shows the auditor's name, a light/dark/system theme switcher, and **Sign out** -- there's no separate profile/password page visible here, a simpler menu than My Portal or the Vendor Portal.

## Configuration

### Email Templates

**Settings > Email Templates > Auditor Emails** provides six templates:

| Template | Sent To / When |
|----------|-----------------|
| **Auditor Invitation Email** | The auditor, when invited to an engagement -- carries the single-use link to set a password and enroll in 2FA |
| **Auditor Access Expiring -- Auditor** | The auditor, before their access window closes |
| **Auditor Access Expiring -- Audit Manager** | The internal audit manager, as a heads-up to extend access if the engagement is still running |
| **Auditor Access Revoked Email** | The auditor, when access is ended early |
| **Auditor Evidence Bundle Ready Email** | The auditor, when a requested evidence bundle export finishes building |
| **Auditor Submission Digest Email** | The auditor, on the configured Submission Digest Interval, listing which requests got new evidence since the last digest |

## Best Practices

- **Flag audit firms once, reuse them** -- Mark a vendor as an Audit Firm the first time you work with them so future engagements don't require re-tagging
- **Set sharing scope deliberately** -- Decide whether a firm needs full control text and implementation details, or just the request itself, before launching an engagement
- **Use Lead vs Staff Auditor roles intentionally** -- Only Lead Auditors can propose findings, so assign that role to whoever should be able to
- **Submit only what's approved internally** -- Let a request finish the internal Assigned -> Responded -> Approved track before submitting it to the auditor, so the firm never sees unreviewed evidence
- **Extend access before it expires, not after** -- Use the Warn Manager/Warn Auditor settings as your cue to extend an access window before the engagement stalls
- **Review the access log periodically** -- It's your audit trail of everything the firm has done; export it for your own records when an engagement closes

## Permissions

- Enabling and configuring the Auditor Portal requires Settings access
- Setting an Audit Firm on an audit, managing the Engagement page, and inviting/revoking auditors requires access to the audit
- Auditors themselves have no OpenGRC login or permissions -- their access is entirely scoped to the engagement(s) they've been invited to, through the separate `/auditor` portal

## Related Documentation

- [Audits](../foundations/audits.md) -- Audit types, Data Requests, and Information Request Lists
- [Vendor Risk Management (TPRM)](../features/vendor-management.md) -- Managing vendors, including audit firms
