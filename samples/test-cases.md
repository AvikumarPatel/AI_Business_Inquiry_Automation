# Test Cases

All records below are fictional.

| Scenario | Expected category | Reviewer action | Expected delivery |
|---|---|---|---|
| Bulk sensor pricing | Sales - Quote Request | Approve | Sent |
| Quote/discount request | Sales - Quote Request | Reject | Not sent |
| Sensor malfunction | Technical Support | Approve | Sent |
| Detection failure | Technical Support | Reject | Not sent |
| Product catalogue request | General Inquiry | Approve | Sent |
| Educational documentation | General Inquiry | Reject | Not sent |

## Semantic classification example

**Name:** Robert Joseph  
**Email:** robert@example.com

**Request:**

> How much would 50 proximity sensors cost? Please share pricing.

Expected category:

```text
Sales - Quote Request
```

This request intentionally avoids the word `quote` to demonstrate semantic classification.

## Sales — Approve

**Name:** Ethan Walker  
**Email:** ethan@example.com

> We are planning to purchase 90 industrial proximity sensors for a new production line. Could you provide pricing information, bulk order options, and estimated delivery timelines?

Expected:
- `reviewStatus = Approved`
- `deliveryStatus = Sent`
- `reviewedAt` populated
- `sentAt` populated

## Technical Support — Approve

**Name:** Laura Mitchell  
**Email:** laura@example.com

> Our industrial temperature sensor is showing inconsistent readings and occasionally stops communicating with the controller. Could your technical team help us identify possible causes and what information we should collect for troubleshooting?

Expected:
- `category = Technical Support`
- approved path reaches outbound-email node
- delivery outcome recorded

## General Inquiry — Approve

**Name:** Noah Bennett  
**Email:** noah@example.com

> Hello, I am researching industrial automation solutions for our facility. Could you share general information about the types of sensors, controllers, and automation technologies your company offers?

Expected:
- `category = General Inquiry`
- `reviewStatus = Approved`
- `deliveryStatus = Sent`

## Rejection behavior

For any category, selecting **Reject** must:

- update `reviewStatus = Rejected`
- populate `reviewedAt`
- not execute the customer-facing outbound Gmail node
- leave `sentAt` blank

## Delivery failure behavior

If an approved outbound message fails:

- `reviewStatus` remains `Approved`
- `deliveryStatus = Failed`
- `deliveryError` contains the captured error
- `sentAt` remains blank
