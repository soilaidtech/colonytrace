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
