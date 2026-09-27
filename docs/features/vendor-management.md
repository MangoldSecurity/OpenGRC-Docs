# Vendor Risk Management (TPRM)

OpenGRC provides comprehensive Third-Party Risk Management (TPRM) capabilities to assess, monitor, and manage vendor security risks. The system includes vendor profiles, security assessments, document management, and a vendor portal for self-service document uploads.

## Overview

Vendor Risk Management in OpenGRC helps organizations:

- Maintain a vendor inventory with risk ratings
- Conduct security assessments via surveys
- Collect and review vendor documentation
- Calculate risk scores based on assessment responses
- Provide vendor portal access for self-service
- Track vendor relationships and contacts

## Vendor Profiles

### Vendor Attributes

Each vendor record includes:

| Field | Description |
|-------|-------------|
| **Name** | Vendor organization name |
| **URL** | Vendor website |
| **Description** | Detailed description of the vendor |
| **Vendor Manager** | Internal relationship manager |
| **Status** | Vendor status (Pending, Accepted, Rejected, Expired, Terminated) |
| **Organizational Risk Rating** | Manual risk classification |
| **Assessed Risk** | Calculated risk from assessments |
| **Contact Name** | Primary vendor contact |
| **Contact Email** | Vendor contact email |
| **Contact Phone** | Vendor contact phone |
| **Address** | Vendor physical address |
| **Notes** | Internal notes |
| **Logo** | Vendor logo image |

### Vendor Statuses

| Status | Description |
|--------|-------------|
| **Pending** | Initial status, awaiting review |
| **Accepted** | Approved vendor relationship |
| **Rejected** | Vendor not approved |
| **Expired** | Vendor relationship has ended |
| **Terminated** | Vendor relationship actively ended |

### Risk Ratings

Vendors are rated on a five-level scale:

| Rating | Score Range | Description |
|--------|-------------|-------------|
| **Very Low** | 0-20 | Minimal risk |
| **Low** | 21-40 | Low risk |
| **Medium** | 41-60 | Moderate risk |
| **High** | 61-80 | Elevated risk |
| **Critical** | 81-100 | Highest risk |

## Adding a Vendor

### Step 1: Navigate to Vendor Management
1. Go to **Vendor Management** in the main navigation
2. Click **Add Vendor**

### Step 2: Enter Vendor Information
1. **Name** - Enter the vendor organization name
2. **URL** - Enter the vendor website (optional)
3. **Description** - Describe the vendor and their services

### Step 3: Assign Management
1. **Vendor Manager** - Select the internal relationship owner
2. **Status** - Set initial status (typically Pending)
3. **Organizational Risk Rating** - Set initial risk level if known

### Step 4: Add Contact Information
1. **Contact Name** - Primary vendor contact
2. **Contact Email** - Contact email address
3. **Contact Phone** - Contact phone number
4. **Address** - Vendor physical address

### Step 5: Save
Click **Create** to save the vendor.

## Vendor Assessments

### Assessment Types

OpenGRC supports two assessment approaches:

**Internal Assessment**
- Completed by you, based on your team's existing knowledge of the vendor
- No email or external link involved -- you answer the questionnaire directly in OpenGRC

**External Assessment (Send Survey)**
- Completed by the vendor
- Sent via email with a secure, time-limited link (30-day token)
- Vendor completes the questionnaire directly, without an OpenGRC account

### Sending or Assigning a Vendor Assessment

1. Navigate to the vendor detail page
2. Click **Send Survey** or **Assess Risk** in the page header (or **Assess Risk** on the **Surveys** tab) -- both open the same dialog
3. Choose an **Assessment type**:
   - **Internal Assessment** - You complete the questionnaire yourself based on what you already know
   - **Send Survey** - The vendor receives a link and completes the questionnaire themselves
4. Select a **Survey template**
5. For **Send Survey**, also enter:
   - **Respondent email** (required)
   - **Respondent name** (optional)
   - **Personal message** (optional note included in the invitation email)
6. Optionally set a **Due date**
7. Click **Start Internal Assessment** or **Send to Vendor**

!!! note "Assigning to a teammate"
    The quick dialog above always starts the Internal Assessment as you. To assign it to a different internal teammate instead, open the survey's full record (via the vendor's **Surveys** tab, or **Create Survey** from a survey template) and set **Assigned To** under **Respondent Information** -- this field is only available on the full survey form, not the quick dialog.

### Completing an Internal Assessment

Starting an Internal Assessment takes you directly into the questionnaire:

- The **Sections** sidebar lists each section of the survey with its answered-question count, plus a **Total Progress** counter
- Each question shows its number, **Required**/**Weight** badges, the question text, and a **Where to find this** hint pointing to the relevant category of evidence
- Answer using the input appropriate to the question type (e.g. Yes/No toggle), and optionally **Add comment** on any question
- Click **Save & exit** to save progress and finish later, or **Submit** once all required questions are answered

The survey then appears on the vendor's **Surveys** tab with your name as the respondent, and its status and risk score update automatically as described below.

### Recurring Vendor Assessments

Any survey (internal or external) can be set to automatically regenerate on a schedule instead of being a one-time assessment:

1. Open the survey's full record (**Edit**, from the vendor's **Surveys** tab)
2. Expand the **Recurrence** section
3. Set **Frequency** to how often a new survey should be generated: **Daily**, **Weekly**, **Monthly**, **Quarterly**, **Semi-Annual** (every 6 months), or **Yearly**
4. Click **Save changes**

The vendor's **Surveys** tab shows a **Recurrence** column with the configured frequency and a **Next Due** column with the date the next instance will be generated, so you can see upcoming reassessments at a glance.

### Resending Questions for Correction

If a respondent's answers need clarification or correction, you can send back just the affected questions instead of re-issuing the entire survey:

1. Open the survey and click **Resend Selected Questions**
2. In the **Questions to resend** list, search or use **Select all** to choose the specific questions to send back
3. Optionally add a **Note to respondent** explaining why the questions are being returned -- this is included in the email and shown above the questions
4. Click **Send Follow-up**

Only the selected questions are sent back to the respondent as a follow-up; answers already submitted on the rest of the survey stay intact.

### Survey Question Types

Surveys support multiple question types:

| Type | Description |
|------|-------------|
| **Boolean** | Yes/No toggle |
| **Text** | Short text response |
| **Long Text** | Multi-line text response |
| **Single Choice** | Radio button selection |
| **Multiple Choice** | Checkbox selection |
| **File** | File upload |

### Risk Scoring

Survey responses are automatically scored based on:

- **Risk Weight** - Each question's contribution to overall score (0-100)
- **Risk Impact** - Whether "Yes" answers reduce or increase risk
- **Option Scores** - Specific scores for each answer option

**Scoring Formula:**
```
Score = (Sum of weighted answer scores) / (Total weight)
```

The calculated score (0-100) is converted to a risk rating:
- 0-20: Very Low
- 21-40: Low
- 41-60: Medium
- 61-80: High
- 81-100: Critical

### Manual Scoring

Some question types require manual scoring:
- **Text questions** - Reviewer assigns a score based on response quality
- **File uploads** - Reviewer evaluates uploaded documentation

To manually score:
1. Open the survey detail view
2. Review text responses and files
3. Assign scores to each manually-scored question
4. Save to update the overall risk score

## Vendor Documents

### Document Types

Vendors can upload various document types:

| Type | Description |
|------|-------------|
| **SOC 2 Report** | SOC 2 Type I or II report |
| **ISO Certificate** | ISO 27001 or other certification |
| **Penetration Test** | Security assessment report |
| **Insurance Certificate** | Cyber liability insurance |
| **Business Continuity Plan** | BCP documentation |
| **Privacy Policy** | Privacy practices documentation |
| **Security Policy** | Security policy documentation |
| **Contract** | Vendor contract or agreement |
| **SLA** | Service level agreement |
| **Other** | Other document types |

### Document Statuses

| Status | Description |
|--------|-------------|
| **Draft** | Not yet submitted for review |
| **Pending** | Awaiting review |
| **Under Review** | Currently being reviewed |
| **Approved** | Document accepted |
| **Rejected** | Document not accepted |
| **Expired** | Past expiration date |

### Managing Vendor Documents

**From the Vendor Detail Page:**
1. Go to the **Documents** tab
2. Click **Create** to add a new document
3. Select document type
4. Enter name and description
5. Upload the file
6. Set issue and expiration dates
7. Save

**Reviewing Documents:**
1. Navigate to **Vendor Documents** in the navigation
2. Filter by status (Pending, Under Review)
3. Click on a document to review
4. **Approve** with optional notes, or
5. **Reject** with required reason

### Document Expiration

The system tracks document expiration:
- **Expiring Soon** - Documents expiring within 30 days are flagged
- **Expired** - Past expiration date, status changes automatically
- Dashboard shows expiring document counts

## Vendor Portal

### Inviting Vendor Users

Enable vendors to access their own portal:
1. Navigate to vendor detail page
2. Go to **Vendor Users** tab
3. Click **Invite User**
4. Enter name and email
5. Vendor receives invitation email
6. They set their password to activate access

### Vendor Portal Capabilities

Vendor users can:
- View their assigned surveys
- Complete survey questionnaires
- Upload documents
- View document status
- Update contact information

### Managing Vendor Users

**Set Primary Contact:**
- Mark one user as primary
- Primary contact receives important communications

**Resend Invitation:**
- Resend activation email to pending users

**Send Magic Link:**
- Send one-time login link to activated users

**Revoke Access:**
- Remove user access when no longer needed

## Vendor Management Dashboard

The Vendor Manager page provides a centralized dashboard with three tabs:

### Vendors Tab
- Statistics widget showing totals and breakdowns
- Full vendor list with filtering and actions
- Quick access to add new vendors

### Vendor Surveys Tab
- All active vendor assessments
- Survey status and progress
- Quick access to review responses

### Survey Templates Tab
- Manage survey templates
- Create and edit question sets
- Configure risk weights and scoring

## Reporting and Analytics

### Dashboard Statistics

The dashboard displays:
- **Total Vendors** - With active/pending breakdown
- **High Risk Vendors** - Count with color coding
- **Vendor Surveys** - Pending and completed counts

### Vendor Risk Tracking

Each vendor shows:
- **Organizational Impact** - Manual inherent risk rating
- **Assessed Risk** - Calculated from latest assessment
- Risk score and last calculated date

## Permissions

| Permission | Capabilities |
|------------|--------------|
| **List Vendors** | View vendor list |
| **Create Vendors** | Add new vendors |
| **Read Vendors** | View vendor details |
| **Update Vendors** | Edit vendor information |
| **Delete Vendors** | Remove vendors |
| **Manage Vendor Management** | Access settings and configuration |

## Best Practices

- **Assess before accepting** - Complete a security assessment before approving vendor relationships
- **Set review schedules** - Reassess vendors annually or when significant changes occur
- **Track document expiration** - Keep SOC 2 reports, insurance, and certifications current
- **Use the pre-built survey** - Start with the included security survey and customize as needed
- **Assign vendor managers** - Every vendor should have an accountable internal owner
- **Categorize by risk** - Use risk ratings to prioritize oversight efforts
- **Enable vendor portal** - Let vendors upload documents and complete surveys directly
- **Monitor high-risk vendors** - Pay special attention to vendors rated High or Critical
