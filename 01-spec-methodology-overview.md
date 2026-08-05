# Spec Methodology: First Principles

As of 2026-08-05, the current direction in spec methodology is strongly shaped by AI-assisted software development. The core idea is simple:

> Agree on intent before implementation.

Specs are no longer treated as throwaway documentation. In modern spec-driven workflows, specs become the shared source of truth between humans, teams, and AI coding agents.

## The Core Problem

AI can generate code quickly, but fast code generation creates risk when the intent is unclear.

Common failure modes:

- The code works, but solves the wrong problem.
- The agent makes hidden design assumptions.
- Requirements live only in chat history.
- Reviewers inspect code without understanding the intended behavior change.
- Future changes become harder because the "why" is missing.

Spec methodology addresses this by putting structured thinking before code.

## The Basic Loop

Most current spec-first tools follow this pattern:

1. Specify what should change.
2. Clarify ambiguity.
3. Plan the technical approach.
4. Break the work into tasks.
5. Implement from the tasks.
6. Validate that implementation matches the spec.
7. Archive or merge the updated spec into the system truth.

In short:

```text
Intent -> Spec -> Plan -> Tasks -> Code -> Validation -> Living Spec
```

## Two Important Modern Flavors

### GitHub Spec Kit

GitHub Spec Kit describes Spec-Driven Development as an intent-driven process where specs define what to build before the coding agent implements it. Its current docs emphasize a core SDD process:

```text
Spec -> Plan -> Tasks -> Implement
```

It also includes optional quality gates such as clarify, checklist, analyze, and converge. The newer Spec Kit docs describe the toolkit as extensible, with integrations, extensions, presets, workflows, and bundles.

Useful source:

- https://github.github.io/spec-kit/
- https://github.github.com/spec-kit/concepts/sdd.html
- https://github.github.com/spec-kit/reference/agentic-sdd.html

### OpenSpec

OpenSpec frames itself as a lightweight agreement layer between the developer and AI. Its mental model is:

```text
Agree first, then build confidently.
```

OpenSpec separates current system truth from proposed changes:

- `openspec/specs/` contains current behavior.
- `openspec/changes/` contains proposed behavior changes.
- Each change can include a proposal, design, tasks, and spec deltas.

Useful source:

- https://openspec.dev/
- https://openspec.dev/docs/overview
- https://openspec.dev/docs/reference/cli

## What A Good Spec Contains

A useful spec is not a long essay. It should answer:

- What behavior should exist?
- Who needs it?
- Why does it matter?
- What should happen in concrete scenarios?
- What is out of scope?
- What constraints must the solution respect?
- How will we know it is done?

The best specs are precise enough to guide implementation, but not so rigid that they prematurely dictate every internal code detail.

## Key Vocabulary

- **Intent**: The real goal behind the requested change.
- **Requirement**: A statement of expected behavior.
- **Scenario**: A concrete example, often written as given/when/then.
- **Proposal**: A description of a change before implementation.
- **Design**: The technical approach for satisfying the spec.
- **Tasks**: Implementation steps derived from the spec and design.
- **Validation**: Proof that the result matches the agreed behavior.
- **Living spec**: A spec that remains updated after implementation.

## First Principle To Remember

Spec methodology is not about writing more documents.

It is about reducing ambiguity before code exists, so humans and AI are building the same thing.

## Next Lesson

Next, learn the smallest possible useful spec:

```text
Problem -> User -> Requirement -> Scenario -> Acceptance Check
```

