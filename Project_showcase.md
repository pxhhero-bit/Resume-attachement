# PM showcase
## Project 1: COPA
### Project Origin
- The project started from a simple frustration: Why does my quotation preparation process, despite being a relatively rule-based engineering selection task, still require extensive manual effort in calculation, searching, copying, formatting, and verification?
### Detailed Action
- I have previously built up a excel-based
### Key Insight
### Results

## Project 2: Reconstructing Business Logic Behind a Legacy Workflow
### Project Origin
- The project was triggered by a personal observation: after transitioning into a new role, my girlfriend inherited a legacy workflow that consumed an entire weekend to understand and complete due to significant manual processing requirements. I initially considered automating the workflow to improve efficiency, but deeper analysis revealed that it was not the lack of automation or formulas that caused the complexity, but the absence of an explicitly modeled underlying business logic.
### Detailed Action
- At first glance, the entire workflow appeared to be an operational calculation buried under massive formulas.
- I initially attempted to refine and automate the workflow for optimization.
- However, while analyzing the manual allocation calculation, I discovered multiple circular references and a large number of unnecessary intermediate variables.
- After reverse-engineering the existing calculation logic, I hypothesized that the core issue was not missing automation, but an improperly represented business logic model.
- Therefore, I reconstructed the underlying business logic, redesigned the calculation flow, and validated the new model with the business owner responsible for the workflow.
- After validating this hypothesis with the business owner, I confirmed that the workflow complexity was mainly caused by attempts to automate volatile and undefined business rules.
- Since there was no standardized rule for overage allocation, I introduced a simplified allocation strategy based on the updated business logic.
- During discussions with the key user regarding historical adjustment cases, I identified additional exceptions that could not be reliably automated due to ad hoc rules. Therefore, I inserted a manual adjustment layer to preserve flexibility.
- I rebuilt the workflow model and implemented the redesigned calculation flow for business validation.
### Business Logic Reconstruction
- Existing formula-driven calculation chain with fragmented intermediate variables, where demand calculation, shipping unit conversion, allocation, and validation logic were tightly coupled, including:
  - RD-level Pcs difference calculation
  - Store-level Pcs difference calculation
  - RD-level Boxes difference calculation
  - Store-level Boxes difference calculation
  - Store-level Shipment ranking
  - Ranking validation
  - Inventory aftershipment
  - Multiple duplicated intermediate variables
  - Mulitple spreadsheets
- New model:
  - Step 1. Store Required Quantity (directly inherit from existing calculation workflow)
  - Step 2. RD-level Cartonization (Convert required quantity into actual shipping packages based on package size)
  - Step 3. Overage Allocation
  - Step 4. Store Shipment Quantity & Overage Record
### Key Insight
- The complexity of the legacy workflow came from mixing different business concepts and semantic shifting of intermediate variables.
- By separating these concepts, redefining the necessary variables and eliminating calculation redundancies, the workflow became much simpler, more transparent, and easier to validate.
- It is unnecessary to optimize areas where the business has no defined objectives, so certain rules and logic was inherited with records.
- Upon reflection, the evolution of the legacy workflow became clear: it was not necessarily poorly designed from the beginning. It likely evolved incrementally as new business requirements, exceptions, and operational workarounds were added over time.
- The problem was that the underlying business logic was never reorganize as the workflow evolved, causing incremental rules to stack as redundant formulas, intermediate variables, and manual workarounds.
### Results
- Reduced the required output from multiple intermediate calculation fields to 2 focused outputs.
- Simplified workflow structure and improved transparency by separating different concepts and neutralizing the sematic shift in key variables.
- Established a clearer foundation for future rule refinement with the key user.