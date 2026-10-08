INX: The System That Should Not Have Failed

Challenge

Automated workflows are expected to follow a predictable sequence.

A request is created, moves through a series of steps, and eventually reaches completion. In practice, workflows can behave differently from what was expected.

A request might be approved twice. A step might occur before the step that should have preceded it. A request might remain stuck for too long. Several individually unusual events might also indicate a larger problem when considered together.

The challenge is to detect this abnormal behaviour and provide enough evidence for a user to understand what went wrong.

What to Build

Build a system that monitors workflow activity, identifies abnormal behaviour, and helps a user investigate the issue.

The core flow is:

Workflow
   ↓
Events
   ↓
Expected Behaviour
   ↓
Detection
   ↓
Anomaly
   ↓
Explanation
   ↓
Investigation

1. Define a Workflow

Choose a workflow containing multiple stages.

For example:

Request Created
       ↓
Verification
       ↓
Approval
       ↓
Payment
       ↓
Completed

The workflow is your choice. Possible domains include:

* Payments
* Approvals
* Customer support
* Logistics
* Employee onboarding
* Order processing
* Document processing

The workflow must have enough structure for abnormal behaviour to be meaningful.

2. Define an Event Model

Your system must represent events occurring within the workflow.

Each event should contain enough information to understand what happened. For example:

event_id
workflow_id
event_type
timestamp
actor/system
status

The exact schema is up to you.

3. Establish Normal Behaviour

Your system must have a defined way of determining what normal behaviour looks like.

This could be based on:

* Valid state transitions
* Expected event sequences
* Time thresholds
* Historical behaviour
* Statistical patterns
* A learned model
* A combination of approaches

Document how your system determines that behaviour is abnormal.

4. Detect Anomalies

The system must identify abnormal workflow behaviour.

For example:

Created
   ↓
Verification
   ↓
Approval
   ↓
Approval
   ↓
Payment

The repeated approval may be suspicious.

Another example:

Created
   ↓
Approval
   ↓
Verification

The ordering may be invalid.

A timing anomaly could look like:

Created
   ↓
Verification
   ↓
       [6 hours]
   ↓
Approval

If the expected processing time is shorter, the delay may be considered abnormal.

These are examples only. The team decides which abnormal behaviours matter for its chosen workflow.

5. Explain the Anomaly

Detecting an anomaly is not enough. When an alert is raised, the user should be able to understand why.

For example:

ANOMALY DETECTED
Workflow: #1042
Issue:
Approval occurred twice.
Expected:
Created → Verification → Approval → Payment
Observed:
Created → Verification → Approval → Approval → Payment

Or:

ANOMALY DETECTED
Workflow: #7821
Issue:
Verification exceeded the expected processing time.
Expected: < 30 minutes
Observed: 2 hours 14 minutes

The explanation must be based on evidence from the workflow events.

6. Investigate History

A user must be able to inspect the events surrounding an anomaly.

At minimum, the system should make it possible to determine:

* What happened
* When it happened
* Which workflow was affected
* Which event triggered the alert
* What the system expected instead

A timeline or equivalent investigation view is recommended.

Constraints

Greenfield System

ARC will not provide:

* A broken application
* A production workflow
* A private event stream
* A custom anomaly dataset
* A monitoring server

You must build the system yourself.

Generate Your Own Events

Your solution must be able to generate or simulate workflow events.

The event generator must support both:

* Normal behaviour
* Abnormal behaviour

This allows the system to be demonstrated independently.

Define Your Detection Logic

Document what your system considers an anomaly.

The system should not simply label an event as anomalous without explaining the underlying rule, baseline, or model used to make that decision.

Real-Time Processing Is Optional

You do not need to build production-grade streaming infrastructure.

A simulated event stream, batch processing system, or historical event dataset is acceptable.

The focus is on the quality of detection and investigation.

Technology

There is no prescribed technology stack.

You may use:

* Rule-based detection
* Statistical methods
* Machine learning
* Sequence analysis
* Time-series analysis
* LLMs
* Anomaly detection algorithms
* Databases
* Event streams
* A hybrid approach

AI is optional.

A well-designed rule-based system can be stronger than a poorly justified ML system.

Evaluation

Detection

Can the system identify meaningful abnormal behaviour?

Precision

Does it avoid flagging every unusual event as an incident?

Explanation

Can a human understand why an alert was generated?

Investigation

Can a user trace the relevant events?

Engineering

Consider:

* Is the workflow model clear?
* Is the event representation sensible?
* Can the system handle increasing event volume?

Judgment

Does the team understand the limitations of its detection approach?

Implementation Choices

The following are left to the team:

* Workflow
* Event schema
* Definition of normal behaviour
* Definition of an anomaly
* Detection method
* Storage approach
* Interface
* Alert design
* Severity model
* Technology stack
* Whether AI or ML is appropriate

There is no prescribed implementation.

Optional Enhancements

These features are optional:

* Anomaly scoring
* Root-cause analysis
* Predictive failure detection
* Recovery recommendations
* Real-time monitoring
* Historical baseline comparison
* Configurable thresholds
* Multiple workflow types
* Incident timelines
* Alert prioritization
* Feedback from human reviewers

Do not add complexity without a reason.

Acceptance Criteria

Your solution must demonstrate the following:

* [ ]	A workflow with multiple stages is defined.
* [ ]	Workflow events can be generated or ingested.
* [ ]	Normal workflow behaviour is defined.
* [ ]	Abnormal behaviour can be generated.
* [ ]	The system detects abnormal behaviour.
* [ ]	Detected anomalies include an explanation.
* [ ]	Historical events can be inspected.
* [ ]	A user can identify the affected workflow.
* [ ]	At least three distinct anomaly cases can be demonstrated.
* [ ]	The system can distinguish normal and abnormal examples.
* [ ]	The complete detection and investigation flow can be demonstrated.

Submission Requirements

The repository must contain enough information for another developer to understand and run the solution.

At minimum, include:

README.md
ARCHITECTURE.md
DECISIONS.md
TESTING.md

ARCHITECTURE.md

Document:

* Workflow model
* Event model
* Processing pipeline
* Detection architecture
* Storage
* User interface
* Major components

Include an architecture diagram.

DECISIONS.md

Document important technical decisions and trade-offs.

For example:

* Why was this anomaly detection approach chosen?
* Why is this behaviour considered abnormal?
* Why was this event schema chosen?
* Why was this threshold or model selected?
* What alternative approaches were considered?

TESTING.md

Include tests covering:

* Normal workflows
* Invalid sequences
* Duplicate events
* Delayed events
* Other anomaly types chosen by the team
* False-positive scenarios
* Edge cases

Demo Expectations

The demonstration should make the anomaly visible.

A recommended flow is:

1. Introduce the workflow
        ↓
2. Show normal behaviour
        ↓
3. Generate normal events
        ↓
4. Show the system accepting them
        ↓
5. Introduce abnormal behaviour
        ↓
6. Show the alert
        ↓
7. Explain why it was detected
        ↓
8. Investigate the underlying events
        ↓
9. Show another anomaly
        ↓
10. Defend the detection approach

Do not spend the entire demonstration explaining the dashboard. Show the system detecting behaviour that should not have happened.

Event-Day Challenge

During evaluation, judges may ask you to:

* Introduce a new abnormal sequence.
* Change an expected threshold.
* Generate additional events.
* Explain why a suspicious event was or was not detected.
* Show the evidence behind an alert.

Your system should make these decisions understandable.

Rules

* Build your own solution.
* AI-assisted development is allowed.
* Public libraries and tools are allowed.
* Do not depend on an ARC-owned backend or dataset.
* Do not commit private credentials.
* Be prepared to explain your implementation.
* Detection logic must be defensible.
* Core requirements take priority over optional features.

Final Checklist

Before submission:

* [ ]	Workflow is clearly defined.
* [ ]	Event schema is documented.
* [ ]	Normal behaviour is documented.
* [ ]	Event generation works.
* [ ]	Normal events can be demonstrated.
* [ ]	Abnormal events can be generated.
* [ ]	Anomalies are detected.
* [ ]	Alerts include explanations.
* [ ]	Historical events can be investigated.
* [ ]	At least three anomaly cases are tested.
* [ ]	False positives and limitations are documented.
* [ ]	No secrets are committed.
* [ ]	Architecture is documented.
* [ ]	Technical decisions are documented.
* [ ]	Testing is documented.
* [ ]	Demo is ready.

INNOVEX | ARC Club