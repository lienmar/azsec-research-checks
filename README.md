# azsec-research-checks

Read-only exposure checks derived from Azure and Entra security research.

Each check tells an assessor holding **Reader** (Azure RBAC) and **Global Reader** (Entra)
whether a tenant matches a published weakness's exposure condition. A check detects a
configuration state. It never exploits, tests or probes anything.

## Lifecycle

checks/proposed/   drafted by the Research Watch Argus, opened as a PR
checks/approved/   Martin moved it here by hand. Engagements run only these.
checks/retired/    the vendor fixed it platform-side, or it no longer applies

Only Martin moves a file between directories. The Argus opens pull requests; it does not merge.

## Check format

id: RES-YYYY-NNN
title:
source: <primary URL>   published: <date>   author:
services: <Azure / Entra services and features affected>
summary: <3-5 sentences in your own words: what the weakness is, what an attacker gains>
vendor_status: <fixed platform-side on <date> | needs tenant action: <what> | by design per vendor | unknown>, with URL
exposure_condition: <the exact configuration state that makes a tenant exposed>
applicability: <how to tell from inventory whether the service or feature is present at all>
reader_query: <ARG KQL, Microsoft Graph GET paths, or az read commands — read-only only>
result_logic: <how to map output to exposed / not_exposed / not_applicable / not_assessable>
blind_spots: <what Reader and Global Reader cannot see that affects the answer>
false_positives: <known benign states that match the query>
related_baseline: <benchmark control IDs that cover this, if any>
recommendation: <what the client should change>
confidence: <high | medium | low>, with one sentence on why

A check with no `reader_query` is not a check. If the exposure cannot be detected with
these two roles, the item is logged as `no_reader_signal` in the research_items table
and no file is written.
