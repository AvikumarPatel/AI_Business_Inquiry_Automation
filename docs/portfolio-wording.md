# Portfolio Wording

## Resume bullets

- Built an AI-powered business inquiry automation in n8n that uses Google Gemini to classify Sales, Technical Support, and General inquiries, generate category-specific response drafts, and route messages through human approval before outbound delivery.
- Integrated Gmail and Google Sheets to track unique inquiry IDs, approval/rejection status, review and send timestamps, and delivery failures, with rejected drafts prevented from entering the customer-email path.

## Short project entry

**AI-Powered Business Inquiry Automation | n8n, Google Gemini, Gmail, Google Sheets**

Designed an end-to-end workflow that captures customer inquiries, uses Gemini to classify intent and draft context-aware responses, requires human approval before sending, and tracks approval and delivery status using unique inquiry IDs. Added separate success and failure paths so unsuccessful email delivery is recorded rather than silently lost.

## Interview explanation

> I wanted hands-on experience with workflow automation and AI integration, so I built an n8n workflow around a realistic industrial-business inquiry process. A form submission gets a unique inquiry ID, Gemini classifies the request into Sales, Technical Support, or General Inquiry, and a category-specific prompt generates a draft. The record is stored in Google Sheets and an internal Gmail approval step pauses the workflow. Rejected drafts stop there; approved drafts enter the outbound email path. I also added success and error branches so the same inquiry record is updated with review timestamps, send timestamps, or delivery errors. I tested approval and rejection paths across all three categories.
