# Project showcase
## Project 1: COPA
### Project Origin
- The project started from a simple frustration: why does a relatively rule-based engineering selection and quotation process still require extensive manual work in calculation, searching, copying, formatting, and verification?
- I had previously built an Excel-based workbook to automate part of the solution and quotation process. However, it was difficult to maintain, covered only one brand, while our actual business required support for 2–3 brands.
- I decided to go one step further: learn Python from scratch and build a more powerful lightweight automation tool for myself and my colleagues.

### Detailed Action
- I started with a rule-based selection engine, which was completed within a month with AI-assisted review. However, I was not satisfied with the CLI-based input and output, so I decided to build an orchestrator layer to manage the engine's inputs and outputs.
- The project was temporarily suspended due to a change in my personal plans and was relaunched in August 2026.
- With the assistance of coding agents, I learned and built the orchestrator — which I named the Commander — together with the supporting modules required to handle the complete workflow.
- COPA can now accept professional inquiries through an input box, parse the requirements, generate a suitable selection of weighing equipment for human confirmation, and produce a standardized quotation sheet upon confirmation.

### Key Insight
- **The software should not make unreasonable guesses.** Therefore, I deliberately introduced zero AI into the core selection process.
- **Human-in-the-loop.** COPA only provides recommendations based on explicit business rules. The final decision remains with the user.
- **Human-readable and editable output.** All outputs remain accessible to users rather than being locked inside the software.
- **Exception cases remain human responsibilities.** COPA is designed to cover common and structured scenarios rather than attempting to replace human judgment in extreme cases.
- **Lightweight and nimble.** The software should remain simple to deploy and use, without introducing unnecessary complexity into the existing workflow.
- **Maintainable by business users.** Product data should remain readable and maintainable by ordinary office workers without software-engineering knowledge.
- **The real value lies in reusable structured data rather than faster quotation.** By preserving project information as a structured snapshot, COPA turns a one-time quotation into a reusable project asset that can support downstream workflows.

### Results
- The first production-ready version of COPA was handed over to me as the primary user on September 1, 2026, and subsequently released to colleagues for commissioning.
- I later upgraded COPA to support a newly launched product series and added English-language output.
- Initial user feedback was positive, followed by a more valuable finding: some colleagues had difficulty using the natural-language input box because their actual working vocabulary may differed from the language patterns covered by my parser.
- In response, I introduced a **dual-input mode**, allowing users to enter requirements either through the natural-language input box or through structured dropdown selections. The two modes are synchronized, allowing users to gradually learn the natural-language input format through the structured interface.
- In COPA v1.3, I further integrated **technical-document generation**, extending the workflow from **inquiry → selection → quotation** to **inquiry → selection → quotation → technical documentation**.

### Future Direction
- **From structured project data to interactive presentation.** COPA's project snapshot could serve as the foundation for automatically generating customer-facing interactive HTML presentations, combining product data, 3D assets, and LLM-assisted web generation.

## Project 2: Reconstructing Business Logic Behind a Legacy Workflow
### Project Origin
- The project was triggered by a personal observation: after transitioning into a new role, my girlfriend inherited a legacy workflow that consumed an entire weekend to understand and complete due to significant manual processing requirements. I initially considered automating the workflow to improve efficiency, but deeper analysis revealed that the core problem was not simply a lack of automation or formulas, but the absence of an explicitly modeled underlying business logic.
### Detailed Action
- At first glance, the entire workflow appeared to be an operational calculation buried under massive formulas.
- I initially attempted to refine and automate the workflow for optimization.
- However, while analyzing the manual allocation calculation, I discovered multiple circular references and a large number of unnecessary intermediate variables.
- After reverse-engineering the existing calculation logic, I hypothesized that the core issue was not missing automation, but an improperly represented business logic model.
- Therefore, I reconstructed the underlying business logic, redesigned the calculation flow, and validated the new model with the business owner responsible for the workflow.
- After validating this hypothesis with the business owner, I confirmed that the workflow complexity was mainly caused by attempts to automate volatile and undefined business rules.
- Since there was no standardized rule for overage allocation, I introduced a simplified allocation strategy based on the updated business logic.
- During discussions with the key user regarding historical adjustment cases, I identified additional exceptions that could not be reliably automated due to ad hoc rules. I therefore inserted a manual adjustment layer to preserve flexibility.
- I rebuilt the workflow model and implemented the redesigned calculation flow for business validation.
- After the redesigned workflow was introduced to the key user, I further explored whether the remaining frequently changing parameters could be modularized and automated. However, user validation showed that the additional abstraction introduced unnecessary learning costs while providing limited practical benefit to the current workflow.
- I therefore decided to **stop further automation at this stage** and retain the simpler workflow that the key user was already comfortable maintaining.

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
  - **Step 1. Store Required Quantity** -- directly inherit from existing calculation workflow
  - **Step 2. RD-level Cartonization** -- Convert required quantity into actual shipping packages based on package size
  - **Step 3. Overage Allocation**
  - **Step 4. Store Shipment Quantity & Overage Record**

### Key Insight
- The complexity of the legacy workflow came from mixing different business concepts and semantic shifting of intermediate variables.
- By separating these concepts, redefining the necessary variables, and eliminating calculation redundancies, the workflow became much simpler, more transparent, and easier to validate.
- It is unnecessary to optimize areas where the business has no defined objectives, so certain rules and logic were deliberately inherited with records rather than being further optimized.
- Upon reflection, the evolution of the legacy workflow became clear: it was not necessarily poorly designed from the beginning. It likely evolved incrementally as new business requirements, exceptions, and operational workarounds were added over time.
- The problem was that the underlying business logic was never **reorganized** as the workflow evolved, causing incremental rules to stack as redundant formulas, intermediate variables, and manual workarounds.
- **Automation should follow actual business friction, rather than technical possibility.** After user validation, I found that the existing simplified workflow had already eliminated most of the practical friction. Further abstraction made the workflow harder to learn without solving a significant remaining problem, so I chose not to continue automating it.

### Results
- Reduced the required output from multiple intermediate calculation fields to 2 **focused outputs**.
- Simplified the workflow structure and improved transparency by separating different concepts and neutralizing the semantic shift in key variables.
- Established a clearer foundation for future rule refinement with the key user.
- Validated the practical usability of the redesigned workflow with the key user and identified that the remaining major friction originated from **institutional constraints rather than the calculation workflow itself.**
- **Phase-gated the project after validation instead of pursuing automation for its own sake.**
