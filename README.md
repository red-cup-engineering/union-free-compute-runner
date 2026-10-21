# Union Free Compute Runner

This public repository contains one secretless, bounded software-test workflow.
Inputs, source identity, and logs are public. It accepts only an exact commit in a
public repository and an optional patch of at most 48 KiB, uses a standard
`ubuntu-latest` runner for at most 15 minutes, and creates no artifacts or cache.
Do not submit proprietary source, secrets, personal data, or secret-bearing tests.


## Source ownership and writable data

Continuous Delivery owns this application:
https://github.com/red-cup-engineering/continuous-delivery-services-section .
Its canonical source is https://github.com/red-cup-engineering/union-free-compute-runner .
The original repository identity, tag and three manual assays are preserved.
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
