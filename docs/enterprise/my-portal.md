# My Portal

!!! enterprise "Enterprise Feature"
    My Portal is available exclusively in OpenGRC Enterprise. [Learn more about Enterprise](https://opengrc.com).

My Portal is a lightweight, self-service workspace where people complete tasks assigned to them from OpenGRC -- signing policy acknowledgements, proposing updates to a record, or responding to an access review step -- without needing the full admin application. It uses the same underlying interface as the main app, but with a deliberately reduced navigation shell built around a single to-do inbox.

!!! note "How internal staff reach My Portal differs by task type"
    Policy Acknowledgements are always completed in My Portal, even for internal staff: an internal recipient gets a to-do on the main app's **To-Do & Approvals** page, but its "Read & acknowledge" link is a silent bridge straight into My Portal under their existing session -- there is no separate admin-side signing form. Record Update Requests and Access Review steps work differently: when assigned to an **internal user**, they stay entirely within the admin app's To-Do & Approvals page and never touch My Portal at all; only assigning them to a **Portal User** routes the task through My Portal via an emailed magic link. Request Exception is available to anyone signed in, regardless of path.

## Overview

My Portal provides:

- **My Assignments** -- a personal to-do inbox of items awaiting a portal user's action: policy acknowledgements, record update requests, and access review steps
- **Request Exception** -- a self-service form for requesting a deviation from a policy
- A simplified profile page for managing name, email, password, and display theme
- Two sign-in paths: a direct portal login for external/portal-only users, and a bridge login for staff who already have an OpenGRC account

## Accessing My Portal

My Portal is reached at `/my` on your OpenGRC instance (e.g. `https://yourcompany.opengrc.net/my`). The sign-in page offers two options:

| Option | Who it's for |
|--------|--------------|
| **Email address / Password** | Portal-only users with no admin account -- typically external contacts added to a campaign via CSV or as Portal Users |
| **Continue with your OpenGRC account** | Staff who already have a login to the main application |

Staff using **Continue with your OpenGRC account** authenticate through the main app's login and are then bridged into the portal under the same session -- there is no separate password. Because the session is shared, a staff member can navigate directly to the main app's `/app` URL at any time to return to the admin interface; My Portal itself does not include a link back.

## My Assignments

The portal's home page (`/my`) and only default sidebar item. It lists items awaiting the signed-in person's action -- for example, a policy acknowledgement invitation from a launched campaign. When nothing is pending, it displays an empty "Nothing needs your attention right now" state.

### Policy Acknowledgements

Opening an assigned acknowledgement (whether from the My Assignments card, an emailed magic link, or the "Read & acknowledge" link on an internal user's admin To-Do page) lands on the campaign's acknowledgement screen, showing the due date, a progress counter ("X of N acknowledged"), and one card per policy in the pack. Each card has a **Read policy** button that opens the full policy text -- metadata (Policy ID, Effective Date, Owner, Purpose, Scope) followed by the complete body -- in a modal.

After closing the modal, the card reveals a checkbox ("I have read and understood *[Policy Name]* and agree to comply with it"), a **Type your full name to sign** field, and an **Acknowledge** button. Submitting shows a "Thank you!" confirmation and requires no further action. The signature, along with sent/viewed/acknowledged timestamps, is written to a permanent record on the campaign's Rounds tab back in the admin app -- visible there with **Resend to all outstanding**, **Export CSV**, and **Attestation report (PDF)** actions, and flagged if the policy text later changes after signing.

### Record Update Requests

Assets, [Controls](../foundations/controls.md#approvals-and-delegation), Implementations, and Risks each have a **Request Update** action on their detail page that asks someone to review the record and propose corrections -- it's a general "please review this record" request, with no way to scope it to specific fields or attach a note. When assigned to a **Portal User**, the assignment appears in that person's My Assignments as a card showing the record type, name, status, and the link's expiration date, with a **Start** button.

Clicking **Start** opens a full review form pre-populated with the record's current values with the guidance: *"Review the information below and update anything that is incorrect or missing. Changes you propose will be reviewed before taking effect."* Edits save automatically as a draft, so the reviewer can leave and come back later, and **Submit for review** sends the proposed changes back for an internal reviewer to accept or reject -- the portal user never writes directly to the record.

### Access Review Responses

When a [User Access Review](access-reviews.md) System Owner or Application Owner is a Portal User rather than an internal OpenGRC user, their review step (assembling the access package, or attesting that access is correct) also arrives as a My Portal assignment rather than an internal to-do, using the same magic-link pattern as everything else in the portal.

## Request Exception

Reached via **Request Exception** in the sidebar (`/my/request-exception`). Lets a person ask for a documented deviation from a policy rather than simply not complying with it.

| Field | Required | Description |
|-------|----------|--------------|
| **Policy** | Yes | The policy the exception applies to |
| **Exception title** | Yes | A short name for the request |
| **Description** | No | What is being requested |
| **Business justification** | Yes | Why the exception is necessary |
| **Risk assessment** | No | Risks introduced by granting the exception |
| **Compensating controls** | No | Mitigations in place to offset the risk |
| **Requested date** | -- | Defaults to today |

Submitting sends the request for review through **Submit for review**.

## Profile

The user menu (avatar, top right) offers:

- **Profile** -- edit **Name**, **Email address**, and set a **New password**
- **Theme** -- switch between light, dark, or system theme
- **Sign out**

## Relationship to the Vendor Portal

My Portal is a general-purpose task portal and is distinct from the dedicated [Vendor Portal](../settings/vendor-portal.md), which is scoped specifically to vendor risk assessments, document uploads, and vendor survey completion. A "Portal user" targeted by a Policy Acknowledgement campaign signs in through My Portal, even if that same person is also a vendor contact elsewhere in the system.

## Permissions

My Portal access is governed by how a person is added as a recipient rather than a standalone role:

- **Portal users** and people added by email to a campaign or one-off acknowledgement sign in with a portal-only account (email/password) and see only what has been assigned to them
- **Internal/staff users** access the portal via **Continue with your OpenGRC account**, using their existing OpenGRC permissions for the main application

## Best Practices

- **Use CSV entry sparingly** -- Reserve the "Additional people" CSV field for genuinely one-off external recipients; add recurring contacts as Portal Users instead so they aren't re-entered on every campaign
- **Point recipients to My Portal, not the main app** -- Invitation and reminder emails link directly into the portal; recipients without admin access should never need `/app` URLs
- **Keep exception requests flowing to a reviewer** -- Make sure a manager or policy owner is monitoring submitted exception requests, since My Portal itself has no built-in approval workflow view for the requester

## Related Documentation

- [Policy Acknowledgements](policy-acknowledgements.md) -- Creating and managing the campaigns that populate My Assignments
- [Access Reviews](access-reviews.md) -- Configuring UAR campaigns and assigning Portal User reviewers
- [Vendor Risk Management (TPRM)](../features/vendor-management.md) -- The vendor-specific portal experience
