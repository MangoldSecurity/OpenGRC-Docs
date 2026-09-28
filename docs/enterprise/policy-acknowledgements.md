# Policy Acknowledgements

!!! enterprise "Enterprise Feature"
    Policy Acknowledgement Campaigns are available exclusively in OpenGRC Enterprise. [Learn more about Enterprise](https://opengrc.com).

Policy Acknowledgement Campaigns let you formally distribute approved policies to your workforce -- and to external contacts -- and track who has read and signed off on them. A campaign can bundle multiple policies into a single "pack," run on a recurring cadence, automatically remind outstanding recipients, and re-issue acknowledgements when a signed policy's content changes. Recipients complete their acknowledgement in [My Portal](my-portal.md).

## Overview

Policy Acknowledgements support:

- Bundling one or more **Approved** policies into a single campaign
- Targeting internal users, departments, existing portal users, and ad-hoc external people by name and email
- Recurring cadences (Monthly, Quarterly, Semi-Annual, Annual) or manual, one-time launches
- Configurable due windows and multi-stage reminder schedules
- Automatic detection of policy drift, with controlled re-acknowledgement of changed policies
- A quick, single-policy "Send for acknowledgement" action directly from any policy record
- Dedicated invitation and reminder email templates

Internally, this feature is built on an "Attestation Campaign" data model -- you may see `attestation-campaigns` in URLs -- but every user-facing label reads "Acknowledgement Campaign" or "Policy Acknowledgement."

## Accessing Policy Acknowledgements

1. Navigate to **Entities > Policies** in the main navigation
2. Click **Acknowledgements** next to **New policy** at the top of the Policies list

This opens the **Policy Acknowledgements** page, which is not a tab within Policies but a separate management screen.

### Dashboard

The top of the page shows five stat tiles summarizing acknowledgement activity across all campaigns:

| Tile | Description |
|------|-------------|
| **Active campaigns** | Number of campaigns currently running |
| **Open rounds** | Number of in-progress acknowledgement rounds |
| **Outstanding** | Acknowledgements not yet signed across open rounds |
| **Overdue** | Outstanding acknowledgements past their due date |
| **Completion rate** | Percentage signed across open rounds |

Below the tiles, four tabs organize the page:

#### Campaigns

The list of all campaigns, with a search box, **Filter** (by Status and Frequency), and **Column manager**. Columns include:

| Column | Description |
|--------|-------------|
| **Campaign** | Campaign name and manager |
| **Status** | Draft, Active, Paused, Completed, or Archived |
| **Policies** | Number of policies in the pack |
| **Audience** | Resolved recipient count |
| **Frequency** | Recurrence cadence |
| **Next run** | When the next round will launch ("Manual" if Frequency is None) |
| **Last launched** | When the most recent round started |

Each row offers **Launch now** and an actions menu with **Duplicate** and **Archive**.

#### Rounds

Shows every round that has been launched, per campaign, with **Period**, **Status**, **Launched**, **Due**, **People**, and **Completion**, plus a separate **Open rounds** table showing progress on rounds still in flight. Opening a round shows a per-recipient table (Person, Policy, Status, Sent, Viewed, Acknowledged, whether it covers the current policy text, and the recipient's typed signature), plus round-level actions: **Resend to all outstanding**, **Export CSV**, **Attestation report (PDF)**, and **Close round**.

#### Outstanding

A per-person view of every unsigned acknowledgement across open rounds: **Person**, **Policy**, **Campaign**, **Status**, **Due**, **Days overdue**, and **Last reminder**. This is the working list for chasing down non-responders.

#### Changed

Flags campaigns whose included policies have been edited since people last signed them: **Campaign**, **Policies changed**, **Acknowledgements affected**, and **Re-acknowledgement**. Re-issuing asks only the affected people to re-sign the current text; their prior signatures are kept and marked superseded, not discarded.

## Creating a Campaign

Click **New campaign** from the Policy Acknowledgements page to open the four-step wizard.

### Step 1: Policies

| Field | Required | Description |
|-------|----------|-------------|
| **Campaign name** | Yes | Name of the campaign |
| **Description** | No | Internal description |
| **Policies** | Yes | Multi-select of policies to include in the pack |

Only policies in **Approved** status appear as options -- each person will sign every policy in the pack individually.

### Step 2: Audience

Audience is built from up to five combinable sources, resolved fresh at every launch (so new hires or updated department tags are automatically covered by the next round):

| Source | Type | Notes |
|--------|------|-------|
| **Every active internal user** | Toggle | Blanket switch covering all active internal users |
| **Departments** | Multi-select | Targets users tagged with the selected department terms |
| **Internal users** | Multi-select | Specific existing OpenGRC application users |
| **Portal users** | Multi-select | Existing external portal contacts (e.g. vendor contacts) |
| **Additional people (CSV)** | Free text | One `name,email` pair per line; people with no existing account get a portal identity automatically at launch |

This means a campaign can reach genuinely external people who have never logged into OpenGRC -- they're provisioned a portal identity the moment the campaign launches.

### Step 3: Schedule

| Field | Required | Default | Description |
|-------|----------|---------|-------------|
| **Campaign manager** | Yes | Current user | Owner responsible for the campaign |
| **Frequency** | Yes | -- | None, Monthly, Quarterly, Semi-Annual, or Annual |
| **Due within (days)** | Yes | 30 | Days from launch to the round's due date |
| **Reminder cap per person** | Yes | 3 | Maximum reminders sent to any one person per round |
| **Remind (days before due)** | No | 7, 1 | One or more day-offsets before the due date to trigger a reminder |
| **Note to recipients** | No | -- | Optional note shown in every invitation and reminder |
| **Re-acknowledge when a signed policy changes** | Toggle | On | If enabled, the Changed tab offers to re-issue affected acknowledgements when policy content is edited after signing; a manager must still confirm each re-issue |

If a new recurring round would open while the previous round is still unfinished, outstanding acknowledgements from the prior round are marked **Expired** and the new round starts clean.

### Step 4: Review

A read-only summary of the resolved audience -- e.g. "1 policy · 1 person" and a breakdown of internal users, portal users, people added by email, and duplicates merged across the audience sources. Click **Create** to save the campaign in **Draft** status. Creating a campaign does not launch it; launching is a separate, explicit action.

## Launching and Managing a Campaign

Open a campaign to see its detail view, organized into:

- **Campaign** -- name, status, manager, description, note to recipients
- **Schedule** -- frequency, next scheduled launch, last launched, due window, reminder behavior in plain English, and re-acknowledgement setting
- **Policies** -- the policies included (only Approved policies are ever sent; any others are named and excluded)
- **Audience** -- resolved recipient count

From the detail view you can:

- **Launch now** -- opens a new round and sends invitation emails immediately
- **Edit** -- change any wizard field
- **Duplicate** -- create a copy as a new draft
- **Archive** -- retire the campaign (there is no delete; Archive is the terminal action)

## How Recipients Sign

Every recipient signs in [My Portal](my-portal.md#policy-acknowledgements), regardless of whether they're an internal user or an external portal user -- there's no separate in-app signing form. The two audience types just reach it differently:

- **Internal users** get a to-do on their **To-Do & Approvals** page (Policy Acknowledgements tab), titled "Policies waiting for your acknowledgement." Its **Read & acknowledge** link bridges silently into My Portal under their existing session -- no separate login or emailed link involved.
- **External portal users** get the **Policy Acknowledgement Invitation Email** with a magic link that opens the same My Portal screen, authenticating into their own portal session.

In My Portal, the recipient reads each policy in the pack (via a **Read policy** button that opens the full text in a modal) and, per policy, checks *"I have read and understood [Policy Name] and agree to comply with it"* and types their full name to sign. This produces a permanent, timestamped record -- sent, viewed, and acknowledged times plus the typed signature -- visible on the round's recipient table, and is what backs the **Attestation report (PDF)** export.

## Sending a One-Off Acknowledgement

To send a single policy for acknowledgement without building a full campaign:

1. From the Policies list, use the **Send for acknowledgement** row action, or open a policy and click **Send for acknowledgement** in its header
2. In the **Send "<Policy Name>" for acknowledgement"** modal, choose the audience using the same fields as the campaign wizard (Every active internal user, Departments, Internal users, Portal users, Additional people)
3. Set **Due within (days)**, **Repeat** (None/Monthly/Quarterly/Semi-Annual/Annual), and an optional **Note to recipients**
4. Review the live **Recipient summary** showing how many acknowledgements will be created
5. Click **Send**

This creates and immediately launches a lightweight, single-policy campaign -- there is no separate draft/review stage.

## Configuration

### Default Acknowledgement Window

**Settings > Policies > Acknowledgements** sets **Default days to acknowledge** -- the default due window used by both the one-off "Send for acknowledgement" action and new campaigns. Individual campaigns can override this default.

### Email Templates

**Settings > Email Templates > Policy Acknowledgement Emails** provides two templates:

| Template | Sent When |
|----------|-----------|
| **Policy Acknowledgement Invitation Email** | A round launches -- one email per person covering the entire policy pack |
| **Policy Acknowledgement Reminder Email** | On the campaign's reminder schedule, or on manual resend, to anyone who hasn't yet acknowledged every policy in the round |

**Available Variables:**

| Variable | Description |
|----------|--------------|
| `{{ $campaignName }}` | Campaign name |
| `{{ $policyCount }}` | Number of policies in the pack |
| `{{ $dueDate }}` | Round due date |
| `{{ $name }}` | Recipient's name |
| `{!! $policyList !!}` | List of policies in the pack |
| `{!! $senderNote !!}` | The campaign's "Note to recipients" |

Each template supports **Reset to default** and **Send test to me** before saving.

## Permissions

Managing campaigns is permission-gated separately from viewing who has signed:

| Permission | Description |
|------------|--------------|
| **List AttestationCampaigns** | View the campaign list and dashboard |
| **Create AttestationCampaigns** | Create new campaigns |
| **Read AttestationCampaigns** | View campaign details |
| **Update AttestationCampaigns** | Edit, launch, duplicate, or archive campaigns |
| **Delete AttestationCampaigns** | Remove campaigns |
| **Read Attestations** | View individual signed acknowledgement records |

Signed acknowledgement records (Attestations) are read-only everywhere -- they are created automatically when a recipient signs in My Portal and cannot be manually created, edited, or deleted.

## Best Practices

- **Bundle related policies** -- Group policies that are typically reviewed together into one campaign so recipients sign them in a single sitting
- **Only approve before sending** -- Move a policy to Approved status before including it in a campaign; drafts and policies under review can't be selected
- **Set a realistic due window** -- Balance urgency against giving recipients enough time to actually read the policy pack
- **Use recurring frequency for standing policies** -- Annual or Semi-Annual cadences keep long-lived policies like an Acceptable Use Policy continuously attested without manual relaunching
- **Review the Changed tab after policy edits** -- Re-issue affected acknowledgements promptly so signed records stay current with policy content
- **Monitor the Outstanding tab** -- Use it as your working list for following up with non-responders before they go overdue

## Related Documentation

- [Policies](../features/policies.md) -- Managing the policy documents that campaigns distribute
- [My Portal](my-portal.md) -- Where recipients read and sign their acknowledgements
