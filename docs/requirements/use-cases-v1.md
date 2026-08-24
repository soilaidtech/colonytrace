# COLONYTRACE USE CASE SPECIFICATION

## 1. SYSTEM DESCRIPTION

ColonyTrace is a production traceability system used by SoilAid Technologies
to record and monitor BSFL production activities from waste collection through
production, processing, inventory and sales.

The operational application will be used on Android devices at the production
site and must support offline data entry and local storage, with synchronization
when connectivity becomes available.

## 2. PRIMARY ACTORS

Operations Manager

Production Manager

Operator

## 3. SECONDARY ACTORS

Directors
SoilAid Technologies management

## 4. SYSTEM GOALS

ColonyTrace shall enable users to:

- Record waste collection trips.
- Record waste received and sorted.
- Track waste batches used in feed preparation.
- Record feed recipes and recipe ingredients.
- Track breeding batches and egg collection.
- Track nursery and larvae batches.
- Record feeding events.
- Record harvest events and pooled harvest batches.
- Record drying events and dried larvae batches.
- Create product batches.
- Track inventory movements.
- Record customer sales.
- Record operational expenses.
- Provide traceability across the waste-to-protein production process.

## 5. GLOBAL PRECONDITIONS

- The user must have an active ColonyTrace account.
- The user must be authenticated.
- The user must have permission to perform the requested operation.

## 6. SYSTEM CONSTRAINTS

- The operational application must run on Android devices.
- Core production records must be creatable without internet connectivity.
- Offline records must be stored locally until synchronization is possible.
- Synchronization must preserve record integrity and prevent duplicate records.

## 7. USE-CASE CATALOGUE

| ID     | Use Case                     | Primary Actor                           |
| ------ | ---------------------------- | --------------------------------------- |
| UC-001 | Log In                       | All users                               |
| UC-002 | Record Waste Collection Trip | Operations Manager / Operator           |
| UC-003 | Record Waste Receiving Event | Operations Manager / Operator           |
| UC-004 | Record Waste Sorting Event   | Operations Manager / Operator           |
| UC-005 | Create Waste Batch           | Operations Manager / Production Manager |
| UC-006 | Create Recipe                | Production Manager                      |
| UC-007 | Record Breeding Batch        | Production Manager                      |
| UC-008 | Record Egg Collection        | Production Manager / Operator           |
| UC-009 | Create Nursery Batch         | Production Manager                      |
| UC-010 | Create Larvae Batch          | Production Manager                      |
| UC-011 | Record Feeding Event         | Production Manager / Operator           |
| UC-012 | Record Harvest Event         | Production Manager / Operator           |
| UC-013 | Create Harvest Batch         | Production Manager                      |
| UC-014 | Record Drying Event          | Production Manager / Operator           |
| UC-015 | Create Dried Larvae Batch    | Production Manager                      |
| UC-016 | Create Product Batch         | Production Manager                      |
| UC-017 | Record Inventory Movement    | Operations Manager                      |
| UC-018 | Record Customer Sale         | Operations Manager                      |
| UC-019 | Record Expense               | Operations Manager                      |
| UC-020 | View Production Dashboard    | Director / Managers                     |

8. USE-CASES


### UC-001 - User Login

All users

#### Goal

Allow an authorised ColonyTrace user to access the system.

#### Preconditions

The user has an active ColonyTrace account.
The application is installed on the device.

#### Trigger

The user opens ColonyTrace and attempts to access the system.

#### Basic Flow

The system displays the login screen.
The user enters their login credentials.
The user submits the login request.
The system validates the credentials.
The system authenticates the user.
The system loads the interface and permissions associated with the user's role.
The user is granted access to ColonyTrace.

#### Postconditions

The user is authenticated.
The user has access only to features permitted by their assigned role.

#### Alternate Flows

**A1 — Invalid credentials**

The system rejects the login attempt.
The system displays an invalid credentials message.
The user may retry.

**A2 — Inactive account**

The system identifies the account as inactive.
Access is denied.
The user is instructed to contact an authorised administrator.

**A3 — Device is offline**

The system attempts to authenticate using locally stored authorised session credentials.
If a valid offline session exists, access is granted with offline functionality.
If no valid offline session exists, the system informs the user that internet access is required for authentication.