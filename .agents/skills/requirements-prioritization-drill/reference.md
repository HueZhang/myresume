# Requirements Prioritization Reference

## Goal

The drill is meant to build one habit:

Take a broad prompt and reduce it to a small, defensible set of requirements before talking about architecture.

## Mental Model

Use this compression sequence:

1. Who is the user?
2. What is the core value delivered to that user?
3. What is the minimum end-to-end loop that creates that value?
4. Which constraints materially change the design of that loop?

If the user can answer those four questions, they are usually ready to write requirements.

## Strong Follow-Up Question Categories

These are the best places to probe first:

### 1. Primary user and workflow

Ask:

- Who is the main user or client?
- What is the most important action they need to complete?
- Is this primarily a read-heavy, write-heavy, or workflow system?

Why:

This reveals the core value loop and prevents premature feature sprawl.

### 2. Scope boundaries

Ask:

- What is explicitly in scope for this interview?
- What can I treat as existing platform functionality?
- Are there important features we can defer?

Why:

Strong candidates narrow the problem. Weak candidates try to design the whole company.

### 3. Scale shape

Ask:

- Roughly how many users, requests, or events are we supporting?
- Is traffic bursty, seasonal, or globally distributed?
- Are reads or writes the main scaling concern?

Why:

The traffic shape matters more than raw DAU numbers.

### 4. Latency, durability, and consistency

Ask:

- Which operations need low latency?
- What data cannot be lost?
- Where do we prefer consistency over availability, or vice versa?

Why:

These usually become the architecture-defining non-functional requirements.

### 5. Failure and correctness

Ask:

- What kinds of mistakes are acceptable versus unacceptable?
- Is eventual consistency acceptable anywhere?
- What are the consequences of duplicate processing, stale reads, or partial failure?

Why:

This turns vague "reliability" into actual design constraints.

## Requirement Selection Heuristics

### Functional Requirements

A strong set usually:

- has 3 items
- represents one end-to-end workflow
- avoids listing every feature mentioned in the prompt
- uses product-facing language like `Users should be able to...`

Good signs:

- clear prioritization
- obvious exclusions or deferrals
- one requirement can be described as the "main loop"

Bad signs:

- feature laundry list
- admin, analytics, billing, permissions, and notifications all included at once
- no distinction between must-have and nice-to-have

### Non-Functional Requirements

A strong set usually:

- has 3 items
- is quantified where possible
- points at a hotspot
- forces trade-offs

Good examples:

- `Ingestion writes should complete in <200ms p99.`
- `The system should support 100k events/sec with burst handling.`
- `Promotion to production must be strongly consistent and auditable.`

Weak examples:

- `The system should be scalable.`
- `The system should be reliable.`
- `The system should be secure.`

These may be true, but they do not yet guide the design.

## Common Failure Modes

### 1. Solving the whole product

Symptom:

The user lists every obvious feature instead of selecting the core loop.

Coaching:

`Pick the one workflow that creates the most value and optimize for that first.`

### 2. Confusing entities with requirements

Symptom:

The user starts naming tables, services, or APIs before clarifying what matters.

Coaching:

`Stay at the product and system behavior level first.`

### 3. Generic non-functional requirements

Symptom:

NFRs are unquantified or do not map to concrete hotspots.

Coaching:

`Tell me which operation needs that property, and how strong the requirement is.`

### 4. Missing the design-defining trade-off

Symptom:

The user never identifies the critical tension, such as write throughput vs durability or availability vs consistency.

Coaching:

`Which requirement would most change the architecture if I changed it?`

## Feedback Template

Use a compact coaching style:

### What was strong

- name one or two real strengths

### What to tighten

- point out the biggest misses

### Suggested improved requirement set

- provide a tighter set of 3 functional and 3 non-functional requirements

### Ideal follow-up questions

- list the top questions that would have unlocked the strongest scope

## Example Of A Strong Compression

Broad prompt:

`Design a platform for rolling out workflow updates using production feedback.`

Weak requirement set:

- users can upload workflows
- users can manage teams
- users can view dashboards
- users can configure alerts
- users can run evaluations
- users can deploy versions

Stronger requirement set:

- customers can ingest production traces and corrections
- customers can freeze a reproducible evaluation snapshot from recent traces
- customers can evaluate and safely roll out a new version with rollback

Stronger NFRs:

- trace ingestion should acknowledge within `<200ms p99`
- approved evaluation snapshots must be immutable and auditable
- production promotion must be strongly consistent and support rollback
