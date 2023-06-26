---
weight: 2
title: API Versions
---

# API Versions

<aside class="warning">
You're viewing the documentation for an older version of the Cobalt API (v1). Please visit the <a href="https://docs.cobalt.io/v2/">documentation</a>
for the latest version (v2). If you've integrated with the Cobalt API in the past using v1,
please see the <a href="https://docs.cobalt.io/v2/#changelog">Changelog</a> to migrate to v2.
</aside>

## Background

When we introduced the Cobalt API in 2021, it was read-only. Initially, we planned to add write support to v1 of the API.

After a careful review of v1, we discovered an odd mix of identifiers—numeric IDs, tokens,
and so on. We decided to switch to a common identifier format for simplicity and consistency.
Because it's difficult to maintain full compatibility between different combinations of
identifiers, we decided to introduce v2 of the API that uses only the new identifier format.

We maintain v1 of the API, but we won't add any new features to it.
