# Custom Dashboards

!!! enterprise "Enterprise Feature"
    Custom Dashboards are available exclusively in OpenGRC Enterprise. [Learn more about Enterprise](https://opengrc.com).

Custom Dashboards let organizations build dashboards tailored to their needs, visualizing the compliance data that matters most to them. Instead of relying on a single fixed view, teams can assemble their own dashboards from a library of widgets pulling data from almost any object in OpenGRC.

## Overview

Custom Dashboards help organizations:

- Build one or more dashboards from a library of widget types (stat cards, tables, and charts)
- Pull data from nearly any object in OpenGRC -- Controls, Risks, Audits, Vendors, Policies, Incidents, and more
- Group, filter, and aggregate data per widget without leaving the dashboard builder
- Arrange and resize widgets freely on a drag-and-drop grid
- Share dashboards with other users, or clone an existing dashboard as a starting point for a new view

## How It Works

### Creating a Dashboard

1. From any dashboard, click the **+** icon in the toolbar
2. Click **New custom dashboard**
3. Enter a **Name** and **Slug**
4. Optionally set a **Default role** (Read, Write, or Owner) to give all users that level of access, or leave it blank to share the dashboard with specific users later
5. Choose whether to **Add to navigation**, and optionally set a custom **Navigation icon**, **Navigation label**, **Navigation group**, and **Navigation position** in the sidebar
6. Click **Create**

### Adding and Configuring Widgets

1. Open a dashboard and click **Edit mode**
2. Click **Insert widget**
3. Choose a **Quick widget** for a one-click add, or a **New widget** type to build one from scratch

**Quick widgets** are pre-configured and require no setup:

| Quick Widget | Description |
|---|---|
| **Compliance Overview** | Summary of compliance status across the organization |
| **Implementation Effectiveness** | Breakdown of implementation effectiveness ratings |
| **Audit List (Top-5)** | The five most relevant audits |
| **My ToDo List (Top-5)** | The user's five most pressing to-dos |

**New widgets** are built from scratch by choosing a type and configuring its data:

| Widget Type | Configuration |
|---|---|
| **Stats overview cards** | One or more cards, each with its own **Data source**, **Metric** (Count, Sum, Average, Min, Max), **Filters**, and **Custom label** |
| **Table** | **Data source**, **Columns** (pick individual columns or add all), **Filters**, **Heading** |
| **Line chart** | **Data source**, **Group by**, **Metric**, **Filters**, **Display** (colors, heading, data label) |
| **Bar chart** | **Data source**, **Group by** (plus a grouping mode for yes/no fields), **Metric**, **Filters**, **Display** (bar colors, heading, data label) |
| **Scatter chart** | **Data source**, **Metric**, **Filters**, **Display** |
| **Pie chart** | **Data source**, **Group by**, **Metric**, **Filters**, **Display** |
| **Doughnut chart** | **Data source**, **Group by**, **Metric**, **Filters**, **Display** |
| **Polar area chart** | **Data source**, **Group by**, **Metric**, **Filters**, **Display** |

The **Data source** for a new widget can be almost any object in OpenGRC, including Controls, Risks, Audits, Audit items, Implementations, Policies, Vendors, Standards, Programs, Incidents, Assessments, Certifications, and more. **Filters** let you build rules (with AND/OR conditions) to limit a widget to a specific subset of that data.

Once a widget is added:

- Drag the resize handles on a widget's edges to resize it
- Click **Edit** on a widget to change its configuration
- Click **Delete** to remove it
- Click **Stop editing** when finished

### Managing a Dashboard

Each dashboard's toolbar provides the following actions:

| Action | Description |
|---|---|
| **Edit mode** | Add, resize, edit, or delete widgets |
| **Clone** | Duplicate the dashboard as a starting point for a new one |
| **Settings** | Update the dashboard's name, slug, default role, and navigation settings, or delete the dashboard |
| **Share** | Grant specific users access to the dashboard |

### Sharing a Dashboard

1. Click **Share** on the dashboard toolbar
2. Click **Add user** and assign the user an access level
3. Click **Save changes**

Sharing individual users this way works alongside the **Default role** set when the dashboard was created -- use **Default role** to grant blanket access to all users, and **Share** to grant access to specific individuals.

## Best Practices

- **Start from a Quick widget** when one covers your need -- they require no configuration and cover the most common views
- **Use filters to scope widgets** to the data that matters (e.g. a specific program, standard, or status) rather than showing every record
- **Choose Default role or Share deliberately** -- use Default role for dashboards meant for broad visibility, and Share for dashboards intended for a specific team or audience
- **Clone before major changes** so you always have a working version to fall back on
- **Use descriptive labels and headings** on widgets so viewers understand each visualization without needing to edit it

## Permissions

- Only **Super Admins** can create new custom dashboards
- Access to view or edit an existing dashboard is controlled by its **Default role** and any users added via **Share**
