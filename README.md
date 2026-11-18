# Union Free Compute Runner

<!-- 561-group-standards:badges:start -->
[![Red Cup Engineering](https://img.shields.io/badge/561%20Group-Red%20Cup%20Engineering-c0392b)](https://github.com/red-cup-engineering)
[![License: MIT](https://img.shields.io/badge/license-MIT-c0392b)](LICENSE)
[![bounded-public-test](https://github.com/red-cup-engineering/union-free-compute-runner/actions/workflows/bounded-public-test.yml/badge.svg)](https://github.com/red-cup-engineering/union-free-compute-runner/actions/workflows/bounded-public-test.yml)
[![Indigenous data: CARE](https://img.shields.io/badge/Indigenous%20data-CARE-4b6f44)](https://github.com/red-cup-engineering/.github/blob/main/GOVERNANCE.md)
[![Tips welcome](https://img.shields.io/badge/tips-welcome-d4a017)](https://github.com/561-group/.github/blob/main/TIPS.md)
<!-- 561-group-standards:badges:end -->

This public repository contains one secretless, bounded software-test workflow.
Inputs, source identity, and logs are public. It accepts only an exact commit in a
public repository and an optional patch of at most 48 KiB, uses a standard
`ubuntu-latest` runner for at most 15 minutes, and creates no artifacts or cache.
Do not submit proprietary source, secrets, personal data, or secret-bearing tests.


The commit-pinned entrance creates a deployment at the exact 40-hex workflow
commit with task and environment `bounded-public-test`,
`production_environment: false`, `transient_environment: true`,
`auto_merge: false` and `required_contexts: []`. Its payload supplies
`target_repository`, `target_commit` and optional `patch_base64`.
The runner checks that the deployed SHA matches its executing workflow revision
and validates the payload before receiving public source. Manual
`workflow_dispatch` accepts the same inputs.


For patches above the inline API payload limit, create at most six input
deployments at the same workflow SHA. Their task and environment are
`bounded-public-test-input`, with the same transient/non-production flags.
Each payload is exactly `{index, data}`, with zero-based ordinal and a canonical
base64 segment of at most 12,000 characters on a four-character boundary.
The final test payload supplies `patch_deployment_ids` in order,
`patch_sha256` and `patch_bytes` in place of `patch_base64`. The runner reads
these public inputs from its own GitHub repository, verifies their identities,
and admits the assembled patch only after its exact byte count and SHA-256
match. The decoded patch limit remains 48 KiB.


## Source ownership and writable data

Continuous Delivery owns this application:
https://github.com/red-cup-engineering/continuous-delivery-engineering-services-section .
Its canonical source is https://github.com/red-cup-engineering/union-free-compute-runner .
The original repository identity and three manual assays are preserved.
The retired pinned automatic branch-intake caller is removed under its original
Continuous Delivery retirement contract; it is not a test or dispatch entrance.

The bounded public workflow puts its exact checkout, optional patch, package
caches, Go/Cargo state and temporary files under `data/logs/bounded-public-test-logs`.
Python installs use an owned virtual environment with the standard runner's
existing packages visible; no user or system install is requested. Rust uses
the runner's already installed compiler directly, with owned Cargo state.
The Deno assay writes its three response logs under `data/logs/deno-assay-logs`.
Existing path redirects and wrong owners are refused before creation. `HOME`
is unchanged. These bindings cover the authored workflows and tool selectors;
they do not promise confinement of arbitrary public candidate test code or
rewrite the hosted runner's internal supplier paths.

No dispatch, platform availability or external Deno signing admission follows
from source custody. The public-source restriction above still applies; this
runner is not a route for private repository CI.
