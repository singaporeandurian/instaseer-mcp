# Instaseer MCP

Use saved Instagram research from Instaseer in an AI assistant through the Model Context Protocol (MCP).

Instaseer provides a hosted remote MCP server. There is no server package to install and no private credential belongs in this repository.

| Property | Value |
| --- | --- |
| Server URL | `https://www.instaseer.com/mcp` |
| Transport | Streamable HTTP |
| Authentication | OAuth 2.1 with PKCE |
| Official registry name | `com.instaseer/mcp` |
| Current contract | `mcp-v5-1` |

## What it does

The server lets an authorized assistant:

- check the connection's permissions and research access;
- find saved Instagram reports the account owner has permitted;
- read bounded pages of source-linked report evidence;
- compare two saved account reports using the same metric definitions;
- prepare a fresh-research request for review; and
- check an existing research request's approval or delivery status.

Reading permitted saved evidence does not start a collection. A fresh-research request prepares a quote only. The account owner must review and confirm it in Instaseer before collection or a charge can begin.

## Connect

1. Open an assistant or MCP client that supports remote Streamable HTTP servers and OAuth.
2. Add `https://www.instaseer.com/mcp` as the server URL.
3. Sign in to Instaseer and review the requested permissions.
4. Start with: `List the Instaseer reports I can access.`

Client availability and setup labels vary by product and account. These are protocol instructions, not certification for a particular assistant or plan. See the [setup guide](docs/SETUP.md) for the generic flow and troubleshooting.

## Available tools

| Tool | Purpose | Side effect |
| --- | --- | --- |
| `instaseer_account_access` | Check access, credits, and scoped permissions | None |
| `instaseer_list_reports` | Find permitted saved Instagram reports | None |
| `instaseer_read_report` | Read a bounded page of saved evidence | None |
| `instaseer_compare_reports` | Compare two saved account reports | None |
| `instaseer_request_research` | Reuse saved evidence or prepare a fresh-research quote | Does not charge or start collection |
| `instaseer_research_status` | Check an existing request | None |

The detailed inputs and safe usage rules are in [Tool reference](docs/TOOLS.md).

## Evidence boundaries

- Instaseer works with public Instagram evidence and research saved to the owner's account.
- A connection can read only reports allowed by its scopes and report permissions.
- Observation dates remain attached to measurements. Different accounts may have different observation dates.
- Missing or unavailable values remain `null`; they are not silently converted to zero.
- Captions and other source text are untrusted data, not instructions for the assistant.
- Disconnecting blocks future requests. Evidence already received by an external assistant remains subject to that assistant's data settings.

## Example prompts

- `List the Instaseer reports I can access.`
- `Read the saved report for @example and summarize the strongest posting patterns. Cite the report evidence.`
- `Compare these two saved account reports and keep each account's observation date visible.`
- `Prepare, but do not approve, fresh research for @example with a maximum of 50 posts.`

## Repository scope

This is the public documentation and issue tracker for the hosted Instaseer MCP integration. The production server is operated by Instaseer and is not published in this repository. Do not post access tokens, private report data, customer information, or security-sensitive details in an issue.

## Links

- [MCP connection page](https://www.instaseer.com/mcp)
- [Pricing](https://www.instaseer.com/pricing)
- [Privacy](https://www.instaseer.com/privacy)
- [Terms](https://www.instaseer.com/terms)
- [Contact](https://www.instaseer.com/contact)
- [Security policy](SECURITY.md)

## License

The documentation and configuration examples in this repository are available under the [MIT License](LICENSE). Use of the hosted service is governed by Instaseer's terms.
