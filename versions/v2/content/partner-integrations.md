---
weight: 16
title: Partner Integrations
---

# Partner Integrations

We request that you set a custom `User-Agent` header when developing a partner integration.
The custom `User-Agent` header should identify your integration.
This allows us to identify traffic originating from your integration for analytical and troubleshooting purposes.

Format:
`User-Agent: [IntegrationName]/[IntegrationVersion]`

Example:
`User-Agent: PartnerCobaltIntegration/1.0.0`

The `User-Agent` header is not required, but we strongly encourage partner integrations to send this header.
