# Exporting Data

The Export Data feature allows you to extract data from OpenGRC in CSV format for backup, reporting, or migration purposes.

## Accessing Export

1. Navigate to **Data Manager** in the admin navigation
2. Click **Export Data**

## Export Wizard

The export process uses a three-step wizard to guide you through selecting and downloading your data.

### Step 1: Select Entity

Choose the type of data you want to export from the dropdown menu. Entities are organized into groups:

| Group | Entities |
|-------|----------|
| **Core GRC** | Standards, Controls, Implementations, Policies, Audits, Audit Items, Risks, Programs, Bundles |
| **Third-Party** | Vendors, Applications, Assets, Vendor Documents |
| **Survey & Assessment** | Surveys, Survey Templates, Survey Questions, Checklists, Checklist Templates |
| **Data Management** | Data Requests, File Attachments, Policy Exceptions |

After selecting an entity, the wizard displays the total number of records available for export.

### Step 2: Select Fields

Configure which data fields to include in your export.

#### Database Fields

Select individual fields using the checkbox list. Field labels include type indicators:

- **(enum)** - Enumeration field with predefined values
- **(FK)** - Foreign key referencing another entity

Use the **Toggle all** button to quickly select or deselect all fields.

#### Include Timestamps

Enable **Include timestamps** to add `created_at`, `updated_at`, and `deleted_at` fields to your export.

#### Relationships

Optionally expand the **Relationships** section to include many-to-many relationship data. Related record IDs are exported as comma-separated values in a single column.

For example, exporting Controls with the "implementations" relationship would create a column containing `1,5,12` representing the IDs of linked Implementation records.

### Step 3: Export

Review your export configuration:

- **Entity**: The selected data type
- **Records**: Total records to be exported
- **Fields**: Number of fields selected
- **Relationships**: Number of relationships selected

Click **Download CSV** to generate and download your export file.

## Export File Format

The exported CSV file:

- Uses the first row as column headers matching field names
- Encodes text using UTF-8
- Escapes special characters according to RFC 4180
- Names files using the pattern: `{entity}_export_{date}_{time}.csv`

### Enum Values

Enumeration fields export their stored values (not display labels). For example, an Implementation status might export as `Implemented` rather than a formatted label.

### Relationship Data

Many-to-many relationships export as comma-separated ID lists. To import this data back, use the same format.

## Use Cases

### Backup

Regularly export critical entities (Standards, Controls, Implementations) to maintain offline backups of your compliance data.

### Reporting

Export data to analyze in spreadsheet applications or business intelligence tools.

### Migration

Export all entities before migrating to a new OpenGRC instance, then use the Import feature to restore.

### Audit Evidence

Export specific entities to provide evidence during external audits.

## Permissions

Requires the **Export Data** permission to access the Export Data page.

## Best Practices

1. **Include ID fields** when exporting data you plan to re-import, enabling updates to existing records
2. **Document your field selections** if you need to repeat exports with the same configuration
3. **Test imports** on a staging environment before importing exported data into production
4. **Include timestamps** for audit trail purposes when backing up data
