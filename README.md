# Ternivo Connect for OpenClaw

Ternivo Connect gives OpenClaw users a controlled remote-MCP interface for authorized social-media operations.

This repository is an **Agent Plugins 1.0** bundle that OpenClaw can map into its native skill and MCP surfaces.

## What it provides

- social-account discovery and connection health
- provider capability checks
- preflight before publish/schedule
- publishing and scheduling where provider access permits
- approval-policy enforcement
- terminal delivery receipts
- targeted retries and diagnostics
- supported analytics, inbox/community, listening, creator and calendar workflows

Ternivo keeps social-provider credentials server-side. The OpenClaw agent authenticates to Ternivo rather than receiving raw provider credentials.

## Install from GitHub

With OpenClaw installed:

```bash
openclaw plugins install https://github.com/homesteadliving/ternivo-openclaw
openclaw plugins inspect ternivo-openclaw
```

The bundle contributes the remote MCP server:

```text
https://ternivo.app/mcp
```

using the `streamable-http` transport.

## Authentication

Ternivo uses OAuth for customer authorization. OpenClaw owns the client-side authorization flow. If the installed bundle requires authorization, complete the Ternivo OAuth consent flow when OpenClaw requests it.

You can also register the server directly:

```bash
openclaw mcp add ternivo --url https://ternivo.app/mcp --transport streamable-http
openclaw mcp login ternivo
openclaw mcp probe ternivo
```

If your OpenClaw version uses the manual OAuth fallback, follow the authorization URL printed by `openclaw mcp login` and then complete the code step it reports.

## Verify

After installation:

```bash
openclaw plugins list
openclaw plugins inspect ternivo-openclaw
openclaw mcp probe ternivo
```

A successful probe should discover Ternivo MCP capabilities after authorization.

## Security model

- Provider passwords and raw provider OAuth tokens are not exposed to OpenClaw.
- Customer organization/workspace isolation is enforced by Ternivo.
- Provider capability state remains authoritative.
- Public writes remain subject to preflight and organization/provider policy.
- Provider acceptance is not represented as final delivery until terminal evidence exists.
- Paid-media activation requires separate human approval.

## Public distribution

This repository is structured so it can be published to **ClawHub** as an OpenClaw-compatible bundle package.

ClawHub publishing uses:

```bash
clawhub login
clawhub package publish homesteadliving/ternivo-openclaw
```

Use `--dry-run` first when publishing from a new ClawHub account.

## Links

- Ternivo Connect: https://ternivo.app/social-delivery
- Developer documentation: https://ternivo.app/developers
- Privacy: https://ternivo.app/connect/privacy.html
- Security: https://ternivo.app/connect/security.html
- Support: https://ternivo.app/connect/support.html
