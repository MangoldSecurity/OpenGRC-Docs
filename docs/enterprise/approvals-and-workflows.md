# Approvals and Workflows

!!! enterprise "Enterprise Feature"
    Approvals and Workflows are available exclusively in OpenGRC Enterprise. [Learn more about Enterprise](https://opengrc.com).

OpenGRC Enterprise ties sign-off and automation together across the platform through two separate systems: **Approval Workflows**, which require one or more people to approve a change before it takes effect, and **Workflows**, an if-this-then-that automation engine triggered by record events or schedules. Policies add a third layer on top -- Change Control settings that govern when editing a policy requires approval.

## Overview

Approvals and Workflows help organizations:

- Require sign-off before changes to Controls, Implementations, Risks, Assets, Policies, Policy Exceptions, or Meeting Minutes take effect
- Build multi-stage approval chains, where each stage is satisfied by anyone holding a given role, a specific pinned approver, or a person tied to the record itself (like its owner)
- Automatically route externally-submitted changes (via [Request Update](../foundations/controls.md#approvals-and-delegation) links) through an approval chain before they're written to the record
- Require approval to edit an already-Approved policy, and lock terminal-status policies from casual edits
- Build independent automation -- notifications, reminders, record updates, webhooks -- triggered by record events or on a schedule, with no approval involved

## Approval Workflows

Approval Workflows are managed under **Settings > Approval Workflows**. The list shows each chain's Name, what it **Applies to**, its number of **Stages**, how it **Starts**, and whether it's **Active**.

OpenGRC ships with one approval chain per governed record type:

| Workflow | Applies to | Purpose |
|----------|-----------|---------|
| **Asset Change Review** | Asset | Reviews portal-proposed asset changes before they're written to the record |
| **Implementation Change Review** | Implementation | Reviews portal-proposed changes before they're written to the record |
| **Control Change Review** | Control | Reviews portal-proposed changes before they're written to the record |
| **Risk Change Review** | Risk | Reviews portal-proposed changes before they're written to the record |
| **Policy Approval Workflow** | Policy | Reviews policy changes -- see [Policy-Specific Approval Behavior](#policy-specific-approval-behavior) below |
| **Policy Exception Request** | Policy Exception | Reviews requested exceptions to a policy |
| **Meeting Minutes Approval** | Meeting | Routes submitted meeting minutes to the governing body chair for sign-off; approval locks the minutes, rejection returns them to draft with the comment |

Each of the four "Change Review" chains above only takes effect once **activated** -- doing so routes [Request Update](../foundations/controls.md#approvals-and-delegation) submissions (from a portal user or an internal user completing a delegated update) through the chain before the change is written to the record.

### Creating and Editing an Approval Workflow

**Definition** -- what the chain governs and when it starts:

- **Name** and **Description**
- **Applies to** -- the record type this chain governs: Asset, Policy Exception, Policy, Implementation, Control, Risk, or Assessment
- **Document types** *(Policy only)* -- which policy-module document types this chain governs (Policy, Procedure, Standard, Guide, Handbook, Other). Leave empty to govern all of them; types not covered by any active workflow save directly, without approval
- **Starts** -- **Manually** (only from explicit submission actions like Submit for Approval or a completed Request Update), **When a record is created**, or **When a record is updated**

**Behavior**:

- **Require a typed signature on approval** -- a toggle requiring approvers to type their name to confirm
- **When a stage rejects** -- **Reject the request** outright, or **Return to prior stage** for another attempt
- **Active** -- whether the chain is currently in effect

**Stages** -- sign-off happens in the order stages are listed. Each stage is decided by any one of:

- **Eligible roles** -- any user holding one of the listed roles
- **Or a pinned approver** -- one specific user
- **Or a person on the record** -- a role resolved dynamically from the record under review (e.g. its Control Owner or Policy Owner)

Click **Add stage** to require multiple sequential approvals (e.g. a technical reviewer followed by a manager).

## Policy-Specific Approval Behavior

Policies have their own approval configuration under **Settings > Policies**, in addition to the Policy Approval Workflow described above:

- **Require approval to edit an Approved policy** -- when on, edits to an Approved policy are staged as a change request and only applied once the approval chain approves them; the published policy stays in force, unchanged, while the change is reviewed. Only the **Policy** document type is covered by default -- Procedure, Standard, Guide, Handbook, and Other document types save directly unless added to the Policy Approval Workflow's Document types
- **Lock Archived, Superseded, and Retired policies** -- when on, policies in a terminal status can't be edited until explicitly reactivated (returned to In Review) with the **Reactivate** action

In the default **Policy Approval Workflow**, the only stage is **Owner Approval**, resolved to the policy's **Policy Owner**. Because it's a single-stage chain, once the owner approves a submitted change it goes straight to Approved -- there's no further review.

## Workflows (Automation)

Workflows are managed under **Settings > Workflows** and provide if-this-then-that automation -- timed or triggered by record events -- independent of the approval system. The list page shows Active workflows, Runs today, Success rate, and how many Need attention, alongside each workflow's Trigger, Actions count, Status, and Last run.

### Creating and Editing a Workflow

**Details** -- Name, **Status** (Draft, Active, or Paused), and Description.

**When this happens** -- the trigger:

- **Trigger type** -- **Record event**, **Schedule**, or **Survey answer** (coming soon)
- For a **Record event**: choose the **Object** (record type), which record events to fire on (**Created**, **Updated**, **Deleted**), and optionally narrow to **Only when field** [Operator] [Value] -- e.g. "Status Id" "changed to" "Approved". Operators include is, is not, changed, changed to, changed from, is empty, and is not empty
- For a **Schedule**: an optional **Object to check** (evaluates the conditions against every record of that type on each run and acts on each match; leave empty for a single run not tied to any record), **Act on matches** (one run per matching record, or a single run covering all matches), **Frequency** (hourly/daily/weekly/monthly/quarterly), time of day, and **Timezone**
- Available merge tokens (e.g. `{{policy.name}}`, `{{vendor.risk_rating}}`, `{{run.date}}`) are listed based on the object chosen, for use in action text fields

**Only continue if** -- optional additional filter conditions (Match **All** or **Any**), for narrowing beyond the trigger itself. Date fields support additional operators like "is within (days)", "is before", and "is after".

**Then do this** -- one or more actions, run in order:

| Action | Description |
|--------|-------------|
| **Create record** / **Update record** / **Delete record** | Manipulate a record directly |
| **Create task** | Add a task |
| **Notify** | In-app notification to one or more users |
| **Send email** | Email to users, "All staff", a dynamic field (e.g. the record owner), or arbitrary addresses |
| **Call webhook** | HTTP request (GET/POST/PUT/PATCH/DELETE) with a JSON payload -- e.g. posting to Slack |
| **Wait / delay** | Pause before continuing to the next action |
| **Send survey** | Launch a survey |
| **Open audit** / **Start audit** | Create or launch an audit |
| **Request evidence** | Create a data request |

Use **Test** on an existing workflow to run it manually, and **Runs** to see its execution history.

### Example Workflows

| Workflow | Trigger | What it does |
|----------|---------|---------------|
| Policy published → notify & sync | Policy updated, when Status changed to Approved | Emails staff, posts to Slack, creates a re-review task |
| Vendor risk escalated to Critical → alert owner | Vendor updated, when Risk Rating changed to Critical | Notifies and emails the vendor owner |
| Critical/High-risk vendor assessment due → alert owner | Daily schedule, per vendor matched | Reminds the owner when a vendor's next assessment is within 30 days |
| Recurring assessments → open quarterly audit | Quarterly schedule, all matching controls together | Opens a single audit covering every control due for reassessment, starts it, and requests evidence from each owner |

## Workflows vs. Approval Workflows

| | Workflows | Approval Workflows |
|---|---|---|
| **Purpose** | Automation: notify, update records, call webhooks | Require human sign-off before a change takes effect |
| **Triggered by** | Record events or a schedule | Submission actions (Submit for Approval, or a completed Request Update) |
| **Configured under** | Settings > Workflows | Settings > Approval Workflows |

The two systems don't call into each other -- a Workflow has no "start an approval chain" action, and an Approval Workflow can't be triggered by a schedule.

## Best Practices

- **Use Approval Workflows** for anything that needs a documented human sign-off before it takes effect; use **Workflows** for notifications, reminders, and system-to-system automation
- **Give each stage a fallback role**, not just a pinned approver, so the chain isn't blocked if one person is unavailable
- **Turn on "Require approval to edit an Approved policy"** for policies subject to external audit, so every change is reviewed and documented before it takes effect
- **Add a second stage** to sensitive approval chains (e.g. a manager after an owner) rather than relying on single-person sign-off
- **Test new Workflows** with the **Test** button before switching their Status to Active

## Permissions

- Configuring Approval Workflows and Workflows requires Settings/admin access
- Only users matching a stage's eligible roles, its pinned approver, or the record-tied person can act on that stage
