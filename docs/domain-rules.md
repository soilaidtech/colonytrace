# ColonyTrace Domain Rules

## Purpose

This document defines the business concepts, lifecycle, and rules that govern the ColonyTrace production system. It serves as the reference for developers, designers, testers and stakeholders before implementation.

## Domain: Waste Operations

### Entity: Trip

#### Definition

A trip represents one vehicle dispatch for collecting waste from supplier or source

#### Created By

Operations Manager or Production Manager

#### Created When

A vehicle arrives to the production site

#### Ends When

All waste has been received and vehicle returns

#### Business Rules

- A trip may visit multiple waste sources
- Every Waste Receiving Event must belong to one Trip
- A completed trip cannot be deleted
- Trip costs are not stored directly in the trip record. Expenses are recorded separately and linked to the trip

### Entity: Waste Receiving Event

#### Definition

A record of waste delivered to the production site

#### Created By

Operations Manager or Production Manager

#### Created When

Waste is weighed and accepted

#### Required Information

- Trip
- Source
- Waste Type
- Weight
- Date

#### Business Rules

- Waste cannot exist without a receiving event
- Weight must be greater than zero
- A rejected load is recorded but marked as rejected
- Receiving records are never deleted

### Entity: Waste Sorting Event

#### Definition

A record of waste sorting process on the waste received at the production site.

#### Created By

Operations Manager or Production Manager

#### Created When

Waste from Waste Receiving Event has been physically sorted, contaminants removed and the resulting material categories have been weighed.

#### Required Information

- Sorted Weight
- Storage Container
- Sorting Date
- Waste Receiving Event
- Compostable Weight
- Plastic Weight
- Rejected Waste Weight
- Contaminants notes
- Waste Sorting Employee

#### Business Rules

- Every Waste Sorting Event must reference one valid Waste Receiving Event
- Sorting cannot be recorded before related waste has been received.
- All recorded weights must be zero or greater.
- The total sorted output should not materially exceed the gross weight recorded during waste receiving.
- Any difference between the received weight and total sorted weight must be recorded as moisture loss, spillage, measurement variance, or another documented reason.
- Usable feedstock must be stored separately from plastics, contaminants, and rejected material.
- All storage containers must be labelled with container ID and sorting date
- A completed sorting record cannot be deleted. Corrections must be made through an authorised amendment or audit process.
- Waste from one receiving event may be sorted across multiple sorting events when sorting is completed in stages.
- Material produced by a sorting event cannot be used in a recipe unless it has been accepted as usable feedstock.

### Entity: Recipe

#### Definition

A feed mixture prepared from one or more sorted waste ingredients for use in feeding larvae.

#### Created By

Production Manager or Production Operator.

#### Created When

A new feed mixture is prepared for larvae feeding.

#### Ends When

The entire recipe has been consumed or discarded.

#### Business Rules

- A recipe may contain one or more sorted waste ingredients.
- Water added during mixing must be recorded.
- The total ingredient weight must equal the recipe weight.
- A recipe cannot be modified after it has been used in a feeding event.
- A recipe may be used in one or more feeding events until fully consumed.

### Entity: Recipe Ingredient

#### Definition

A record of a mtaerial and quantity added to a recipe

#### Created By

Operations Manager or Production Manager

#### Created When

An ingredient is added during recipe preparation

#### Ends When

The recipe is completed, discarded or fully used

#### Business Rules

- Every recipe ingredient must belong to one recipe.
- An ingredient may come from sorted waste, purchased material, water, or another approved material.
- The ingredient type, quantity, and unit of measure must be recorded.
- The quantity must be greater than zero.
- Ingredients sourced from sorted waste should reference the related sorting record.
- Ingredients taken from inventory cannot exceed the available quantity.

## Domain: Biological Production

### Entity: Breeding Batch

#### Definition

A group of mature BSFL transferred to a breeding cage for egg production

#### Created By

Operations Manager or Production Manager

#### Created When

Mature prepupae or adult BSFL are transferred into a breeding cage

#### Ends When

A breeding cycle is completed or the batch is retired

#### Required Information

- Breeders weight
- Breeding cage
- Transfer date
- Source type
- Source reference

#### Business Rules

- Every breeding batch must be assigned to one breeding cage.
- A breeding batch must originate from an internal harvest or an external supplier.
- Breeder weight must be greater than zero.
- A breeding batch can produce multiple egg collection events.
- A completed breeding batch cannot receive additional breeders.

### Entity: Egg Collection Event

#### Definition

An event where eggs produced by various breeding batches are collected from a breeding cage

#### Created By

Operations Manager or Production Manager

#### Created When

An eggie full of BSFL eggs is collected from a breeding cage

#### Ends When

An eggie is weighed and prepared for hatching in the nursery

#### Required Information

- Eggie Placement date
- Empty eggie weight
- Full eggie weight
- Eggie collection date

#### Business Rules

- Every egg collection event must reference one breeding cage.
- An empty eggie must be weighed before placement in the cage.
- A full eggie must be weighed after collection.
- Full eggie weight must be greater than empty eggie weight.
- Egg weight is calculated as full eggie weight minus empty eggie weight.
- Egg collection must occur after eggie placement.
- The breeding batches occupying the cage during the collection period must be traceable.
- Collected eggs may originate from multiple active breeding batches.
- Collected eggs must be transferred to the nursery or recorded as rejected.

### Entity: Nursery Batch

#### Definition

A batch of BSFL eggs transferred from an egg collection event to the nursery for hatching and early larval development.

#### Created By

Production Manager or Operations Manager.

#### Created When

Collected eggs are placed in the nursery for hatching.

#### Ends When

The neonates are transferred to a production larvae batch or the nursery batch is rejected.

#### Required Information

- Egg collection event
- Nursery start date
- Expected hatch date
- Transfer date
- Egg weight
- Neonate weight (optional)
- Nursery status

#### Business Rules

- Every nursery batch must originate from one egg collection event.
- A nursery batch cannot be transferred before hatching.
- A nursery batch may only be transferred once to production.
- A completed or rejected nursery batch cannot be modified.
- All transfers from the nursery must be recorded.

### Entity: Larvae Batch

#### Definition

A group of BSFL larvae reared in a specific container from nursery until harvest

#### Created By

Production Manager or Operations Manager

#### Created When

Nursery larvae or externally sourced larvae are placed into a production basin.

#### Ends When

A batch is fully harvested or rejected

#### Required Information

- Nursery batch
- Transfer date
- Initial weight
- Status

#### Business Rules

- Every larvae batch must originate from one source, either a nursery batch or an external source.
- Each larvae batch must be assigned to one basin or container.
- One nursery batch may be divided into multiple larvae batches.
- Each basin-based larvae batch must have a unique batch ID.
- A larvae batch may have multiple feeding events.
- A larvae batch may be harvested when it reaches the required maturity.
- Multiple larvae batches may be included in the same harvest event.
- Feeding is only permitted while the batch is active.
- A fully harvested or rejected batch cannot receive additional feeding.
- All basin transfers, harvests, and rejections must be recorded.

### Entity: Feeding Event

#### Definition

A record of a recipe provided to an active larvae batch or nursery batch

#### Created By

Operations Manager or Production Manager

#### Created When

A prepared recipe is added to a nursery batch or larvae batch

#### Required Information

- Feeding date
- Recipe
- Target batch
- Quantity fed
- Employee responsible

#### Business Rules

- Every feeding event must reference one recipe.
- A feeding event must target either a nursery batch or a larvae batch, but not both.
- Feed quantity must be greater than zero.
- A recipe cannot be fed before it is prepared.
- Only active batches may receive feeding.
- The total quantity fed cannot exceed the available quantity of the recipe.
- Feeding events cannot be deleted after approval; corrections must be recorded through an audit process.

### Entity: Harvest Event

#### Definition

A record of harvesting a larvae batch from its production basin.

#### Created By

Operations Manager or Production Manager

#### Created When

One or more larvae batches are harvested

#### Required Information

- Harvest date
- Harvested larvae batches
- Larvae Batch
- Employee responsible

#### Business Rules

- Every harvest event must reference one larvae batch.
- A larvae batch may have one or more harvest events.
- Only active larvae batches may be harvested.
- Multiple harvest events may be pooled into one harvest batch.
- A harvest event may only belong to one harvest batch.
- Harvest output weights are recorded at the harvest batch level after pooling and weighing.
- A completed harvest event cannot be deleted; corrections must be recorded through an audit process.

### Entity: Harvest Batch

#### Definition

A pooled and weighed batch of harvested material produced from one or more harvest events.

#### Created By

Operations Manager or Production Manager

#### Created When

Harvested material from one or more harvest events is pooled and weighed.

#### Required Information

* Wet larvae weight
* Prepupae weight
* Frass weight
* Reject weight

#### Business Rules

* A harvest batch must originate from one or more harvest events.
* A harvest event may belong to only one harvest batch.
* Wet larvae, prepupae, frass and rejects must be recorded separately.
* Harvest weights must not be negative.
* Wet larvae from a harvest batch may be allocated across one or more drying events.
* Prepupae may be transferred to breeding.
* Frass may be used to create a product batch.
* The total wet larvae allocated to drying must not exceed the wet larvae weight recorded for the harvest batch.


## Domain: Processing and Inventory

### Entity: Drying Event

#### Definition

A record of drying a portion of a harvested larvae batch in a charcoal oven.

#### Created By

Operations Manager or Production Manager

#### Created When

The drying process is completed and the dried larvae are removed from the oven.

#### Ends When

A larvae batch has been dried

#### Required Information

- Harvest batch
- Oven
- Drying start date and time
- Drying completion date and time
- Wet larvae weight
- Dried larvae weight
- Charcoal used (optional)
- Employee responsible

#### Business Rules

- Every drying event must reference one harvest batch.
- Every drying event must be assigned to one oven.
- A harvest batch may be dried through multiple drying events.
- Wet larvae weight must be greater than zero.
- Dried larvae weight must not exceed the wet larvae weight.
- Drying output must be recorded before packing.
- Completed drying events cannot be modified without an authorised correction.

### Entity: Product Batch

#### Definition

A quantity of finished product created from one or more completed drying events and prepared for storage or sale.

#### Created By

Production Manager or Operations Manager.

#### Created When

Dried larvae are weighed, grouped, and recorded as finished product.

#### Ends When

The full batch quantity has been sold, used internally, discarded, or otherwise removed from inventory.

#### Required Information

- Product
- Batch number
- Production date
- Source drying event(s)
- Total batch weight
- Storage location
- Status

#### Business Rules

- Every product batch must reference one product.
- Every product batch must originate from one or more completed production events appropriate for its product type.
- Batch weight must be greater than zero.
- Product from different types must not be combined into one batch.
- Available quantity must not fall below zero.
- All sales, losses, samples, and internal use must reduce the recorded inventory.
- A product batch cannot be sold before it is completed and approved.
- Completed product batches cannot be deleted; corrections must be auditable.

### Entity: Inventory Movement

#### Definition

A record of any transaction that increases, decreases, or transfers inventory.

#### Created By

Operations Manager Storekeeper, Sales Officer, or Production Manager.

#### Created When

A product is added to, removed from, transferred within, or adjusted in inventory.

#### Required Information

- Product batch
- Movement type
- Quantity
- Movement date
- Source location (if applicable)
- Destination location (if applicable)
- Related event
- Employee responsible

#### Ends When

The inventory transaction has been completed and recorded.

#### Business Rules

- Every inventory movement must reference one product batch.
- Every inventory movement must have a movement type.
- Quantity must be greater than zero.
- Inventory cannot become negative.
- Every movement must be traceable to a business event (e.g. packing, sale, transfer, adjustment, sample, disposal).
- Completed inventory movements cannot be deleted; corrections must be recorded through an audit process.

## Domain: Commercial

### Entity: Product

#### Definition

A finished product manufactured and sold by SoilAid Technologies.

#### Created By

Production Manager or System Administrator.

#### Created When

A new product is introduced for production or sale.

#### Ends When

The product is discontinued.

#### Required Information

- Product name
- Product category
- Unit of measure
- Packaging size
- Status

#### Business Rules

- Every product must have a unique name or SKU.
- A product may have multiple product batches.
- A product may be active or discontinued.
- Discontinued products cannot be assigned to new product batches.
- Product details may be updated without affecting historical production or sales records.
- Products are never permanently deleted; they are marked as inactive when discontinued.

### Entity: Customer

#### Definition

An individual or organisation that purchases products from SoilAid Technologies.

#### Created By

Sales Officer, Production Manager, or System Administrator.

#### Created When

A new customer is registered in the system.

#### Ends When

The customer is marked as inactive.

#### Required Information

- Customer name
- Customer type
- Contact information
- Delivery location
- Status

#### Business Rules

- Every customer must have a unique customer record.
- A customer may have multiple sales.
- Inactive customers cannot be assigned to new sales.
- Customer information may be updated without affecting historical sales records.
- Customer records are never permanently deleted; they are marked as inactive when no longer active.

### Entity: Sale

#### Definition

A record of finished products sold to a customer.

#### Created By

Sales Officer, Production Manager, or Operations Manager.

#### Created When

A customer purchases one or more product batches.

#### Ends When

The sale has been completed or cancelled.

#### Required Information

- Customer
- Sale date
- Product batch
- Quantity sold
- Unit price
- Total amount
- Employee responsible
- Sale status

#### Business Rules

- Every sale must reference one customer.
- Every sale must reference one or more product batches.
- Quantity sold must be greater than zero.
- Quantity sold cannot exceed the available inventory.
- Total amount is calculated from the quantity sold and unit price.
- A completed sale reduces the available inventory.
- Completed sales cannot be deleted; corrections must be made through an authorised adjustment or reversal.

## Domain: Workforce and accountability

### Entity: Employee

#### Definition

A person employed by SoilAid Technologies who performs operational, administrative, or management activities.

#### Created By

System Administrator or Human Resources.

#### Created When

A new employee joins the organisation.

#### Ends When

The employee leaves the organisation or is marked as inactive.

#### Required Information

- Employee ID
- Full name
- Job title
- Department
- Employment type
- Status

#### Business Rules

- Every employee must have a unique employee ID.
- An employee may perform multiple operational events.
- Only active employees may be assigned to new events.
- Employee information may be updated without affecting historical records.
- Employee records are never permanently deleted; they are marked as inactive when employment ends.
