# Security Notes

This repository is intended for portfolio/demo use.

## Never commit

- API keys
- OAuth access/refresh tokens
- n8n credential exports
- personal reviewer addresses
- production spreadsheet IDs
- webhook secrets
- real customer information
- private company data

## Workflow export

The workflow JSON included here has been sanitized. After importing it, reconnect credentials and replace placeholder resources inside your private n8n instance.

## Email testing

During development, keep outbound message nodes pointed to inboxes you control. Validate recipient mapping, human approval behavior, and delivery-error handling before using real external recipients.
