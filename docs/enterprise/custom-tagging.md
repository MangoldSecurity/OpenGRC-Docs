# Custom Tagging

!!! enterprise "Enterprise Feature"
    Custom Tagging is available exclusively in OpenGRC Enterprise. [Learn more about Enterprise](https://opengrc.com).

Custom Tags let organizations create their own free-form labels and apply them across almost any record in OpenGRC -- Controls, Implementations, Standards, Vendors, Surveys, Custom Dashboards, and more. Unlike [Department and Scope](#tags-vs-department-and-scope), which are fixed, managed classification lists, tags are open-ended: create as many as you need, and apply as many as make sense to a single record.

## Overview

Custom Tagging helps organizations:

- Create their own labels without needing a predefined list of values
- Apply multiple tags to a single record
- Organize records by project, initiative, team, or any ad hoc grouping that doesn't fit existing fields
- Scope [AI-Powered Audits](ai-audit.md#scoping-an-ai-audit) and [Risk Assessor](risk-assessor.md#scoping-ai-analysis) analysis to only tagged records

## Managing Tags

Tags are managed centrally under **Settings > Tags**. The list shows every tag's name and a **Used By** count of how many records reference it.

- Click **New tag** and enter a **Tag Name** to create one
- Click **Edit** to rename a tag -- since tags are referenced by name, renaming updates it everywhere the tag is used
- Click **Delete** to remove a tag entirely

## Tagging a Record

Most record forms include a **Tags** field where you can:

1. Select one or more existing tags from the dropdown
2. Click **Create** next to the field to add a new tag on the spot, without leaving the form

Because tag creation is available inline, most users never need to visit the central Tags list -- it exists mainly for renaming, cleanup, and seeing how widely a tag is used.

## Using Tags to Scope AI Analysis

Tags are one of three filters (alongside Department and Scope) available when launching an [AI-Powered Audit](ai-audit.md#scoping-an-ai-audit) or running [Risk Assessor](risk-assessor.md#scoping-ai-analysis) AI analysis. Selecting one or more tags restricts the AI to only implementations and policies carrying at least one of those tags, alongside any Department and Scope filters also set.

## Tags vs. Department and Scope

Department and Scope are **taxonomies** -- managed, single-select classification lists configured under **Settings > Taxonomy Types**, with a fixed set of terms (e.g. specific department names) that an administrator defines ahead of time. Tags are simpler and more flexible:

| | Tags | Department / Scope |
|---|---|---|
| **Values** | Created freely by any user, on the fly | Predefined terms managed centrally |
| **Per record** | Multiple tags at once | Typically one value |
| **Best for** | Ad hoc grouping, projects, initiatives | Stable organizational classification |

Use Department and Scope for classification that mirrors your org chart or a fixed set of categories. Use Tags for anything more fluid -- a specific project, an audit initiative, or a temporary grouping you don't want to formalize into a taxonomy.

## Best Practices

- **Reuse existing tags** rather than creating near-duplicates (e.g. "Q3-Audit" vs "Q3 Audit") -- check the Tags list before creating a new one
- **Rename instead of recreating** -- since tags are referenced by name everywhere, renaming a tag updates all its usages at once
- **Combine tags with Department and Scope** when scoping AI analysis for the most precise targeting
- **Periodically review the Used By count** to clean up tags that are no longer referenced
