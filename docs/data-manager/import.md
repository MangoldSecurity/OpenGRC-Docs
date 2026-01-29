# Importing Data

The Import Data feature allows you to bulk create or update records in OpenGRC using CSV files.

## Accessing Import

1. Navigate to **Data Manager** in the admin navigation
2. Click **Import Data**

## Import Wizard

The import process uses a four-step wizard to guide you through uploading, mapping, and importing your data.

### Step 1: Select Entity

Choose the entity type you want to import from the dropdown menu. Entities are organized into groups:

| Group | Entities |
|-------|----------|
| **Core GRC** | Standards, Controls, Implementations, Policies, Audits, Audit Items, Risks, Programs, Bundles |
| **Third-Party** | Vendors, Applications, Assets, Vendor Documents |
| **Survey & Assessment** | Surveys, Survey Templates, Survey Questions, Checklists, Checklist Templates |
| **Data Management** | Data Requests, File Attachments, Policy Exceptions |

After selecting an entity:

- The wizard displays available fields and required field count
- Click **Download CSV Template** to get a pre-formatted template file

#### CSV Template

The downloadable template includes:

- **Header row**: All available field names
- **Description row**: Type hints and validation requirements (prefixed with #)
- **Empty row**: For your data

Template descriptions indicate:

- `REQUIRED` - Field must have a value
- `Optional - provide to update existing, omit to create new` - ID field for upsert operations
- `Options: value1, value2, ...` - Valid options for enum fields
- `true/false or 1/0` - Boolean field format
- `Format: YYYY-MM-DD` - Date field format
- `Format: YYYY-MM-DD HH:MM:SS` - DateTime field format
- `Foreign Key (ID)` - Reference to another entity's ID
- `Integer`, `Decimal`, `Text` - Data type hints

### Step 2: Upload File

Upload your CSV file using the file picker or drag-and-drop.

**Requirements:**

- File format: CSV (`.csv`)
- Maximum size: 10MB
- Encoding: UTF-8 recommended

After upload, the wizard:

- Parses the CSV headers
- Displays the total number of data rows detected
- Prepares for column mapping

### Step 3: Map Columns

Map your CSV columns to database fields.

#### Auto-Mapping

The wizard automatically matches CSV headers to database fields when names are similar (case-insensitive, ignoring underscores and spaces). For example:

- `Control Code` automatically maps to `code`
- `standard_id` automatically maps to `standard_id`

#### Manual Mapping

For each CSV column, select the corresponding database field from the dropdown. Options show:

- Field name and label
- `(required)` indicator for mandatory fields

#### Required Fields

All required fields (marked with asterisks) must be mapped before proceeding. The wizard validates mapping completeness and shows errors if required fields are missing.

#### Skipping Columns

Select **Skip this column** to exclude a CSV column from import.

### Step 4: Review & Import

Preview your data before importing.

#### Data Preview

The wizard displays the first 5 rows of mapped data in a table format, showing:

- Row numbers
- Mapped field values as they will be imported

Review the preview to verify:

- Column mapping is correct
- Data formats are valid
- Required fields have values

#### Import Summary

- **Total Rows**: Number of data rows to process
- **Mapped Fields**: Number of CSV columns mapped to database fields

#### Starting the Import

Click **Start Import** to begin processing.

During import:

- A loading spinner indicates processing
- The button is disabled to prevent duplicate submissions

#### Import Results

After completion, the wizard displays:

**Success Summary:**

- Total records processed
- Successfully imported count
- Error count (if any)

**Error Details:**

If errors occurred, a detailed list shows:

- Row number where the error occurred
- Error message describing the issue

Common error causes:

- Missing required field values
- Invalid enum values
- Foreign key references to non-existent records
- Data type mismatches

## Upsert Behavior

The import feature supports **upsert** operations (update or insert):

### Creating New Records

- Omit the `id` field or leave it empty
- The system creates a new record with an auto-generated ID

### Updating Existing Records

- Include the `id` field with the existing record's ID
- The system updates the matching record

### Alternative Unique Fields

If `id` is not provided, the system attempts to match records by:

1. `code` field (for Standards, Controls, etc.)
2. `email` field (for user-related entities)
3. `name` field (as fallback)

If a match is found, the record is updated; otherwise, a new record is created.

## Data Validation

### Required Fields

All fields marked as required must have non-empty values.

### Enum Fields

Enum values are matched using flexible resolution:

1. Exact value match
2. Case-insensitive value match
3. Display label match
4. Enum case name match

For example, an Implementation status accepts: `Implemented`, `implemented`, `IMPLEMENTED`, or the enum case name.

### Boolean Fields

Accepted values:

- True: `true`, `1`, `yes`, `on`
- False: `false`, `0`, `no`, `off`

### Date Fields

Expected format: `YYYY-MM-DD` (e.g., `2024-03-15`)

### DateTime Fields

Expected format: `YYYY-MM-DD HH:MM:SS` (e.g., `2024-03-15 14:30:00`)

### Foreign Keys

Foreign key fields require the numeric ID of the related record. Use the Export feature to discover existing IDs.

## Transaction Safety

Imports use database transactions for safety:

- All changes are atomic (all succeed or all fail)
- If more than 10% of rows have errors, the entire import is rolled back
- No partial imports occur on transaction failure

## Use Cases

### Bulk Data Entry

Import large datasets from spreadsheets rather than manual entry.

### Data Migration

Import data exported from another OpenGRC instance or external system.

### Batch Updates

Update multiple records by exporting, modifying in a spreadsheet, and re-importing with IDs.

### Framework Import

Import custom security frameworks with Standards and Controls from structured CSV files.

## Permissions

Requires the **Import Data** permission to access the Import Data page.

## Best Practices

1. **Start with the template** - Download and use the CSV template to ensure correct column names
2. **Test with small batches** - Import a few rows first to verify mapping and validation
3. **Include IDs for updates** - Always include the `id` column when updating existing records
4. **Validate enum values** - Check the template's description row for valid enum options
5. **Use consistent date formats** - Stick to `YYYY-MM-DD` format for all date fields
6. **Back up before bulk imports** - Export existing data before large import operations
7. **Review the preview** - Carefully check the data preview before starting the import

## Troubleshooting

### "Required field is missing or empty"

Ensure all required fields have values in your CSV. Check the template for field requirements.

### "Invalid enum value"

The value doesn't match any valid option. Check the template description row for accepted values.

### "Could not read the uploaded file"

- Verify the file is a valid CSV
- Check file encoding (use UTF-8)
- Ensure file size is under 10MB

### "Import rolled back"

Too many rows had errors (>10%). Review the error details, fix your CSV, and retry.

### Foreign key errors

The referenced record doesn't exist. Verify IDs by exporting the related entity first.
