# Setup

## Requirements

- An Instaseer account
- An MCP client that supports remote Streamable HTTP servers
- OAuth support in the client

## Connect with OAuth

1. In your MCP client, choose the option to add a remote or custom MCP server.
2. Enter `https://www.instaseer.com/mcp`.
3. Continue to the Instaseer sign-in and consent screen.
4. Review the requested scopes and choose which saved research the connection may access.
5. Return to the client and ask it to list accessible reports.

Instaseer publishes OAuth discovery metadata for the MCP resource. A compatible client should discover the authorization flow from the server URL.

## Permissions

The current integration uses these scopes:

| Scope | Purpose |
| --- | --- |
| `instaseer:usage:read` | Read account access and credit status |
| `instaseer:reports:read` | List and read permitted saved reports |
| `instaseer:research:request` | Prepare research requests for owner review |

Report access can be narrower than the scope itself. A report that is not permitted or whose access period has ended will not become readable merely because the connection has `instaseer:reports:read`.

## First connection check

Ask:

> List the Instaseer reports I can access.

A successful list followed by a successful report read confirms that the assistant can use the permitted research. Checking access and reading saved evidence do not start a new collection.

## Fresh research

The assistant may prepare a request when `instaseer:research:request` is authorized. With `fresh: true`, the tool returns a review operation and quote. It does not approve, charge, or start a provider.

Open the returned Instaseer review link. Confirm the account, scope, maximum cost, and funding method there. A message inside the assistant cannot approve a charge.

If a request is retried, reuse the same `request_key`. For a request already created, use `instaseer_research_status` instead of creating another one.

## Troubleshooting

### Expired or revoked credentials

Reconnect through OAuth. Reconnecting does not restore report access that has expired.

### A saved report is missing

Check the connection's report permissions and the report's access period in Instaseer. Select the exact report in the library if the connection is intentionally restricted.

### Research is waiting

Open the review link returned by Instaseer. The account owner must act in Instaseer before fresh collection can begin.

### Service unavailable

Retry the connection check later. Do not create repeated fresh-research requests. Saved research and already approved work stay attached to the Instaseer account.

### Client-specific setup

Menu names and remote-MCP availability change across client products and plans. Consult the client's current official documentation if it does not accept a remote Streamable HTTP server URL or cannot complete OAuth.
