# Implementation Notes

## Semantic classification

The first version of the project used a simple keyword check for the word `quote`. It was upgraded to a Gemini Text Classifier so intent can be recognized from meaning.

A representative test request was:

> How much would 50 proximity sensors cost? Please share pricing.

Even without the word `quote`, the classifier correctly routed the request to **Sales - Quote Request**.

## Response generation

Separate prompts are used for Sales, Technical Support, and General Inquiry. Each prompt is constrained to avoid fabricated business facts.

## Human approval

The Gmail approval node returns a response containing an `approved` Boolean and response timestamp. An IF node uses the Boolean to select the approved or rejected branch.

Rejected branches update the record and stop. Approved branches update the record and proceed to controlled outbound email.

## Stable record matching

The workflow originally used timestamps for row matching. It was improved by adding a unique `inquiryId` generated from the n8n execution ID.

## Delivery tracking

Successful sends update `deliveryStatus` and `sentAt`.

Failed sends follow a dedicated error output, set `deliveryStatus = Failed`, capture `deliveryError`, and update the same inquiry row by `inquiryId`.

## Final workflow corrections

During final review, the public portfolio workflow was corrected to:

- remove an unintended direct Technical Support connection that bypassed the approval-wait step
- correct the General Inquiry outbound-email subject
- standardize the Technical Support save-node name
- connect all three delivery-error branches to Google Sheets failure updates
- normalize worksheet display naming
- validate expression node references and connection targets
- sanitize account-specific identifiers and credentials
