# Audits

Audits in OpenGRC allow you to assess and document the status of your security controls and implementations. Whether you're preparing for an external assessment or conducting an internal review, OpenGRC provides flexible auditing capabilities to meet your needs.

## What is an Audit?

An audit is a systematic evaluation of your security posture against a defined set of controls. During an audit, each control or implementation is reviewed and assigned a status indicating whether it meets the required criteria. Audits capture evidence, findings, and recommendations that can be used for internal improvement or shared with external auditors.

## Types of Audits

OpenGRC supports three types of audits, each serving a different purpose:

### Standards Audit

A **Standards Audit** evaluates the controls within a specific standard. This is the most common type of audit and is typically used when assessing compliance against a framework like NIST 800-171, ISO 27001, or SOC 2.

Use a Standards Audit when:
- Preparing for a formal certification or compliance assessment
- Evaluating your organization against a specific security framework
- Conducting a gap analysis against a new standard

### Implementation Audit

An **Implementation Audit** focuses on the actual implementations rather than the controls themselves. This audit type examines how controls are implemented in your environment and whether those implementations are operating effectively.

Use an Implementation Audit when:
- Verifying that technical controls are functioning as intended
- Conducting operational reviews of security measures
- Assessing the effectiveness of specific security technologies or processes

### Program Audit

A **Program Audit** evaluates all standards and controls within a program. This provides a comprehensive view of a functional area or compliance initiative, such as your entire Physical Security Program or CMMC readiness.

Use a Program Audit when:
- Conducting a holistic review of a compliance initiative
- Managing and controlling a piece of multiple standards (e.g., Physical security controls across multiple standards)
- Preparing for audits that span multiple standards (e.g., CMMC)
- Reporting on the overall health of a security program to leadership

## AI-Powered Audits

!!! enterprise "Enterprise Feature"
    OpenGRC Enterprise includes **AI-Powered Audits** that can automatically assess every control in your audit against your documented implementations and policies. Launch an AI audit from the **Workflow** menu on any in-progress audit to get effectiveness ratings, applicability determinations, and detailed auditor notes in minutes. [Learn more](../enterprise/ai-audit.md).

## Audit Statuses

During an audit, each item is assigned a status:

| Status | Description |
|--------|-------------|
| **Not Assessed** | The item has not yet been reviewed |
| **Compliant** | The control or implementation meets requirements |
| **Partially Compliant** | Some aspects meet requirements, but gaps exist |
| **Non-Compliant** | The control or implementation does not meet requirements |
| **Not Applicable** | The control does not apply to the organization's environment |

## Data Requests

**Data Requests** are a powerful feature for gathering evidence and information during an audit. When you need documentation, screenshots, or other artifacts from control owners or stakeholders, Data Requests streamline the collection process.

### How Data Requests Work

1. Create a Data Request specifying what information you need
2. Assign the request to the appropriate person or team
3. The assignee receives a notification and can respond directly in OpenGRC
4. Responses are tracked and linked to the relevant audit items
5. All evidence is stored and organized for easy reference

Data Requests help maintain a clear audit trail and reduce the back-and-forth typically required to gather audit evidence.

## Information Request Lists (IRLs)

An **Information Request List (IRL)** is a comprehensive list of all documentation and evidence needed for an audit. IRLs are commonly used by ***external auditors*** to communicate their requirements upfront.

In OpenGRC, you can:
- Import IRLs to organize audit evidence requirements
- Track the status of each requested item
- Link IRL items to specific controls or implementations
- Export evidence packages for auditors

IRLs help ensure nothing is missed during audit preparation and provide visibility into evidence collection progress.

## Reporting

OpenGRC provides several reporting options to communicate audit results:

### Audit Reports

Generate detailed audit reports that include:
- Overall compliance status and statistics
- Control-by-control findings
- Evidence and documentation references
- Recommendations for remediation

### Export Options

Audit data can be exported in multiple formats for sharing with external parties or integration with other tools:
- PDF reports for formal documentation
- CSV exports for data analysis

### Evidence Downloads

OpenGRC provides a comprehensive evidence export feature designed for handoff to external auditors or long-term archival storage. When you download evidence from Data Requests, you receive:

- **PDF files** - All evidence documents converted to PDF format for consistency
- **ZIP package** - Everything bundled into a single downloadable archive
- **File hashes** - A cryptographic hash of each file included for integrity verification

This ensures auditors can verify that evidence has not been modified since collection and provides a complete, portable package of all audit artifacts.

## Best Practices

- **Plan your audit scope** - Clearly define what will be assessed before starting
- **Use Data Requests early** - Give stakeholders time to gather evidence
- **Document everything** - Capture notes and observations during the assessment
- **Review findings before finalizing** - Ensure accuracy before generating reports
- **Track remediation** - Use audit findings to drive security improvements
