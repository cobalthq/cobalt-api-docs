---
weight: 2
title: API Versions
---

# API Versions

<aside class="warning">
You are currently viewing the documentation of v1 of Cobalt API. <a href="/v2">Click here</a>
for the documentation of v2 of Cobalt API.
</aside>

## Background

When the Cobalt API was introduced in 2021, it was read-only but plans were already in place to add
write support. Initially this was envisioned as being added to `v1` of the API.

A close examination of `v1` of the API will reveal an odd mix of identifiers - numeric IDs, tokens,
and so on. For the sake of simplicity and consistency Cobalt decided to migrate to a common identifier
format. Due to the difficulty of maintaining full compatibility across different combinations of
identifiers, we decided to introduce `v2` of the API exclusively using the new identifier format.

`v1` is currently maintained but will not see any new features.
