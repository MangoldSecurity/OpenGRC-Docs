# Standards

Standards define the "what" of security and compliance -- the requirements, guidelines, or best practices your organization measures itself against. A standard can come from a regulatory body (HIPAA, GDPR), an industry framework (ISO 27001, NIST), or an internal policy. Standards are the foundation for [Controls](controls.md), which implement their requirements in practical ways.

For the underlying concept, see [Key Terms](key-terms.md#standards).

## Overview

The Standards list (**Foundations > Standards**) shows every standard with its Code, Name, Description, Issuing Authority, and Status. From here you can:

- Search the list
- Export the list with **Export Standards**
- Create a standard with **New Standard**
- Use the row **Actions** menu to toggle a standard's scope, edit it, or delete it

## The Standard Detail Page

Opening a standard shows its details -- Name, Code, Authority, Status, Department, Scope, and Description -- along with two tabs:

- **Controls** -- every control that belongs to this standard. Use **Add New Control** to create one directly against the standard
- **Audits** -- the audit history for this standard

## Creating and Editing a Standard

A standard requires:

- **Name**
- **Code** -- a unique ID for the standard
- **Authority** -- the organization that maintains the standard
- **Status** -- see below
- **Description** -- the purpose and scope of the standard

Optional fields include **Department**, **Scope**, **Reference URL** (a link to the official standard document), and **Tags**.

### Standard Status

| Status | Description |
|--------|-------------|
| **Draft** | The standard is being set up and not yet in active use |
| **In Scope** | The standard applies to your organization and its controls are actively tracked |
| **Not In Scope** | The standard doesn't currently apply, but is kept for reference |

You can toggle a standard between In Scope and Not In Scope directly from the **Actions** menu on the Standards list, without opening the full edit form.

## Importing Controls in Bulk

Rather than adding controls to a standard one at a time, you can bulk-import an entire framework's controls via CSV. See [Importing Data](../data-manager/import.md) for the full import workflow.

## Best Practices

- **Set Status accurately** -- keep standards you don't currently need to comply with as Not In Scope rather than deleting them, so you can reactivate them later without re-importing
- **Use a Reference URL** -- link to the official standard text so anyone reviewing a control can trace it back to the source requirement
- **Import controls in bulk** for large frameworks instead of creating them individually
- **Group related standards with a Program** when you need to audit or report on them together (see [Key Terms](key-terms.md#programs))
