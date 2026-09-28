# Asset Management

OpenGRC provides comprehensive IT asset management capabilities to track hardware, software licenses, and equipment throughout their lifecycle. Assets can be linked to control implementations, enabling compliance tracking at the asset level.

## Overview

Asset management in OpenGRC enables organizations to:

- Maintain a complete hardware and software inventory
- Track asset assignment and location
- Manage financial information (purchase, depreciation, value)
- Monitor warranty and support contracts
- Track lifecycle stages (acquisition to disposal)
- Link assets to security controls and implementations
- Maintain compliance and security status

## Asset Attributes

### Identification

| Field | Description |
|-------|-------------|
| **Asset Tag** | Unique identifier for the asset |
| **Serial Number** | Manufacturer serial number |
| **Name** | Descriptive asset name |
| **Asset Type** | Type classification (Laptop, Server, etc.) |
| **Status** | Current status (Available, In Use, Retired, etc.) |

### Hardware Specifications

| Field | Description |
|-------|-------------|
| **Manufacturer** | Hardware manufacturer |
| **Model** | Model name/number |
| **Processor** | CPU specification |
| **RAM (GB)** | Memory capacity |
| **Storage Type** | SSD, HDD, NVMe, etc. |
| **Storage Capacity (GB)** | Storage size |
| **Graphics Card** | GPU specification |
| **Screen Size** | Display size (for laptops/monitors) |
| **MAC Address** | Network interface address |
| **IP Address** | Assigned IP address |
| **Hostname** | Network hostname |
| **Operating System** | OS name |
| **OS Version** | OS version number |

### Assignment & Location

| Field | Description |
|-------|-------------|
| **Assigned To** | User the asset is assigned to |
| **Assigned At** | Date of assignment |
| **Location** | Location reference |
| **Building** | Building name/number |
| **Floor** | Floor number |
| **Room** | Room number/name |
| **Department** | Department assignment |

### Financial Information

| Field | Description |
|-------|-------------|
| **Purchase Date** | When the asset was purchased |
| **Purchase Price** | Original purchase cost |
| **Purchase Order Number** | PO reference |
| **Supplier** | Vendor who supplied the asset |
| **Invoice Number** | Invoice reference |
| **Depreciation Method** | Straight-line, declining balance, etc. |
| **Depreciation Rate** | Annual depreciation percentage |
| **Current Value** | Current book value |
| **Residual Value** | Expected value at end of life |

### Warranty & Support

| Field | Description |
|-------|-------------|
| **Warranty Start Date** | When warranty begins |
| **Warranty End Date** | When warranty expires |
| **Warranty Type** | Type of warranty coverage |
| **Warranty Provider** | Who provides the warranty |
| **Support Contract Number** | Support agreement reference |
| **Support Expiry Date** | When support expires |

### Lifecycle Management

| Field | Description |
|-------|-------------|
| **Received Date** | When asset was received |
| **Deployment Date** | When put into service |
| **Last Audit Date** | Most recent inventory audit |
| **Next Audit Date** | Scheduled next audit |
| **Retirement Date** | When retired from service |
| **Disposal Date** | When disposed |
| **Disposal Method** | How asset was disposed |
| **Expected Life (Years)** | Expected useful life |

### Security & Compliance

| Field | Description |
|-------|-------------|
| **Encryption Enabled** | Whether disk encryption is active |
| **Antivirus Installed** | Whether AV is installed |
| **Last Security Scan** | Most recent security scan date |
| **Compliance Status** | Compliant, Non-Compliant, Exempt, Pending |
| **Data Classification** | Public, Internal, Confidential, Restricted |

## Asset Types

Assets are classified by type:

- **Laptop** - Portable computers
- **Desktop** - Stationary workstations
- **Server** - Server hardware
- **Monitor** - Display devices
- **Phone** - Mobile devices
- **Tablet** - Tablet devices
- **Network Equipment** - Routers, switches, firewalls
- **Peripheral** - Keyboards, mice, printers
- **Software License** - Software licensing
- **Other** - Other asset types

## Asset Statuses

| Status | Description |
|--------|-------------|
| **Available** | Asset is available for assignment |
| **In Use** | Asset is currently assigned and active |
| **In Repair** | Asset is being repaired |
| **Retired** | Asset has been retired from service |
| **Lost** | Asset has been lost |
| **Stolen** | Asset has been reported stolen |
| **Disposed** | Asset has been disposed of |

## Asset Conditions

| Condition | Description |
|-----------|-------------|
| **Excellent** | Like new condition |
| **Good** | Normal wear, fully functional |
| **Fair** | Minor wear, functional |
| **Poor** | Significant wear |
| **Damaged** | Physical damage present |

## Data Classification

Assets can be tagged with data classification levels:

| Classification | Description |
|----------------|-------------|
| **Public** | Information intended for public disclosure |
| **Internal** | Information for internal use only |
| **Confidential** | Sensitive business information |
| **Restricted** | Highly sensitive, regulated information |

## Creating an Asset

### Step 1: Navigate to Assets
1. Go to **Assets** in the main navigation
2. Click **Create Asset**

### Step 2: Enter Core Information
1. **Asset Tag** - Enter a unique identifier
2. **Serial Number** - Enter the manufacturer serial number
3. **Name** - Enter a descriptive name
4. **Asset Type** - Select the type classification
5. **Status** - Set the current status

### Step 3: Add Hardware Specifications
Enter relevant hardware details:
- Manufacturer and model
- Processor, RAM, storage specifications
- Network information (MAC, IP, hostname)
- Operating system details

### Step 4: Set Assignment & Location
1. **Assigned To** - Select the user who will use this asset
2. **Department** - Select the department
3. Enter location details (building, floor, room)

### Step 5: Enter Financial Information
1. **Purchase Date** - When the asset was purchased
2. **Purchase Price** - Original cost
3. **Supplier** - Select the vendor
4. Configure depreciation settings if needed

### Step 6: Configure Warranty & Support
1. Set warranty dates and type
2. Enter support contract details
3. Set expiry dates for tracking

### Step 7: Set Security & Compliance
1. **Encryption Enabled** - Toggle if disk encryption is active
2. **Antivirus Installed** - Toggle if AV is installed
3. **Compliance Status** - Set current compliance state
4. **Data Classification** - Set the data sensitivity level

### Step 8: Save
Click **Create** to save the asset.

## Linking Assets to Implementations

Assets can be linked to implementations (controls) to track which security measures apply to specific assets.

### From the Asset Detail Page
1. Open an asset
2. Go to the **Implementations** tab
3. Click **Attach** to add implementations
4. Search and select relevant implementations
5. Save

### From an Implementation
1. Open an implementation
2. Go to the **Assets** tab
3. Click **Attach** to add assets
4. Select assets this implementation covers
5. Save

## Parent-Child Asset Relationships

Assets can have hierarchical relationships for complex equipment:

- A server rack can be a parent to multiple servers
- A workstation bundle can include a desktop, monitor, and peripherals
- Track component assets under their parent asset

To set a parent asset:
1. Edit the child asset
2. Select the **Parent Asset** field
3. Choose the parent asset
4. Save

## Searching and Filtering

### Search
Search assets by:
- Asset tag
- Name
- Serial number
- Manufacturer
- Model

### Filters
Filter the asset list by:
- Asset type
- Status
- Assigned user
- Condition
- Compliance status
- Data classification
- Encryption enabled
- Antivirus installed
- Warranty expiry
- And more

## Requesting an Update

**Request Update**, on an asset's detail page, delegates a review of the record the same way it works for [controls](../foundations/controls.md#approvals-and-delegation) -- assign it to an external portal user for a magic-link review form in [My Portal](../enterprise/my-portal.md#record-update-requests), or to an internal user for a to-do on their To-Do & Approvals page.

## Best Practices

- **Use consistent tagging** - Establish a naming convention for asset tags
- **Keep information current** - Update assignments and locations when assets move
- **Track security status** - Monitor encryption and antivirus status
- **Schedule audits** - Use audit dates to plan regular inventory checks
- **Monitor warranties** - Track warranty expiration to plan replacements
- **Link to implementations** - Connect assets to the controls that protect them
- **Classify data appropriately** - Tag assets with correct data classification levels
- **Document disposal** - Record disposal method and date for compliance
