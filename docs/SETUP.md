# Setup

Use the [hosted connection guide](https://www.instaseer.com/mcp) for the current entry point. These are protocol setup instructions, not certification for a particular assistant or plan.

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

The `mcp-v5-1` source contract defines these scopes. The hosted consent screen and the permissions returned for your connection determine what is actually granted; this reference does not enable access.

| Scope | Purpose |
| --- | --- |
| `instaseer:usage:read` | Read account access and credit status |
| `instaseer:reports:read` | List and read permitted saved reports |
| `instaseer:research:request` | Prepare research requests for owner review |
| `instaseer:free-tools:run` | Run permitted bounded tool operations |
| `instaseer:library:read` | Read permitted saved analyses, shortlists, and boards |
| `instaseer:library:write` | Save permitted evidence to the library |

Report access can be narrower than the scope itself. A report that is not permitted or whose access period has ended will not become readable merely because the connection has `instaseer:reports:read`.

Free collection requires a separate collection grant and available shared web allowance. Saving evidence requires the explicit library-write grant. Reading saved research does not authorize either action, and connection permission does not authorize spending.

## First connection check

Ask:

> List the Instaseer reports I can access.

A successful list followed by a successful report read confirms access to that permitted evidence. It does not certify every tool or client workflow. Checking access and reading saved evidence do not start a new collection.

## Fresh research

The assistant may prepare a request when `instaseer:research:request` is authorized. With `fresh: true`, the tool returns a review operation and credit quote. It does not approve, charge, or start collection.

Open the returned Instaseer review link. Confirm the account, requested scope, and credit cost there. A message inside the assistant cannot approve a charge.

If a request is retried, reuse the same `request_key`. For a request already created, use `instaseer_research_status` instead of creating another one.

## Discover tools and use saved results

Use the tool list and input schema exposed by your connected client. When available, `instaseer_discover_tools` reports capabilities, evidence requirements, and enabled state. Choose only a mode and capability permitted for the connection.

- `manual` uses supplied inputs; `owned` reuses permitted saved evidence. Both are free.
- `free` collection uses its separate grant and the account's shared web allowance.
- Reuse the same `request_key` when retrying `instaseer_run_tool`. Read or resume an accepted operation with `instaseer_read_tool` instead of starting a duplicate.
- Save exact permitted evidence with `instaseer_save_tool` only when library-write permission is explicitly granted.

See the [tool reference](TOOLS.md) for operation-specific inputs and evidence boundaries.

## Troubleshooting

### Expired or revoked credentials

Reconnect through OAuth. Reconnecting does not restore report access that has expired.

### A saved report is missing

Check the connection's report permissions and the report's access period in Instaseer. Select the exact report in the library if the connection is intentionally restricted.

### A tool is absent or disabled

Check the connected client's discovered tool list and, when available, the enabled state returned by `instaseer_discover_tools`. A tool documented in the source contract may not be available to this hosted connection. Report the limitation rather than assuming it is enabled or creating repeated requests.

### Research is waiting

Open the review link returned by Instaseer. The account owner must act in Instaseer before fresh collection can begin.

### Service unavailable

Retry the connection check later. Do not create repeated fresh-research requests. Saved research and already approved work stay attached to the Instaseer account.

### Client-specific setup

Menu names and remote-MCP availability change across client products and plans. Consult the client's current official documentation if it does not accept a remote Streamable HTTP server URL or cannot complete OAuth.
