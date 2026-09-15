# Security policy

## Reporting a vulnerability

Do not open a public issue for a suspected vulnerability, access token, private report, personal information, or customer data.

Report security concerns through [Instaseer contact](https://www.instaseer.com/contact) and include only the minimum information needed to reproduce the issue. Remove secrets and personal data from screenshots and logs.

## Supported service

This repository documents the hosted MCP server at `https://www.instaseer.com/mcp`. Security fixes are deployed to the hosted service rather than distributed as releases from this documentation repository.

## Credential safety

- Complete authorization only on `https://www.instaseer.com`.
- Do not paste OAuth tokens, scoped keys, or private report contents into GitHub issues.
- Revoke a connection in Instaseer if a credential may have been exposed.
- Use the narrowest report permissions and scopes that satisfy the workflow.
