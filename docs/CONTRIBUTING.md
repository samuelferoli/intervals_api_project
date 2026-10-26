# Contribution and learning workflow

## Project ownership

Samuel Fernandes is the project owner and decision maker. AI assistance supports his understanding and implementation. The initial documentation was drafted with AI assistance from the project discussion and is submitted for human review.

## Language

Use English in discussions, documentation, code, identifiers, comments, issues, commits, and pull requests. Keep established API field names unchanged. Language corrections should help communication without replacing the technical discussion.

## Suggested working loop

1. Describe the problem or expected behavior.
2. Explain your proposed approach and assumptions.
3. Discuss alternatives or request a hint.
4. Implement a small, reviewable change.
5. Verify it with checks appropriate to the risk.
6. Explain the result and update documentation when behavior or decisions change.

This is a proposed development workflow, not permission for an assistant to complete unrelated work.

## Changes and review

Use focused branches and pull requests to keep changes reviewable. Branch naming, issue labels, milestones, and required automated checks have not been established yet.

A pull request should explain:

- The problem and scope.
- The proposed or implemented change.
- Important decisions and alternatives.
- Evidence from checks actually performed.
- Remaining risks, questions, and follow-up work.

Do not treat an unchecked task as complete. Keep observed behavior separate from expected behavior.

## Documentation

Update the [decision log](decisions.md) when a choice is accepted, rejected, or superseded. Preserve the rationale and relevant evidence.

Before accepting a metric, document its purpose, grain, inputs, units, missing-value behavior, and calculation. Use business questions to guide the data model rather than designing tables only to demonstrate a tool.

## Private data and public examples

Use synthetic data in committed fixtures, examples, screenshots, and demonstrations. Do not publish credentials, raw personal API responses, route coordinates, or database exports.

The real application requires personal authentication even though it has only one intended user. The authentication design remains open.

## Verification

Documentation changes need link and consistency review. Code changes need meaningful checks suited to the behavior they introduce. Deployment and integration claims require actual evidence.

## Definition of a reviewable change

A change is ready for Samuel's review when its scope is clear, relevant checks are reported honestly, documentation matches the result, and unresolved questions are visible. Review readiness does not mean implementation or deployment is approved automatically.
