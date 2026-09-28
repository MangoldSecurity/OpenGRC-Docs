# Risk Management

OpenGRC provides a straightforward risk management framework to identify, assess, and track cybersecurity risks. The system uses a standard likelihood-impact methodology with visual heatmaps and links risks to mitigating controls.

## Overview

Risk Management in OpenGRC enables organizations to:

- Document and categorize security risks
- Assess inherent risk (before controls)
- Assess residual risk (after controls)
- Link risks to mitigating implementations
- Visualize risk posture with heatmaps
- Track risk treatment decisions
- Generate risk reports

## Risk Attributes

Each risk record includes:

| Field | Description |
|-------|-------------|
| **Code** | Unique identifier (e.g., RISK-001) |
| **Name** | Risk title |
| **Description** | Detailed description of the risk |
| **Department** | Responsible department |
| **Scope** | Business scope or area |
| **Status** | Assessment status |
| **Inherent Likelihood** | Likelihood score before controls (1-5) |
| **Inherent Impact** | Impact score before controls (1-5) |
| **Residual Likelihood** | Likelihood score after controls (1-5) |
| **Residual Impact** | Impact score after controls (1-5) |
| **Inherent Risk** | Calculated score (likelihood x impact) |
| **Residual Risk** | Calculated score (likelihood x impact) |
| **Implementations** | Linked mitigating controls |

## Risk Status

| Status | Description |
|--------|-------------|
| **Not Assessed** | Risk has not been evaluated |
| **In Progress** | Assessment is underway |
| **Assessed** | Risk has been fully evaluated |
| **Closed** | Risk has been resolved or accepted |

## Risk Response (Mitigation Type)

When assessing a risk, select how the organization will respond:

| Response | Description |
|----------|-------------|
| **Open** | No action taken yet |
| **Avoid** | Eliminate the risk entirely |
| **Mitigate** | Reduce likelihood or impact through controls |
| **Transfer** | Transfer risk to a third party (insurance, outsourcing) |
| **Accept** | Accept the residual risk |

## Risk Scoring Methodology

### Likelihood Scale (1-5)

| Score | Level | Description |
|-------|-------|-------------|
| 1 | Very Low | Highly unlikely to occur |
| 2 | Low | Low likelihood of occurrence |
| 3 | Moderate | May occur at some point |
| 4 | High | Likely to occur |
| 5 | Very High | Almost certain to occur |

### Impact Scale (1-5)

| Score | Level | Description |
|-------|-------|-------------|
| 1 | Very Low | Minimal damage or disruption |
| 2 | Low | Minor damage, easily recoverable |
| 3 | Moderate | Noticeable damage, requires effort to recover |
| 4 | High | Significant damage, major recovery effort |
| 5 | Very High | Catastrophic damage, may not recover |

### Risk Calculation

Risk scores are calculated as:
```
Risk Score = Likelihood x Impact
```

This produces scores ranging from 1 (lowest) to 25 (highest).

### Inherent vs. Residual Risk

**Inherent Risk**
- Assessed assuming NO controls are in place
- Represents the baseline risk exposure
- Used to understand the natural risk level

**Residual Risk**
- Assessed WITH all current controls in place
- Represents the remaining risk after mitigations
- Used for reporting and decision-making

## Creating a Risk

### Step 1: Navigate to Risks
1. Go to **Risks** in the main navigation
2. Click **Create Risk**

### Step 2: Enter Risk Overview
1. **Code** - Auto-generated or enter custom code
2. **Name** - Enter a descriptive risk name
3. **Description** - Describe the risk scenario in detail
4. **Department** - Select the responsible department
5. **Scope** - Select the business scope

### Step 3: Assess Inherent Risk
Evaluate the risk assuming no controls exist:
1. **Inherent Likelihood** - Select 1-5 based on how likely the risk is to occur
2. **Inherent Impact** - Select 1-5 based on the potential damage

Use the reference tables provided in the form to guide your assessment.

### Step 4: Assess Residual Risk
Evaluate the risk with current controls in place:
1. **Residual Likelihood** - Select 1-5 with mitigations considered
2. **Residual Impact** - Select 1-5 with mitigations considered

### Step 5: Link Implementations (Optional)
Associate implementations (controls) that mitigate this risk:
1. Search for relevant implementations
2. Select all implementations that reduce this risk
3. These can be added later if not known yet

### Step 6: Save
Click **Create** to save the risk. The system automatically calculates inherent and residual risk scores.

## Managing Risks

### Viewing the Risk List
The risk list displays:
- Risk name and description
- Inherent risk score (color-coded)
- Residual risk score (color-coded)
- Department and scope
- Default sort: Residual risk (highest first)

### Filtering Risks
Filter by:
- Department
- Scope
- Status
- Risk score ranges

### Editing Risks
1. Click on a risk to view details
2. Click **Edit** to modify
3. Update scores or link additional implementations
4. Save changes (scores recalculate automatically)

## Risk Heatmaps

OpenGRC provides visual 5x5 risk heatmaps showing risk distribution:

### Inherent Risk Heatmap
- Shows risks plotted by inherent likelihood and impact
- X-axis: Likelihood (Very Low to Very High)
- Y-axis: Impact (Very Low to Very High)
- Each cell shows count of risks in that zone
- Hover to see risk names

### Residual Risk Heatmap
- Shows risks plotted by residual likelihood and impact
- Same layout as inherent heatmap
- Compare with inherent to see control effectiveness

### Interpreting Heatmaps
- **Top-right (red zone)** - High likelihood, high impact - immediate attention needed
- **Bottom-left (green zone)** - Low likelihood, low impact - acceptable risk
- **Movement from inherent to residual** - Shows effectiveness of controls

## Linking Risks to Controls

### From the Risk Detail Page
1. Open a risk
2. View the **Implementations** section
3. Click **Attach** to add implementations
4. Search and select relevant implementations
5. Save

### From an Implementation
1. Open an implementation
2. Go to the **Risks** tab
3. Click **Attach** to add risks
4. Select risks this implementation mitigates
5. Save

### From a Policy
1. Open a policy
2. Go to the **Risks** tab
3. Click **Attach** to add risks
4. Select risks the policy addresses
5. Save

## Risk Reports

### Generating a Risk Report
1. Navigate to the risk list
2. Click **Download Risk Report**
3. PDF report is generated with:
   - Inherent and residual heatmaps (side-by-side)
   - Detailed risk table with:
     - Risk name and description
     - Inherent risk score
     - Associated implementations
     - Residual risk score

### Report Use Cases
- Board and executive reporting
- Audit documentation
- Risk committee reviews
- Compliance evidence

## Risk Color Coding

Risk scores are color-coded for quick identification:

| Score Range | Color | Interpretation |
|-------------|-------|----------------|
| 1-4 | Green | Low risk |
| 5-8 | Blue | Low-Moderate risk |
| 9-12 | Yellow | Moderate risk |
| 13-19 | Orange | Moderate-High risk |
| 20-25 | Red | High risk |

## API Access

Risks can be accessed via the REST API:

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/risks` | GET | List all risks |
| `/api/risks/{id}` | GET | Get specific risk with implementations |
| `/api/risks` | POST | Create new risk |
| `/api/risks/{id}` | PUT | Update risk |
| `/api/risks/{id}` | DELETE | Delete risk |

## Requesting an Update

**Request Update**, on a risk's detail page, delegates a review of the record the same way it works for [controls](../foundations/controls.md#approvals-and-delegation) -- assign it to an external portal user for a magic-link review form in [My Portal](../enterprise/my-portal.md#record-update-requests), or to an internal user for a to-do on their To-Do & Approvals page.

## Best Practices

- **Start with inherent risk** - Always assess the baseline risk before considering controls
- **Be realistic about residual risk** - Controls reduce but rarely eliminate risk
- **Link all mitigating controls** - Connect risks to implementations for traceability
- **Review regularly** - Reassess risks quarterly or when conditions change
- **Use consistent criteria** - Apply the same likelihood and impact definitions across all risks
- **Focus on high residual risks** - Prioritize attention on risks that remain high after controls
- **Document your reasoning** - Use the description field to explain risk scenarios
- **Compare heatmaps** - Review inherent vs. residual heatmaps to validate control effectiveness
- **Accept risk formally** - Use the Accept response only after conscious decision-making
