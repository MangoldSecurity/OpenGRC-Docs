# Access Reviews

!!! enterprise "Enterprise Feature"
    Access Reviews are available exclusively in OpenGRC Enterprise, currently in Beta. [Learn more about Enterprise](https://opengrc.com).

Access Reviews (User Access Reviews, or UAR) let organizations periodically verify who has access to which applications, and produce the audit evidence to prove it. A campaign creates recurring or one-off review rounds; each round walks every application in scope through a three-step process and finishes with a manager sign-off that becomes the audit record.

## Overview

Access Reviews help organizations:

- Run recurring or one-off access review campaigns across applications
- Walk each application through a structured three-step process: package, verification, manager decision
- Notify each participant automatically with customizable email templates
- Snapshot owners, instructions, and reference files at launch so a closed round's evidence never shifts
- Track open, overdue, and completed items from a single dashboard
- See which applications haven't been reviewed recently

## How It Works

### The Three-Step Review Process

Each review item (one per application, per round) moves through up to three steps:

| Step | Role | Responsibility |
|------|------|-----------------|
| **1. Review Package** *(optional)* | System Owner -- the technical administrator who can export the application's user list | Exports the current user list and describes how it was produced. Applications without an evidence requirement skip straight to verification |
| **2. Verification** | Application Owner -- the business owner accountable for who should have access | Checks the list and attests that access is correct, or spells out the changes required |
| **3. Manager Decision** | UAR Manager -- the person running the campaign | Approves and closes the item, parks it while changes are worked out, or restarts the review |

When every item in a round is decided, the UAR Manager finalizes the round with their sign-off -- that record is the audit evidence.

### Creating a Campaign

1. Navigate to **Access Reviews** and click **New Campaign**
2. Under **Campaign**, set the **Name**, **UAR Manager**, optional **Description**, **Status** (Active or Paused), and **Due within (days)** -- how long reviewers get after a round launches
3. Under **Schedule**, choose a **Frequency** (None, Monthly, Quarterly, Semi-Annual, or Annual) and optionally a **Next run** date to launch automatically; leave it empty to launch rounds manually
4. Under **Review Package**, choose whether the **System Owner prepares the package first** (the full three-step flow) or to **go straight to the Application Owner** (when the verifier already has the access data), set **Default instructions to the System Owner**, and choose whether **Verifier evidence** is Optional or Always required
5. Under **Reference Materials**, upload files reviewers keep asking for (an employee roster, a recent leavers list, a role matrix) and choose which step sees each one. Files are snapshotted per round, so a later replacement only affects future rounds
6. Under **Scope**, either leave **Review all active applications** on, or turn it off and pick specific applications or assets flagged for access review
7. Review the **What This Campaign Will Do** summary -- it shows how many review items the next round will create, when reviewers will see it's due, and (if a frequency is set) the schedule of upcoming rounds -- then click **Create**

### Launching a Round

Clicking **Launch UAR** opens a **Launch [date] Round** screen before anything is sent, so you can review and adjust the round first:

- Three status chips summarize the round: **Ready to launch** (applications with both owners resolved), **Package step skipped** (applications with no System Owner set, so the Review Package step is skipped for that item), and **External reviewers** (owners who are portal users, which will get a magic link by email instead of an in-app notification)
- A **Review targets in scope** table lists each application with its **System Owner** and **Owner** (verifier) -- adjust either assignment here, or add another reviewer with **+**. A per-application **Package step** toggle lets you override the campaign's default for that one application
- An **Email participants** toggle controls whether each assignee is emailed their step request. When off, internal users still see their work on the **To-Do** page

Click **Launch N Review Items** to start the round.

!!! note "Portal Users as reviewers"
    A System Owner or Application Owner can be a **Portal User** rather than a full internal OpenGRC user. Portal User reviewers complete their step via a magic link emailed into [My Portal](my-portal.md#access-review-responses), the same pattern used elsewhere for external reviewers (e.g. vendor surveys). Internal reviewers instead see their step on the **To-Do** page, as noted below.

### Running a Round

Once launched, the campaign page shows:

- A round selector for viewing past rounds
- Stage counts across the round: Package, Attestation, Manager, Closed
- A table of review items with Review Target, Type, a progress stepper, who the item is **Waiting On**, Status, Resolution, and Due date

Each review item has its own detail page showing a full **Item History** timeline (round launched, package submitted, attestation recorded, decision made), the **Review Package** details (source system, data-as-of date, how the list was produced, System Owner, and any attached files), and the verifier's **Attestation** once submitted.

#### Item Statuses

| Status | Meaning |
|--------|---------|
| **Awaiting Review Package** | Waiting on the System Owner to assemble the package |
| **Awaiting Validation** | Waiting on the Application Owner to verify access |
| **Awaiting Manager Review** | Waiting on the UAR Manager's decision |
| **Waiting on Changes** | Parked while reported changes are worked |
| **Closed** | Decided -- Resolution shows the outcome (e.g. Approved) |

### Finalizing a Round

Once every item in a round is decided, click **Finalize Round** to record the UAR Manager's sign-off -- this is the record you present as audit evidence. Use **Export Round** to download the round's evidence package.

### Email Templates

Click **Email templates** from the Access Reviews page or a campaign to customize the three notification emails, one per step:

| Template | Sent to |
|----------|---------|
| **Evidence Request** | System Owner, at the Review Package step |
| **Validation Request** | Application Owner, at the Verification step |
| **Manager Review** | UAR Manager, at the Manager Decision step |

Each template has a Subject, optional Preheader, and a Markdown Body built from placeholders such as `{{recipient_name}}`, `{{application_name}}`, `{{campaign_name}}`, `{{due_date}}`, `{{review_procedure}}`, `{{organization_name}}`, and the required `{{action_url}}` -- the link recipients use to complete their step. Use **Preview** or **Send test to me** before saving, or **Reset to default** to revert.

## Dashboard

The Access Reviews home page shows:

- **Open Items**, **Overdue**, **Waiting On You**, and **Closed This Round** counts
- **Where the Current Round Stands** -- a breakdown of items by stage (Package, Attestation, Manager Review, Closed) with percent closed
- A list of **access review campaigns** with each one's latest round progress
- **Needs Your Attention** -- items that are overdue or blocked
- **Review Coverage** -- how many applications have been reviewed at least once in the last 12 months, surfacing applications with no recent review

## Best Practices

- **Set a recurring Frequency** for applications that need regular review cadences instead of launching rounds manually
- **Skip the Review Package step** for low-risk applications where the verifier already has the access data, to speed up the round
- **Require verifier evidence** for high-risk or regulated applications, and keep it optional elsewhere
- **Keep reference materials current** -- an outdated leavers list undermines the verifier's ability to attest accurately
- **Finalize every round promptly** once all items are decided -- the sign-off is what makes the round usable as audit evidence
- **Watch Review Coverage** to catch applications that haven't been reviewed in the last year and add them to a campaign

## Permissions

- Creating and managing campaigns requires access to the Access Reviews app
- System Owners and Application Owners complete their step via the secure link in their notification email
- Only the UAR Manager assigned to a campaign can make Manager Decisions and finalize a round

## Related Documentation

- [My Portal](my-portal.md) -- Where Portal User reviewers complete their step
