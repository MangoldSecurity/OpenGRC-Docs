# Controls

Controls are the practical mechanisms -- policies, procedures, and technical safeguards -- that satisfy the requirements defined by a [Standard](key-terms.md#standards). Every control belongs to a standard, and its detail page is where you connect that requirement to real-world evidence: implementations, policies, and audit results.

For the underlying concepts (what a control is, and the meaning of Control Type, Category, and Enforcement), see [Key Terms](key-terms.md#controls).

## Overview

The Controls list (**Foundations > Controls**) shows every control across all standards, with columns for Code, Title, Standard, Type, Category, Enforcement, Effectiveness, Applicability, Status, Last Assessed, Assessment Frequency, Next Assessment Due, Owner, Department, and Scope. From here you can:

- Search and filter controls
- Export the list with **Export Controls**
- Create a control directly with **New Control**

## The Control Detail Page

Opening a control shows a header with its code, parent standard, and title, followed by a summary row:

| Field | Description |
|-------|-------------|
| **Effectiveness** | How well the control is operating, based on the latest audit or manual entry |
| **Status** | The control's lifecycle status: Draft, Active, or Retired |
| **Applicability** | Whether the control applies to the organization, and what set that determination (e.g. "set by Audit") |
| **Next Assessment** | When the control is next due for reassessment, based on its Assessment Frequency |
| **Last Assessed** | The date of the most recent assessment |
| **Owner** | The internal user accountable for the control |

Below the summary row, four tabs organize the control's details:

### Overview

- **Description** -- what the control requires
- **Discussion** -- optional context from the standard to help with implementation
- **Test Plan** -- optional guidance describing how an auditor should verify the control
- **Classification** -- Type, Category, Enforcement, and Violation Risk Factor
- **Ownership** -- Control Owner, Department, Scope, and Tags
- **Assessment** -- Frequency, Last completed date, and Next due date

### Implementations

Lists the implementations mapped to this control, with their code, title, status, effectiveness, and last audit date. Use **New implementation** to document a new implementation directly against this control, or **Add Existing Implementation** to map one already in your library.

### Audit History

Every audit item that has assessed this control, showing the audit name, effectiveness rating, date assessed, and auditor notes. Click **View Audit Item** to see the full assessment.

### Policies

Policies related to this control. Use **Relate to Policy** to attach an existing policy, or **Detach** to remove an association.

## Creating and Editing a Control

A control requires:

- **Code** -- a unique identifier used to reference the control throughout the system
- **Title**
- **Description** -- what the control requires, in detail
- **Standard** -- the parent standard this control belongs to

Optional fields let you add more detail:

- **Discussion** -- context from the standard to help someone determine how to implement it
- **Test Plan** -- how an auditor should verify the control
- **Type**, **Category**, **Enforcement** -- classification (see [Key Terms](key-terms.md#controls))
- **Violation Risk** -- the risk associated with a violation of this control (High, Medium, or Low)
- **Family**, **Subcategory**, **Assurance Level** -- for frameworks with native groupings that don't map cleanly to Type or Category (e.g. an ASVS chapter, a NIST CSF function, or an OWASP SAMM maturity tier)
- **Control Owner**, **Department**, **Scope**, **Tags**
- **Assessment Frequency** -- how often the control must be reassessed; the next due date is calculated from the last completed assessment

!!! note "Retired controls"
    Setting a control's **Status** to Retired excludes it from AI analysis and assessments.

## Approvals and Delegation

From a control's detail page:

- **Submit for Approval** starts the approval chain for the control record
- **Request Update** generates a secure link so someone else can update the control without needing full OpenGRC access. Assign it to an **External portal user** or an **Internal user**, and optionally configure a **Link expiration**, make it **Single use**, or leave it **Resumable** so progress is saved as a draft between visits

## AI Assistant

!!! enterprise "Enterprise Feature"
    OpenGRC Enterprise adds an **AI Assistant** to every control, offering implementation suggestions and assessing whether your mapped implementations meet the control's requirements. [Learn more](../enterprise/ai-controls-assistant.md).

## Best Practices

- **Assign an owner to every control** so there's clear accountability for keeping it current
- **Set an Assessment Frequency** on controls that need regular reassessment, rather than relying on ad hoc audits
- **Write a Test Plan** for controls you expect to be audited, so auditors know exactly what evidence to look for
- **Use Family/Subcategory/Assurance Level** when importing frameworks with their own native structure that doesn't map to Type or Category
- **Retire controls you no longer track** instead of deleting them, to preserve audit history while excluding them from active analysis
