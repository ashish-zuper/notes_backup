# Amway Job Creation Process Flow

## Overview
This is an Angular component that handles the creation of jobs in the Amway system. It involves multiple steps including asset management, customer management, and job creation. The process is divided into two main pages with various sub-processes.

## Step 1: Asset Management

### 1.1 Product Search
- **Action**: User enters a product SKU
- **Process**:
  - System searches for the product using the SKU
  - Validates if the product exists
  - Checks if the product is serialized
- **Expected Output**:
  - If product found: Product details are populated
  - If product not found: Error message displayed
- **Next Step**:
  - If product is serialized: Proceed to asset serial number input
  - If not serialized: Proceed to customer details

### 1.2 Asset Serial Number Search
- **Action**: User enters asset serial number
- **Process**:
  - System searches for the asset in both Zuper and GWMS systems
  - Compares asset details from both systems
- **Possible Scenarios**:
  1. **Asset Found in Both Systems**
     - Shows comparison popup
     - User can choose to:
       - Update existing asset
       - Create new asset
       - Select existing asset
  2. **Asset Found Only in GWMS**
     - Shows asset details
     - User can choose to create new asset
  3. **Asset Found Only in Zuper**
     - Shows asset details
     - User can choose to select or update asset
  4. **Asset Not Found**
     - Shows error message
     - User can choose to create new asset
- **Next Step**: Proceed to customer details

## Step 2: Customer Management

### 2.1 Customer Search
- **Action**: User searches for customer using:
  - Customer name (Zuper search)
  - ABO number (MDMS search)
- **Process**:
  - System searches in both Zuper and MDMS systems
  - Displays matching customers
- **Expected Output**:
  - List of matching customers
  - Customer details including address information

### 2.2 Customer Selection
- **Action**: User selects a customer
- **Process**:
  - System compares customer details between Zuper and MDMS
  - Shows comparison popup
- **Possible Scenarios**:
  1. **Customer Found in Both Systems**
     - User can choose to:
       - Select existing customer
       - Update customer details
  2. **Customer Found Only in MDMS**
     - User can create new customer
  3. **Customer Found Only in Zuper**
     - User can update customer
  4. **Customer Not Found**
     - User can create new customer

### 2.3 Address Selection
- **Action**: User selects customer address
- **Process**:
  - System displays available addresses
  - User selects appropriate address
- **Expected Output**:
  - Selected address details populated in form
  - Option to copy address to billing address

## Step 3: Job Creation

### 3.1 Form Validation
- **Action**: System validates all entered information
- **Process**:
  - Checks required fields
  - Validates asset and customer information
- **Expected Output**:
  - If valid: Proceeds to job creation
  - If invalid: Shows error messages

### 3.2 Job Creation
- **Action**: System creates the job
- **Process**:
  - Creates/updates customer if needed
  - Creates/updates asset if needed
  - Creates the job record
- **Expected Output**:
  - Success message if job created
  - Error message if creation fails

## Error Handling

### Asset Errors
- Invalid serial number
- Product not found
- Asset not found
- System errors during asset creation/update

### Customer Errors
- Invalid ABO number
- Customer not found
- Address validation errors
- System errors during customer creation/update

## State Management

### Asset States
- `CREATE`: New asset needs to be created
- `UPDATE`: Existing asset needs to be updated
- `SELECTED`: Existing asset selected
- `INVALID`: Invalid asset state
- `NOT_FOUND`: Asset not found
- `SKIP`: Skip asset creation

### Customer States
- `CREATE`: New customer needs to be created
- `UPDATE`: Existing customer needs to be updated
- `SELECTED`: Existing customer selected
- `INVALID`: Invalid customer state
- `SKIP`: Skip customer creation

## Navigation Flow

1. Start with product search
2. If product is serialized, proceed to asset search
3. After asset management, proceed to customer search
4. After customer management, proceed to job creation
5. Each step has validation and error handling
6. User can navigate back and forth between steps

## API Integration

The component integrates with multiple systems:
- Zuper system for asset and customer management
- GWMS system for asset information
- MDMS system for customer information

Each system call includes proper error handling and loading states to ensure a smooth user experience.

This process flow ensures that all necessary information is collected and validated before creating a job, while maintaining data consistency across different systems.
