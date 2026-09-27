# Implementations

Implementations are the actual deployment and operation of a security control -- the specific tools, configurations, processes, and procedures used to put a control into practice. While a control might require access reviews, an implementation documents exactly how: which tool is used, who conducts the reviews, how often, and what evidence is kept. Implementations bridge the gap between a control's requirement and its practical application.

For the underlying concept, see [Key Terms](key-terms.md#implementations).

## Overview

The Implementations list (**Foundations > Implementations**) shows every implementation with its Code, Title, Effectiveness, Last Audit date, Status, Critical flag, Assessment Frequency, Next Assessment Due, Owner, Department, and Scope. From here you can:

- Search and filter implementations
- Export the list with **Export implementations**
- Create one with **Create Implementation**

## The Implementation Detail Page

Opening an implementation shows a header with its code and title, followed by a summary row:

| Field | Description |
|-------|-------------|
| **Effectiveness** | How well the implementation is operating, based on the latest audit |
| **Status** | The implementation's lifecycle status (see below) |
| **Next Assessment** | When the implementation is next due for reassessment |
| **Last Assessed** | The date of the most recent assessment |
| **Owner** | The internal user accountable for the implementation |

Below the summary row, tabs organize how the implementation connects to the rest of your GRC data:

### Overview

- **Details** -- what is in place and how it works
- **Test Procedure** -- optional guidance on how to verify the implementation is operating
- **Notes** -- internal notes, not shown to auditors
- **Satisfies Controls** -- the controls this implementation maps to
- **Ownership** -- Owner, Frequency, Department, and Scope
- **Linked Resources** -- a quick summary of related Applications, Vendors, Assets, and Risks, each linking to its full tab

### Controls, Risks, Assets, Applications, Vendors, and Policies

Each of these appears as its own tab, listing the related records and, for Risks, showing Inherent and Residual risk scores. Every tab has a **Relate to [Entity]** button to attach an existing record, and a **Detach** action to remove the association -- so an implementation can be the connective tissue between a control, the risk it mitigates, the vendor or application it protects, the asset it runs on, and the policy that governs it.

### Audit History

Every audit item that has assessed this implementation, with the audit name, effectiveness rating, date, and auditor notes.

## Creating and Editing an Implementation

An implementation requires:

- **Code** -- a unique identifier
- **Title**
- **Details** -- what is in place and how it works

Optional fields:

- **Test Procedure** -- how to verify it's operating
- **Notes** -- internal only, not shown to auditors
- **Implementation Status** -- see below
- **Critical Implementation** -- a toggle that's auto-flagged when the implementation is mapped to enough controls, standards, or programs, but can also be set manually
- **Related Controls**, **Related Applications**, **Related Vendors** -- these three relationships can be set directly from the edit form; Risks, Assets, and Policies are managed from their own tabs on the view page instead
- **Owner**, **Assessment Frequency**, **Department**, **Scope**, **Tags**

### Implementation Status

| Status | Description |
|--------|-------------|
| **Implemented** | Fully in place |
| **Partially Implemented** | Partially in place, with gaps |
| **Not Implemented** | Not yet in place |
| **Unknown** | Status hasn't been determined |
| **Retired** | No longer in use |

## Approvals and Delegation

From an implementation's detail page:

- **Submit for Approval** starts the approval chain for the implementation record
- **Request Update** generates a secure link so someone else can update the implementation without full OpenGRC access, the same way it works for [controls](controls.md#approvals-and-delegation)

## Best Practices

- **Write enough detail that an auditor doesn't need to ask follow-up questions** -- name the specific tool, process, and frequency, not just "access is reviewed"
- **Fill in the Test Procedure** for implementations you expect to be audited, so reviewers know exactly what to check
- **Map one implementation to multiple controls** when it genuinely satisfies more than one requirement, rather than duplicating it
- **Use Related Risks to show risk mitigation** -- linking an implementation to the risks it addresses makes your risk register's residual scores easier to justify
- **Keep Notes for internal context** (like known limitations or planned improvements) separate from Details, since Notes are never shown to auditors
