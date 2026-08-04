---
name: interview-generation
description: Generates Python coding interview practice prompts in this repository's 4-part format. Use only when the user explicitly asks to create or refine interview practice questions/prompts (not for general coding tasks).
---

# Interview Generation

## Purpose

Generate one new interview practice question as a markdown file, while avoiding overlap with existing completed scenarios in this repository.

## Workflow

### 1) Scan Existing Content First

Before generating anything:

1. List repository files and relevant subdirectories.
2. Review markdown/python files that look like prior interview questions, attempts, or solutions.
3. For each discovered question, note:
   - Topic/scenario
   - Whether tests are included
   - Whether it is a full solution vs skeleton/partial
4. Treat all discovered scenarios as completed and avoid duplicates.

Also treat these as already completed:

- Rate Limiter Service
- Task Scheduler
- In-Memory File System
- Spreadsheet Engine
- Text Editor Buffer
- Bank Account System
- OnChange Handler
- LRU Cache
- Message Broker
- Org Chart
- Snake Game

### 2) Ask Exactly Two Questions

Ask the user only these two questions, then wait for answers:

1. What style of interview should this be?
   - Implementation-focused
   - Algorithm-leaning
   - Mixed
2. Should tests be included?
   - Generate tests
   - No tests
   - Partial (Part 1 tests only)

### 3) Generate One Markdown Interview

Create a single markdown file in the repository with a descriptive name (for example, `http_router_interview.md`).

Use this interview structure:

- Part 1 (~20 min): core implementation, fully completable foundation.
- Part 2 (~15 min): extension that stresses Part 1 design.
- Part 3 (~15 min): deeper twist (state transitions, failure handling, cycle/consistency concerns).
- Part 4 (~10 min): discussion only, 3-4 production/system-design questions, including at least one scale failure question.

## Design Constraints

- Real-world framing over puzzle framing.
- Emphasize state management, edge cases, and clean implementation.
- Avoid requiring memorized niche algorithms as the core trick.
- Keep requirements precise and explicit.
- Ensure later parts build naturally from Part 1.
- Include at least one formatting/output-oriented method.

Avoid:

- Questions that hinge on topological sort/union-find/segment trees.
- Math-trick-heavy tasks (bit hacks, modular arithmetic, number theory).
- Bare data-structure exercises without realistic context.
- Trivial Part 1 with all difficulty deferred to later parts.

## Test Rules (When Tests Are Requested)

- Include `test_partN()` functions for applicable parts and call them at module level.
- Use only built-in assertions and try/except (no external dependencies).
- Use fake clock injection when time behavior is part of requirements.
- Cover happy path, edge cases, error cases, independent state, and post-mutation state.
- Use descriptive variable names.

## Skeleton Rules

- Provide a full class skeleton with `__init__` and Part 1 public methods stubbed with `pass`.
- Add type hints on method signatures.
- Include precise docstrings for behavior, args, returns, and exceptions.
- Organize code blocks as:
  - imports
  - helpers/dataclasses
  - class definition
  - Part 1 tests
  - Part 2 additions/tests
  - Part 3 additions/tests
  - Part 4 discussion
- For Part 2/3, present new methods as explicit additions to the class.
- Keep code pasteable/runnable in an IDE (failing tests are acceptable before implementation).

## Required Output Format

The generated markdown must include:

1. Title and metadata (duration, language, focus areas).
2. Background with terminology and scenario framing.
3. Parts 1-4, each with behavioral spec and code skeleton (plus tests if requested).
4. An evaluation criteria table at the end.

## Scenario Inspiration

- HTTP router with path params and middleware
- Pub/sub event system with filtering
- Simplified version control system
- Connection pool manager with health checks
- Log aggregator with time-windowed queries
- RBAC/permission system
- Package dependency resolver with conflict detection
- Circuit breaker with thresholds
- DNS resolver with TTL cache
- In-memory table with indexing/query support
- Terminal emulator subset
- Regex engine subset
- Shopping cart with discounts/tax
- Elevator simulator
- Chat room with history and presence
