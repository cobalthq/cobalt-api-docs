---
weight: 2
title: API Versions
---

# API Versions

## Background

When the Cobalt API was introduced in 2021, it was read-only but plans were already in place to add
write support.  Initially this was envisioned as being added to `v1` of the API.

A close examination of `v1` of the API will reveal an odd mix of identifiers - numeric IDs, tokens,
etc.  For the sake of simplicity and consistency Cobalt decided to migrate to a common identifier
format.  Due to the difficulty of maintaining full compatibility across different combinations of
identifiers, we decided to introduce `v2` of the API exclusively using the new identifier format.

As of March 2022 the plan is to go forward with write support in `v2`.  `v1` is currently maintained
but will not see any major new features.
