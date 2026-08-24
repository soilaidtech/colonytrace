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

## UC-002 — Record Waste Collection Trip

### Primary Actor
Operations Manager / Operator

### Goal
Record a vehicle trip undertaken to collect waste for the production facility.

### Preconditions
- The user is authenticated.
- The user has permission to record waste collection trips.
- The vehicle and driver are known.

### Trigger
A vehicle is dispatched to collect waste.

### Basic Flow
1. The user selects **Record Waste Collection Trip**.
2. The user enters the vehicle, driver and waste collection location.
3. The user records the dispatch time.
4. The system creates the trip with a status of **In Progress**.
5. When the vehicle returns, the user opens the active trip.
6. The user records the return time.
7. The user confirms completion of the trip.
8. The system updates the trip status to **Completed**.

### Postconditions
- The waste collection trip is recorded.
- The trip contains its vehicle, driver, collection location, dispatch time and return time.
- A completed trip is available for use when recording waste received.
- Expenses incurred during the trip may be linked to the trip.

### Alternate Flows

**A1 — Trip is cancelled**
1. The user selects the active or scheduled trip.
2. The user marks the trip as cancelled.
3. The system records the trip status as **Cancelled**.

**A2 — Vehicle has not returned**
1. The trip remains **In Progress**.
2. The return time remains empty.
3. The trip may be completed when the vehicle returns.

**A3 — Required information is missing**
1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A4 — Device is offline**
1. The system stores the trip record locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-003 — Record Waste Receiving Event

### Primary Actor
Operations Manager / Operator

### Goal
Record waste received at the production facility from a waste collection trip.

### Preconditions
- The user is authenticated.
- The user has permission to record waste receiving events.
- The associated waste collection trip exists.
- The waste has arrived at the production facility.

### Trigger
Collected waste arrives at the production facility.

### Basic Flow
1. The user selects **Record Waste Receiving Event**.
2. The user selects the associated waste collection trip.
3. The user enters the waste source.
4. The user selects the waste type.
5. The user records the gross weight of the received waste.
6. The user records the contamination level.
7. The user indicates whether the waste is accepted.
8. The user enters any relevant notes.
9. The user submits the record.
10. The system validates the entered information.
11. The system records the waste receiving event and the employee responsible.
12. The system confirms that the waste receiving event was successfully recorded.

### Postconditions
- A waste receiving event is recorded.
- The received waste is traceable to its collection trip.
- Accepted waste is available for subsequent waste sorting.
- Rejected waste remains recorded for traceability but cannot proceed to waste sorting.

### Alternate Flows

**A1 — Waste is rejected**
1. The user marks the waste as not accepted.
2. The user records the reason for rejection.
3. The system records the waste receiving event as rejected.
4. The rejected waste cannot proceed to waste sorting.

**A2 — Required information is missing**
1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A3 — Device is offline**
1. The system stores the waste receiving event locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-004 — Record Waste Sorting Event

### Primary Actor
Operations Manager / Operator

### Goal
Record the sorting of received waste into usable feedstock and other separated waste outputs.

### Preconditions
- The user is authenticated.
- The user has permission to record waste sorting events.
- An accepted waste receiving event exists.
- The received waste is available for sorting.

### Trigger
Received waste is sorted at the production facility.

### Basic Flow
1. The user selects **Record Waste Sorting Event**.
2. The user selects the associated waste receiving event.
3. The user records the sorting date.
4. The user records the weight of usable feedstock.
5. The user records the weight of compostable material.
6. The user records the weight of plastics.
7. The user records the weight of rejected material.
8. The user records the storage container used for the sorted feedstock.
9. The user enters any relevant notes.
10. The user submits the record.
11. The system validates the entered information.
12. The system records the waste sorting event and the employee responsible.
13. The system confirms that the waste sorting event was successfully recorded.

### Postconditions
- A waste sorting event is recorded.
- The sorting event remains traceable to its waste receiving event.
- The quantities of feedstock, compost, plastic and rejected material are recorded separately.
- Usable feedstock is available for creation of a waste batch.

### Alternate Flows

**A1 — No usable feedstock remains after sorting**
1. The user records the feedstock weight as zero.
2. The user records the quantities of the remaining sorted outputs.
3. The system records the sorting event.
4. No waste batch can be created from the sorting event.

**A2 — Required information is missing**
1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A3 — Recorded sorted weight exceeds received waste weight**
1. The system identifies that the combined sorted output exceeds the available received weight.
2. The system prevents submission.
3. The user reviews and corrects the recorded weights.

**A4 — Device is offline**
1. The system stores the waste sorting event locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-005 — Create Waste Batch

### Primary Actor
Operations Manager / Production Manager

### Goal
Create a traceable batch of usable feedstock produced from a completed waste sorting event.

### Preconditions
- The user is authenticated.
- The user has permission to create waste batches.
- A completed waste sorting event exists.
- Usable feedstock is available from the sorting event.

### Trigger
Sorted feedstock is placed into storage and needs to be recorded as a waste batch for future use in feed preparation.

### Basic Flow
1. The user selects **Create Waste Batch**.
2. The user selects the associated waste sorting event.
3. The system displays the feedstock available from the selected sorting event.
4. The user records the weight of the waste batch.
5. The user enters any relevant notes.
6. The user submits the record.
7. The system validates the entered information.
8. The system creates the waste batch and records the employee responsible.
9. The system confirms that the waste batch was successfully created.

### Postconditions
- A waste batch is created.
- The waste batch is traceable to its waste sorting event.
- The waste batch is available for use as a recipe ingredient.
- The available quantity of sorted feedstock is updated accordingly.

### Alternate Flows

**A1 — No usable feedstock is available**
1. The system identifies that the selected sorting event has no usable feedstock available.
2. The system prevents creation of the waste batch.
3. The user selects another sorting event or exits the process.

**A2 — Waste batch weight exceeds available feedstock**
1. The system identifies that the entered batch weight exceeds the feedstock available from the sorting event.
2. The system prevents submission.
3. The user corrects the batch weight.

**A3 — Required information is missing**
1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A4 — Device is offline**
1. The system stores the waste batch locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-006 — Create Recipe

### Primary Actor
Production Manager

### Goal
Record a feed mixture prepared from one or more ingredients for feeding nursery or larvae batches.

### Preconditions
- The user is authenticated.
- The user has permission to create recipes.
- The ingredients required for the recipe are available.
- Any waste-derived ingredient that requires traceability has an existing waste batch.

### Trigger
Ingredients are mixed to prepare feed for a nursery or larvae batch.

### Basic Flow
1. The user selects **Create Recipe**.
2. The user enters the recipe name.
3. The user adds each ingredient used in the mixture.
4. For each ingredient, the user records the ingredient name and weight.
5. For a waste-derived ingredient, the user selects the associated waste batch.
6. For a non-waste ingredient, the user records the ingredient without a waste batch reference.
7. The system calculates the total recipe weight from the recorded ingredient weights.
8. The user reviews the recipe and enters any relevant notes.
9. The user submits the recipe.
10. The system validates the entered information.
11. The system creates the recipe and its recipe ingredient records.
12. The system records the employee responsible.
13. The system confirms that the recipe was successfully created.

### Postconditions
- A recipe is created.
- All ingredients and their respective weights are recorded.
- Waste-derived ingredients remain traceable to their source waste batches.
- The recipe is available for use in feeding events.

### Alternate Flows

**A1 — Ingredient is not derived from a waste batch**
1. The user enters the ingredient name and weight.
2. No waste batch is selected.
3. The ingredient is recorded as part of the recipe.

**A2 — Insufficient quantity exists in a selected waste batch**
1. The system identifies that the requested ingredient weight exceeds the available quantity.
2. The system prevents submission.
3. The user adjusts the ingredient quantity or selects another waste batch.

**A3 — Required information is missing**
1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the recipe again.

**A4 — Device is offline**
1. The system stores the recipe and its ingredients locally.
2. The records are marked as pending synchronization.
3. The system synchronizes the records when connectivity becomes available.

## UC-007 — Record Breeding Batch

### Primary Actor
Production Manager

### Goal
Record a batch of prepupae introduced into a breeding cage for reproduction.

### Preconditions
- The user is authenticated.
- The user has permission to record breeding batches.
- The breeding cage exists and is available for use.
- The prepupae to be introduced into the breeding cage are available.

### Trigger
A batch of prepupae is introduced into a breeding cage.

### Basic Flow
1. The user selects **Record Breeding Batch**.
2. The user selects the breeding cage receiving the batch.
3. The user records the start date.
4. The user records the weight of the prepupae.
5. The user identifies the batch source as **Internal** or **External**.
6. The user enters any relevant notes.
7. The user submits the record.
8. The system validates the entered information.
9. The system creates the breeding batch with an **Active** status.
10. The system records the employee responsible.
11. The system confirms that the breeding batch was successfully recorded.

### Postconditions
- A breeding batch is recorded.
- The breeding batch is associated with its breeding cage.
- The source and initial prepupae weight are recorded.
- The breeding batch is available as part of the breeding cage's production history.

### Alternate Flows

**A1 — Breeding batch originates from an external source**
1. The user selects **External** as the source.
2. The user records the prepupae weight.
3. The system creates the breeding batch without requiring an internal production source.

**A2 — Breeding cage is unavailable**
1. The system identifies that the selected cage is unavailable or under maintenance.
2. The system prevents the breeding batch from being assigned to the cage.
3. The user selects an available breeding cage.

**A3 — Required information is missing**
1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A4 — Device is offline**
1. The system stores the breeding batch locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.