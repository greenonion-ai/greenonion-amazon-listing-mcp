# GreenOnion Amazon Listing Images MCP

Use GreenOnion from ChatGPT, Codex, Claude, or another MCP client to plan a coordinated Amazon listing image set from your product photos.

[GreenOnion Product Images](https://greenonion.ai/mcp) is a live ChatGPT plugin and remote Model Context Protocol service for Amazon sellers, brands, and agencies. It plans the role of every image before generation: main image, feature infographics, lifestyle scenes, detail views, comparisons, and related listing visuals.

## Choose the right connection

| Client | What GreenOnion does | How to connect |
| --- | --- | --- |
| ChatGPT | Accepts attached product photos, plans and revises the nine-image set, generates selected 2K images, reports progress, and returns the private project and eligible ZIP download. | In ChatGPT, open Plugins and search for **GreenOnion Product Images**. |
| Codex | Connects to the production Amazon listing MCP server over Streamable HTTP and OAuth. Available tools depend on the host's support for attachments and interactive results. | Use the command below. |
| Claude | Builds and revises the nine-image plan from public product-photo URLs or a GreenOnion upload link, then opens the confirmed plan in GreenOnion for generation. | Add the planner URL as a custom connector. |
| Other MCP clients | Can connect to the remote endpoint when they support Streamable HTTP and OAuth 2.1. Attachment and UI support varies by client. | Add the production URL in the client's MCP settings. |

## Connect from Codex

```bash
codex mcp add greenonion --url https://api.greenonion.ai/plugins/amazon-listing/mcp
```

The first use opens GreenOnion sign-in. Approve the requested access, then try:

> Make a full Amazon listing image set from this product photo.

## Connect from Claude

Open **Settings → Connectors → Add custom connector** and enter:

```text
https://mcp.greenonion.ai/plugins/listing-planner/mcp
```

Then ask:

> Plan Amazon listing images for this product: https://example.com/product-photo.jpg

Claude cannot pass a normal chat attachment to this connector. Use a public HTTPS image URL or ask GreenOnion for a private upload link. The [Claude setup guide](https://greenonion.ai/help/claude-connector) documents the complete flow and all planner tools.

## Remote endpoints

### Amazon listing image server

```text
https://api.greenonion.ai/plugins/amazon-listing/mcp
```

This is the production endpoint used by the GreenOnion Product Images plugin. It exposes the authenticated Amazon listing workflow, including draft creation, product analysis, plan revisions, selected-image generation, job recovery, and eligible downloads.

OAuth protected-resource metadata:

```text
https://api.greenonion.ai/.well-known/oauth-protected-resource/plugins/amazon-listing/mcp
```

### Listing planner server

```text
https://mcp.greenonion.ai/plugins/listing-planner/mcp
```

This endpoint is designed for planner-first integrations. It creates and revises a listing plan and returns a GreenOnion generation link rather than generating images inside Claude.

OAuth protected-resource metadata:

```text
https://mcp.greenonion.ai/.well-known/oauth-protected-resource/plugins/listing-planner/mcp
```

## What the Amazon listing workflow does

1. Reuses product photos, facts, and preferences already supplied in the conversation when the host can provide them.
2. Analyzes the product and proposes a coordinated nine-image plan with a role and feature assignment for every image.
3. Lets the seller revise facts, design choices, image types, included slots, exact wording, and scene direction.
4. Generates the confirmed selected images in the ChatGPT workflow, or hands a confirmed planner draft to GreenOnion when the host cannot run generation directly.
5. Keeps the work private in the connected GreenOnion account and supports resumable jobs.

## Authentication, credits, and data

- Both endpoints use OAuth 2.1. Do not put a GreenOnion password or token in an MCP configuration file.
- Connecting and planning do not use GreenOnion credits. Final image generation uses credits already available in the connected account.
- Product photos, plans, and generated images are stored privately in the connected GreenOnion account.
- Disconnecting an MCP client stops future access. It does not delete projects already saved in GreenOnion.
- See the [Privacy Policy](https://greenonion.ai/privacy-policy) and [Terms of Service](https://greenonion.ai/terms-conditions).

## Support

- Product and installation guide: <https://greenonion.ai/mcp>
- Claude connector reference: <https://greenonion.ai/help/claude-connector>
- Support: <hello@greenonion.ai>
- Security reports: <security@greenonion.ai>

GreenOnion is independent and is not affiliated with or endorsed by Amazon. Review all generated text, claims, and product details before publishing.

## About this repository

This repository contains public integration documentation and registry metadata for GreenOnion's hosted MCP servers. The production server implementation is not distributed from this repository.
