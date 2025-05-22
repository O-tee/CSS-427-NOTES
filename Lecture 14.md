# Iterative Development.pptx 

## Things I'm confused about 

## After class TODO

## Notes 

## Object Oriented Design
- An object is an abstract data type with the addition of polymorphism and inheritance.
- Rather than structure programs as code and data, an object-oriented system integrates the two using the concept of an "object".
- An object has state (data) and behavior (code or method).
- C++ was invented to support objects as classes.

## Agile Manifesto 
- Individuals and interactions
  - over processes and tools
- Working software
  - over comprehensive documentation
- Customer collaboration
  - over contract negotiation
- Responding to change
  - over following a plan

### Agile Principles (1)
- Our highest priority is to satisfy the customerthrough early and continuous deliveryof valuable software.
- Welcome changing requirements, even late in development. Agile processes harness change for the customer's competitive advantage.
- Deliver working software frequently, from acouple of weeks to a couple of months, with apreference to the shorter timescale.
- Business people and developers must worktogether daily throughout the project.

### Agile Principles (2)
- Build projects around motivated individuals. Give them the environment and support they need, and trust them to get the job done.
- The most efficient and effective method of conveying information within a development team is face-to-face conversation.
- Working software is the primary measure of progress.
- Agile processes promote sustainable development. The sponsors, developers, and users should be able to maintain a constant pace indefinitely.

### Agile Principles (3)
- Continuous attention to technical excellence and good design enhances agility.
- Simplicity--the art of maximizing the amount of work not done--is essential.
- The best architectures, requirements, and designs emerge from self-organizing teams.
- At regular intervals, the team reflects on how to become more effective, then tunes and adjusts its behavior accordingly.

### Agile methods
- Extreme Programming
- SCRUM
- Crystal
- Adaptive Software Development
- Dynamic Systems Development Method (DSDM)
- Feature Driven Development

## UML and Patterns
- “Applying UML and Patterns” by Craig Larman.
- UML = Unified Modeling Language
- An introduction to Object-Oriented Analysis and Design and Iterative Development.
- Larman strongly advocates against the waterfall model.

## Waterfall
- OK if requirements are fixed.
- In software, typically get 25% to 50% change in requirements.
- If an “iterative” project spends too much time on requirements, it has been afflicted with waterfall thinking.
- Instead, use feedback from early development and testing.

## Iterative Example
- Three-Week early iteration
  - Kickoff meeting – Clarify tasks and goals for the iteration.
  - One person makes UML diagrams from previous iteration.
  - On day 1, team works in pairs at whiteboards doing models.
  - On remaining days, implement, test, design, integrate, daily builds.
 
### Expanded example
- All iterations are timeboxed – they go for a certain fixed length of time.
- Let’s say there are 20 iterations.
- Put risky, high value, or difficult things in an early iteration.
- Each iteration ends with tested, production quality code.

### Before iteration 1:
- Hold a timeboxed (e.g. 2 days) requirements workshop.
- On the morning of day 1, do high-level requirements, such as just the names.
- Pick 10% of the requirements that have high risk or value or significantly impact the core architecture.
- For the remaining day and a half, do a detailed analysis of these requirements.

## Iteration 1
- On 1st two days, pairs model the system with UML diagrams.
- Developers then program, test and integrate.
- One week before the end, ask if all iteration goals can be met; if not, descope.
- Have a code freeze, then a demo to stakeholders.

## Second requirements workshop
- Held near the end of iteration 1.
- Pick another 10-15% of significant use cases.
- Analyze them in detail.
- About 25% of use cases and non-functional requirements are done in detail.
- Requirements are not perfect.

### Requirements
- Functional – Services the system shall provide and how it behaves in particular situations
- Non-functional – Constraints such as timing and standards
- Domain – Characteristics of the application domain
There is a soft boundary between these three

## More iterations
- Iteration 2 is similar to 1.
- After 4 iterations, have 80-90% of requirements in detail.
- About 10% of the system is done.
- End of elaboration phase.
- Because of realistic investigation and feedback, estimates are much more reliable.
- Requirements are stabilized, though never completely frozen.


## Agile UP
- Prefer a small set of Unified Process (UP) activities and artifacts.
- Requirements and design use feedback; not completed before implementation.
- Detailed plan only for the next iteration.

### Agile modeling
- The purpose of modeling is primarily to understand, not to document.
- Quickly explore alternatives.
- Don’t model all the software. Model and apply UML to unusual and tricky parts of the design.
- Use the simplest tool possible.
- Model in pairs at whiteboard.
- Accept that all models will be inaccurate.

## Best practices
- Do high risk and high value issues first.
- Continuously engage users.
- Build core architecture early.
- Test early, often and realistically.
- Apply use cases where appropriate.
- Do some visual modeling.
- Manage change requests and configurations.

## UP Phases
- Inception – like a feasibility study.
- Elaboration – refine the vision and implement core architecture.
- Construction – Implement remaining low risk tasks.
- Transition – Beta tests, deployment.

## UP disciplines
- Business (domain) modeling.
- Requirements – Use cases, etc.
- Design of software
- Implementation
- Test
- Deployment

## Phases and disciplines
- During any phase, all disciplines are present to greater or lesser degree.
- An artifact is the UP term for any work product.
- All UP artifacts are optional.
"You should use iterative development only on projects that you want to succeed." – Martin Fowler

## Iterative development
- Less project failure.
- Early mitigation of high risks.
- Early visible progress.
- Early feedback that better meets real needs.
- Managed complexity.
- Development process can improve iteration to iteration.

## Inception
- Envision the product scope, vision, and business case.
- Do the stakeholders have basic agreement on the vision and is it worth investing in serious investigation?
- Get a rough, unreliable range of cost.

## Evolutionary requirements
- Requirements are capabilities and conditions to which the system must conform.
- Find, document, organize and track the changing requirements of a system.

## FURPS
- Functional – features, capabilities, security.
- Usability – human factors, help, documentation.
- Reliability – frequency of failure, recoverability, predictability.
- Performance – response time, throughput, resource usage.
- Supportability – maintainability, internationalization, configurability.




















