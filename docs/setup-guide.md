# Setup Guide

## 1. Import the workflow

Import:

```text
workflow/ai_business_inquiry_automation.json
```

The public export is sanitized, so credentials and resource IDs must be reconfigured.

## 2. Configure Google Gemini

Connect the Gemini nodes to your Google Gemini credential or supported n8n AI gateway.

Gemini is used for:

- semantic inquiry classification
- Sales response drafting
- Technical Support response drafting
- General Inquiry response drafting

## 3. Create the Google Sheets tracker

Create a worksheet called `Inquiries` with:

```text
Name
Email
Request
category
submittedAt
draftReply
reviewStatus
inquiryId
reviewedAt
deliveryStatus
sentAt
deliveryError
```

Open every Google Sheets node and point it to your own spreadsheet.

## 4. Connect Gmail

Configure Gmail credentials for:

- internal approval requests
- approved outbound test messages

During development, use only inboxes you control.

## 5. Replace placeholders

The public workflow contains placeholder addresses/resources such as:

```text
reviewer@example.com
test-recipient@example.com
YOUR_GOOGLE_SHEET_ID
```

Replace them inside your private n8n instance.

## 6. Verify approval logic

For each category, confirm:

```text
Approval request
→ Check approval decision
   → True: Approved update → Send approved email
   → False: Rejected update → Stop
```

There must be no outbound-email path from a rejected branch.

## 7. Verify update keys

All later updates should match the Google Sheets row using:

```text
inquiryId
```

## 8. Test all categories

Run at least:

- Sales Approve
- Sales Reject
- Technical Support Approve
- Technical Support Reject
- General Inquiry Approve
- General Inquiry Reject

Then test a delivery failure path in a controlled environment.

## 9. Public-repository check

Before publishing a new export, search for:

- personal email addresses
- spreadsheet IDs
- `credentials`
- `webhookId`
- API keys/tokens
- real customer information

Publish only a sanitized export.
