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

## UC-008 — Record Egg Collection

### Primary Actor

Production Manager / Operator

### Goal

Record BSFL eggs collected from a breeding cage using an eggie and make the collected eggs available for nursery production.

### Preconditions

- The user is authenticated.
- The user has permission to record egg collection events.
- The breeding cage exists and contains active breeding batches.
- An eggie has been placed in the breeding cage.

### Trigger

A full eggie is removed from a breeding cage for collection and transfer to the nursery.

### Basic Flow

1. The user selects **Record Egg Collection**.
2. The user selects the breeding cage.
3. The user records the eggie placement date.
4. The user records the eggie collection date.
5. The user records the empty eggie weight.
6. The user records the full eggie weight.
7. The system calculates the egg weight as the difference between the full and empty eggie weights.
8. The user enters any relevant notes.
9. The user submits the record.
10. The system validates the entered information.
11. The system records the egg collection event and the employee responsible.
12. The system confirms that the egg collection event was successfully recorded.

### Postconditions

- An egg collection event is recorded.
- The collected eggs are traceable to the breeding cage.
- The calculated egg weight is available for nursery tracking.
- The egg collection event is available for creation of a nursery batch.

### Alternate Flows

**A1 — Full eggie weight is not greater than empty eggie weight**

1. The system identifies the invalid weight values.
2. The system prevents submission.
3. The user verifies and corrects the recorded weights.

**A2 — Eggie collection date is earlier than placement date**

1. The system identifies the invalid date sequence.
2. The system prevents submission.
3. The user corrects the dates.

**A3 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A4 — Device is offline**

1. The system stores the egg collection event locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-009 — Create Nursery Batch

### Primary Actor

Production Manager

### Goal

Create a nursery batch from collected BSFL eggs and track the batch through hatching and early larval development.

### Preconditions

- The user is authenticated.
- The user has permission to create nursery batches.
- A valid egg collection event exists.
- The collected eggs are available for transfer to the nursery.

### Trigger

Collected eggs are placed in the nursery for hatching.

### Basic Flow

1. The user selects **Create Nursery Batch**.
2. The user selects the associated egg collection event.
3. The user records the nursery batch start date.
4. The user enters any relevant notes.
5. The user submits the record.
6. The system validates the entered information.
7. The system creates the nursery batch with an **Active** status.
8. The system records the employee responsible.
9. The system confirms that the nursery batch was successfully created.

### Postconditions

- A nursery batch is created.
- The nursery batch is traceable to its egg collection event.
- The nursery batch is available for feeding events.
- The nursery batch is available for creation of one or more larvae batches when the neonates are ready for transfer.

### Alternate Flows

**A1 — Egg collection event is unavailable or invalid**

1. The system prevents creation of the nursery batch.
2. The user selects a valid egg collection event or exits the process.

**A2 — Nursery batch is rejected**

1. The user updates the nursery batch status to **Inactive** or the appropriate rejected status.
2. The batch cannot be used to create larvae batches.

**A3 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A4 — Device is offline**

1. The system stores the nursery batch locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-010 — Create Larvae Batch

### Primary Actor

Production Manager

### Goal

Create a larvae batch when larvae are transferred from a nursery batch or received from an external source and placed into a production basin.

### Preconditions

- The user is authenticated.
- The user has permission to create larvae batches.
- A production basin or container is available.
- For internally produced larvae, an active nursery batch exists.
- For externally sourced larvae, the larvae have been received at the production facility.

### Trigger

Larvae are placed into a production basin for growth and feeding.

### Basic Flow

1. The user selects **Create Larvae Batch**.
2. The user selects the batch source as **Internal** or **External**.
3. For an internal batch, the user selects the source nursery batch.
4. The user selects or enters the production basin/container identifier.
5. The user records the initial larvae weight.
6. The user records the batch start date.
7. The user enters any relevant notes.
8. The user submits the record.
9. The system validates the entered information.
10. The system creates the larvae batch with an **Active** status.
11. The system records the employee responsible.
12. The system confirms that the larvae batch was successfully created.

### Postconditions

- A larvae batch is created.
- The larvae batch is associated with its production basin/container.
- An internally produced larvae batch remains traceable to its nursery batch.
- An externally sourced larvae batch is identified as externally sourced.
- The larvae batch is available for feeding and subsequent harvesting.

### Alternate Flows

**A1 — Larvae originate from an external source**

1. The user selects **External** as the batch source.
2. A nursery batch is not required.
3. The user records the initial larvae weight and production basin/container.
4. The system creates the larvae batch as externally sourced.

**A2 — One nursery batch is divided across multiple basins**

1. The user selects the same nursery batch as the source.
2. The user creates a separate larvae batch for each production basin.
3. Each larvae batch receives its own identifier and container identifier.
4. All created larvae batches remain traceable to the same nursery batch.

**A3 — Production basin/container is unavailable**

1. The system identifies that the selected container is unavailable for a new larvae batch.
2. The system prevents the batch from being assigned to that container.
3. The user selects an available container.

**A4 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A5 — Device is offline**

1. The system stores the larvae batch locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-011 — Record Feeding Event

### Primary Actor

Production Manager / Operator

### Goal

Record feed provided to an active larvae batch or nursery batch.

### Preconditions

- The user is authenticated.
- The user has permission to record feeding events.
- An active larvae batch or nursery batch exists.
- A prepared recipe exists and is available for feeding.

### Trigger

A larvae batch or nursery batch requires feeding or a feed top-up.

### Basic Flow

1. The user selects **Record Feeding Event**.
2. The user selects whether the feed is being provided to a larvae batch or nursery batch.
3. The user selects the active batch being fed.
4. The user selects the recipe being used.
5. The user records the current larvae weight where applicable.
6. The user records the weight of feed provided.
7. The system calculates the feeding ratio.
8. The user records the feeding date.
9. The user enters any relevant notes.
10. The user submits the record.
11. The system validates the entered information.
12. The system records the feeding event and the employee responsible.
13. The system confirms that the feeding event was successfully recorded.

### Postconditions

- A feeding event is recorded.
- The feeding event is associated with one larvae batch or one nursery batch.
- The feed provided is traceable to the recipe used.
- The quantity of feed provided and feeding ratio are recorded.
- The batch's feeding history is updated.

### Alternate Flows

**A1 — Nursery batch is being fed**

1. The user selects a nursery batch instead of a larvae batch.
2. The system associates the feeding event with the selected nursery batch.
3. No larvae batch is associated with the feeding event.

**A2 — Selected batch is not active**

1. The system identifies that the selected batch is not active.
2. The system prevents the feeding event from being recorded.
3. The user selects an active batch or exits the process.

**A3 — Recipe is unavailable**

1. The system identifies that the selected recipe is unavailable for feeding.
2. The system prevents submission.
3. The user selects another available recipe or records the required recipe before continuing.

**A4 — Feed weight is invalid**

1. The system identifies that the feed weight is zero, negative or otherwise invalid.
2. The system prevents submission.
3. The user corrects the feed weight.

**A5 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A6 — Device is offline**

1. The system stores the feeding event locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-012 — Record Harvest Event

### Primary Actor

Production Manager / Operator

### Goal

Record the harvesting of a larvae batch from its production basin or container.

### Preconditions

- The user is authenticated.
- The user has permission to record harvest events.
- The larvae batch exists.
- The larvae batch is active.

### Trigger

A larvae batch is ready to be harvested.

### Basic Flow

1. The user selects **Record Harvest Event**.
2. The system displays active larvae batches.
3. The user selects the larvae batch being harvested.
4. The system displays the selected batch and its basin/container identifier.
5. The user records the harvest date.
6. The user records the harvest reason.
7. The user enters any relevant notes.
8. The user submits the record.
9. The system validates the entered information.
10. The system creates the harvest event and records the employee responsible.
11. The system confirms that the harvest event was successfully recorded.
12. The harvest event becomes available for inclusion in a harvest batch.

### Postconditions

- A harvest event is recorded for the selected larvae batch.
- The harvest event remains traceable to the larvae batch and its production basin/container.
- The harvest event is available for inclusion in a harvest batch.
- The larvae batch's harvest history is updated.

### Alternate Flows

**A1 — Multiple larvae batches are harvested**

1. The user selects each larvae batch being harvested.
2. The system creates a separate harvest event for each larvae batch.
3. The individual harvest events may subsequently be pooled into the same harvest batch.

**A2 — Larvae batch is not active**

1. The system identifies that the selected larvae batch is not active.
2. The system prevents the harvest event from being recorded.
3. The user selects an active larvae batch or exits the process.

**A3 — Larvae batch is partially harvested**

1. The user records the harvest event.
2. The larvae batch remains active because larvae remain in the production basin.
3. Additional harvest events may be recorded against the same larvae batch later.

**A4 — Larvae batch is fully harvested**

1. The user records the harvest event.
2. The user indicates that the larvae batch has been fully harvested.
3. The system marks the larvae batch as completed.
4. No further feeding or harvest events may be recorded against the completed larvae batch.

**A5 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A6 — Device is offline**

1. The system stores the harvest event locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-013 — Create Harvest Batch

### Primary Actor

Production Manager

### Goal

Create a pooled harvest batch from one or more completed harvest events and record the quantities of material produced.

### Preconditions

- The user is authenticated.
- The user has permission to create harvest batches.
- One or more completed harvest events exist.
- The selected harvest events have not already been assigned to another harvest batch.
- Harvested material from the selected events has been physically pooled and weighed.

### Trigger

Material from one or more harvest events is pooled and weighed after harvesting.

### Basic Flow

1. The user selects **Create Harvest Batch**.
2. The system displays completed harvest events that have not yet been assigned to a harvest batch.
3. The user selects the harvest events whose harvested material has been pooled.
4. The system displays the larvae batches associated with the selected harvest events.
5. The user records the wet larvae weight.
6. The user records the prepupae weight.
7. The user records the frass weight.
8. The user records the reject weight.
9. The user enters any relevant notes.
10. The user submits the record.
11. The system validates the entered information.
12. The system creates the harvest batch.
13. The system associates the selected harvest events with the harvest batch.
14. The system confirms that the harvest batch was successfully created.

### Postconditions

- A harvest batch is created.
- The harvest batch is traceable to all harvest events that contributed to it.
- Each contributing harvest event is traceable to its original larvae batch.
- Wet larvae, prepupae, frass and reject quantities are recorded separately.
- The wet larvae are available for subsequent drying events.
- Frass is available for subsequent product processing where applicable.
- The selected harvest events cannot be assigned to another harvest batch.

### Alternate Flows

**A1 — Only one harvest event contributes to the harvest batch**

1. The user selects one completed harvest event.
2. The user records the resulting harvest quantities.
3. The system creates the harvest batch from that single harvest event.

**A2 — Selected harvest event already belongs to another harvest batch**

1. The system identifies that the harvest event has already been assigned.
2. The system prevents the event from being added to the new harvest batch.
3. The user removes the event or selects another eligible harvest event.

**A3 — Invalid harvest weight is entered**

1. The system identifies a negative or otherwise invalid weight.
2. The system prevents submission.
3. The user corrects the recorded weight.

**A4 — No harvest events are selected**

1. The system prevents creation of the harvest batch.
2. The system informs the user that at least one harvest event must be selected.
3. The user selects one or more eligible harvest events.

**A5 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A6 — Device is offline**

1. The system stores the harvest batch and its harvest-event associations locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the records when connectivity becomes available.

## UC-014 — Record Drying Event

### Primary Actor

Production Manager / Operator

### Goal

Record the drying of wet larvae from a harvest batch in a single drying oven.

### Preconditions

- The user is authenticated.
- The user has permission to record drying events.
- A harvest batch exists.
- Wet larvae are available in the selected harvest batch.
- A drying oven is available for use.

### Trigger

Wet larvae from a harvest batch are loaded into an oven for drying.

### Basic Flow

1. The user selects **Record Drying Event**.
2. The user selects the source harvest batch.
3. The system displays the wet larvae quantity available for drying.
4. The user selects or enters the oven/dryer identifier.
5. The user records the wet larvae input weight.
6. The user records the drying start time.
7. When drying is completed, the user opens the drying event.
8. The user records the stop time.
9. The user records the dried larvae output weight.
10. The user records the moisture content.
11. The system calculates the drying duration.
12. The user enters any relevant notes.
13. The user submits the completed drying event.
14. The system validates the entered information.
15. The system records the employee responsible.
16. The system confirms that the drying event was successfully completed.

### Postconditions

- A drying event is recorded.
- The drying event is traceable to its source harvest batch.
- Wet input weight and dried output weight are recorded.
- Drying duration and moisture content are recorded.
- The amount of wet larvae remaining available for drying from the harvest batch is updated.
- The completed drying event is available for inclusion in a dried larvae batch.

### Alternate Flows

**A1 — Harvest batch is split across multiple ovens**

1. The user creates a separate drying event for each oven used.
2. Each drying event references the same source harvest batch.
3. The system tracks the wet input allocated to each drying event.
4. The combined wet input cannot exceed the wet larvae available in the harvest batch.

**A2 — Drying is still in progress**

1. The drying event remains in progress after the start time is recorded.
2. Output weight, stop time and final moisture content remain incomplete.
3. The user returns to the drying event when the drying cycle is completed.
4. The user records the remaining information and completes the event.

**A3 — Wet input exceeds available harvest quantity**

1. The system identifies that the entered wet input exceeds the wet larvae available in the harvest batch.
2. The system prevents submission.
3. The user corrects the wet input weight.

**A4 — Dried output exceeds wet input**

1. The system identifies that the dried output weight exceeds the wet input weight.
2. The system prevents completion of the drying event.
3. The user verifies and corrects the recorded weights.

**A5 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents completion of the drying event.
3. The user provides the required information and submits the record again.

**A6 — Device is offline**

1. The system stores the drying event locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-015 — Create Dried Larvae Batch

### Primary Actor

Production Manager

### Goal

Create a pooled batch of dried larvae from one or more completed drying events.

### Preconditions

- The user is authenticated.
- The user has permission to create dried larvae batches.
- One or more completed drying events exist.
- The selected drying events have not already been assigned to another dried larvae batch.
- Dried larvae from the selected drying events have been physically pooled.

### Trigger

Dried larvae from one or more completed drying events are pooled after drying.

### Basic Flow

1. The user selects **Create Dried Larvae Batch**.
2. The system displays completed drying events that have not yet been assigned to a dried larvae batch.
3. The user selects the drying events whose dried larvae have been pooled.
4. The system displays the dried output weight from each selected drying event.
5. The system calculates the combined dried output weight.
6. The user records the actual total weight of the pooled dried larvae.
7. The user records the batch date.
8. The user enters any relevant notes.
9. The user submits the record.
10. The system validates the entered information.
11. The system creates the dried larvae batch.
12. The system associates the selected drying events with the dried larvae batch.
13. The system records the employee responsible.
14. The system confirms that the dried larvae batch was successfully created.

### Postconditions

- A dried larvae batch is created.
- The dried larvae batch is traceable to all drying events that contributed to it.
- The total dried larvae weight is recorded.
- The selected drying events cannot be assigned to another dried larvae batch.
- The dried larvae batch is available for creation of a product batch.

### Alternate Flows

**A1 — Only one drying event contributes to the batch**

1. The user selects one completed drying event.
2. The user records the pooled dried larvae weight.
3. The system creates the dried larvae batch from the single drying event.

**A2 — Selected drying event already belongs to another dried larvae batch**

1. The system identifies that the drying event has already been assigned.
2. The system prevents the drying event from being added.
3. The user removes the drying event or selects another eligible drying event.

**A3 — Recorded total weight exceeds combined drying output**

1. The system identifies that the recorded dried larvae batch weight exceeds the combined output of the selected drying events.
2. The system prevents submission.
3. The user verifies the selected drying events and recorded weight.

**A4 — No drying events are selected**

1. The system prevents creation of the dried larvae batch.
2. The system informs the user that at least one completed drying event must be selected.
3. The user selects one or more eligible drying events.

**A5 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A6 — Device is offline**

1. The system stores the dried larvae batch and its drying-event associations locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the records when connectivity becomes available.

## UC-016 — Create Product Batch

### Primary Actor

Production Manager

### Goal

Create a traceable batch of a defined product from a completed production output.

### Preconditions

- The user is authenticated.
- The user has permission to create product batches.
- The product exists in the system.
- The appropriate source batch exists and is available for product creation.
- For dried larvae products, a dried larvae batch exists.
- For frass products, a harvest batch exists.

### Trigger

A production output is ready to be recorded as a defined product.

### Basic Flow

1. The user selects **Create Product Batch**.
2. The user selects the product being produced.
3. The system determines the required source type based on the selected product.
4. The user selects the appropriate source batch.
5. The user records the production date.
6. The user records the quantity produced.
7. The user records the packaging status.
8. The user records the product batch expiry date where applicable.
9. The user enters any relevant notes.
10. The user submits the record.
11. The system validates the entered information.
12. The system creates the product batch.
13. The system records the quantity available.
14. The system records the employee responsible.
15. The system confirms that the product batch was successfully created.

### Postconditions

- A product batch is created.
- The product batch is associated with its defined product.
- The product batch remains traceable to its production source.
- The quantity produced and quantity available are recorded.
- The product batch is available for inventory movements and sales.

### Alternate Flows

**A1 — Dried larvae product is being created**

1. The user selects a dried larvae product.
2. The system requires the user to select a dried larvae batch.
3. The product batch is linked to the selected dried larvae batch.

**A2 — Frass product is being created**

1. The user selects a frass product.
2. The system requires the user to select a harvest batch.
3. The product batch is linked to the selected harvest batch.

**A3 — Quantity produced exceeds available source quantity**

1. The system identifies that the entered quantity exceeds the quantity available from the selected source batch.
2. The system prevents submission.
3. The user verifies the source batch or corrects the quantity produced.

**A4 — Incorrect source type is selected**

1. The system identifies that the selected source is incompatible with the product type.
2. The system prevents submission.
3. The user selects the appropriate source batch.

**A5 — Product is not yet packaged**

1. The user records the packaging status as **Unpackaged** or **In Progress**.
2. The system creates the product batch with the selected packaging status.
3. The packaging status may be updated when packaging is completed.

**A6 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A7 — Device is offline**

1. The system stores the product batch locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-017 — Record Inventory Movement

### Primary Actor

Operations Manager

### Goal

Record any movement that increases, decreases, or transfers finished product inventory.

### Preconditions

- The user is authenticated.
- The user has permission to record inventory movements.
- The product batch exists.
- The quantity being moved is available where required.

### Trigger

A product batch is added to inventory, removed from inventory, or transferred.

### Basic Flow

1. The user selects **Record Inventory Movement**.
2. The user selects the product batch.
3. The user selects the movement type.
4. The user records the quantity moved.
5. The user records the movement date.
6. The user enters the reason for the movement.
7. The user enters any relevant notes.
8. The user submits the record.
9. The system validates the entered information.
10. The system records the inventory movement and the employee responsible.
11. The system updates the available quantity of the product batch.
12. The system confirms that the inventory movement was successfully recorded.

### Postconditions

- An inventory movement is recorded.
- The movement is traceable to the relevant product batch.
- The available quantity of the product batch is updated.
- The inventory history reflects the movement.

### Alternate Flows

**A1 — Inventory is added**

1. The user selects **Addition** as the movement type.
2. The system increases the available quantity of the selected product batch.

**A2 — Inventory is removed**

1. The user selects **Removal** as the movement type.
2. The system verifies that sufficient quantity is available.
3. The system decreases the available quantity of the selected product batch.

**A3 — Inventory is transferred**

1. The user selects **Transfer** as the movement type.
2. The user records the quantity being transferred.
3. The system records the transfer without changing the total quantity of the product batch.

**A4 — Quantity exceeds available inventory**

1. The system identifies that the requested removal quantity exceeds the available inventory.
2. The system prevents submission.
3. The user corrects the quantity.

**A5 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A6 — Device is offline**

1. The system stores the inventory movement locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-018 — Record Customer Sale

### Primary Actor

Operations Manager

### Goal

Record the sale of a product from an available product batch to a customer.

### Preconditions

- The user is authenticated.
- The user has permission to record customer sales.
- The customer exists in the system.
- The product batch exists.
- Sufficient product quantity is available for sale.

### Trigger

A customer purchases a product from SoilAid Technologies.

### Basic Flow

1. The user selects **Record Customer Sale**.
2. The user selects the customer.
3. The user selects the product batch being sold.
4. The system displays the product and quantity available from the selected batch.
5. The user records the quantity sold.
6. The user records the unit price.
7. The system calculates the total sale amount.
8. The user records the sale date.
9. The user selects the payment status.
10. The user enters any relevant notes.
11. The user submits the sale.
12. The system validates the entered information.
13. The system records the sale and the employee responsible.
14. The system reduces the available inventory for the product batch by the quantity sold.
15. The system confirms that the sale was successfully recorded.

### Postconditions

- A customer sale is recorded.
- The sale is traceable to the customer and product batch.
- The quantity sold, unit price and total sale amount are recorded.
- The available quantity of the product batch is reduced by the quantity sold.
- The payment status of the sale is recorded.
- The sale contributes to revenue reporting.

### Alternate Flows

**A1 — Customer has not been recorded**

1. The system cannot find the customer.
2. The user creates the customer record.
3. The user returns to the sale and selects the newly created customer.

**A2 — Quantity sold exceeds available inventory**

1. The system identifies that the requested quantity exceeds the available product quantity.
2. The system prevents submission.
3. The user corrects the quantity sold or selects another product batch.

**A3 — Sale has not been paid**

1. The user records the payment status as **Unpaid** or **Pending**.
2. The system records the sale without marking the payment as completed.
3. The payment status may be updated when payment is received.

**A4 — Invalid price or quantity**

1. The system identifies that the unit price or quantity sold is zero, negative or otherwise invalid.
2. The system prevents submission.
3. The user corrects the invalid value.

**A5 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the sale again.

**A6 — Device is offline**

1. The system stores the sale locally.
2. The system reserves the sold quantity locally to prevent it from being sold again on the same device.
3. The record is marked as pending synchronization.
4. The system synchronizes the sale when connectivity becomes available.
5. If synchronization identifies an inventory conflict, the system flags the sale for review.

## UC-019 — Record Expense

### Primary Actor

Operations Manager

### Goal

Record a cost incurred during production or other site operations for cost tracking and reporting.

### Preconditions

- The user is authenticated.
- The user has permission to record expenses.
- The expense has been incurred.

### Trigger

Money is spent or a financial obligation is incurred during production or site operations.

### Basic Flow

1. The user selects **Record Expense**.
2. The user records the expense date.
3. The user selects the expense category.
4. The user enters the amount.
5. The user enters a description of the expense.
6. Where applicable, the user associates the expense with the relevant operational activity.
7. The user enters any relevant notes.
8. The user submits the record.
9. The system validates the entered information.
10. The system records the expense and the employee responsible.
11. The system confirms that the expense was successfully recorded.

### Postconditions

- An expense is recorded.
- The expense is assigned to an expense category.
- Where applicable, the expense is traceable to the operational activity that incurred the cost.
- The expense is available for cost and profitability reporting.

### Alternate Flows

**A1 — Expense is directly attributable to an operational activity**

1. The user selects the relevant operational activity.
2. The system associates the expense with that activity.
3. The expense becomes available for calculating the cost of that activity.

**A2 — Expense is a general operational expense**

1. The user records the expense without associating it with a specific production activity.
2. The system records it as a general operational expense.

**A3 — Expense category is Other**

1. The user selects **Other** as the expense category.
2. The user provides a description identifying the nature of the expense.
3. The system records the expense.

**A4 — Invalid expense amount**

1. The system identifies that the amount is zero, negative or otherwise invalid.
2. The system prevents submission.
3. The user corrects the amount.

**A5 — Required information is missing**

1. The system identifies the missing required information.
2. The system prevents submission.
3. The user provides the required information and submits the record again.

**A6 — Device is offline**

1. The system stores the expense locally.
2. The record is marked as pending synchronization.
3. The system synchronizes the record when connectivity becomes available.

## UC-020 — View Production Dashboard

### Primary Actor

Director / Operations Manager / Production Manager

### Goal

View summarized production, operational, financial and traceability information to monitor the performance of the production facility.

### Preconditions

- The user is authenticated.
- The user has permission to view the dashboard.
- Production or operational data has been recorded in ColonyTrace.

### Trigger

The user opens the production dashboard.

### Basic Flow

1. The user selects **Production Dashboard**.
2. The system retrieves available production, inventory, sales and expense data.
3. The system displays key production metrics.
4. The system displays waste collection and processing metrics.
5. The system displays larvae production and harvest metrics.
6. The system displays drying and finished-product metrics.
7. The system displays current product inventory.
8. The system displays sales and revenue information.
9. The system displays operational expense information.
10. The user selects a date range or other available filters.
11. The system updates the dashboard using the selected filters.
12. The user reviews the displayed information.

### Postconditions

- No production records are modified.
- The user has access to summarized operational and financial information based on their permissions.
- Dashboard information remains traceable to the underlying production records.

### Alternate Flows

**A1 — No data exists for the selected period**

1. The system identifies that no records exist for the selected period.
2. The system displays an empty state.
3. The user may select another date range.

**A2 — Some records have not synchronized**

1. The system displays the most recently synchronized data.
2. The system indicates that some locally recorded information may not yet be included in the dashboard.
3. The dashboard updates after synchronization is completed.

**A3 — User has restricted permissions**

1. The system determines the user's role and permissions.
2. The system displays only the dashboard information the user is authorised to view.

**A4 — Device is offline**

1. The system displays dashboard information available from locally stored data.
2. The system indicates when the displayed information was last synchronized.
3. Data requiring server-side aggregation may remain unavailable until connectivity is restored.
