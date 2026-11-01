# Billing

Billing defines how a user or organization pays for NeuroStack resources. Billing setup is part of account creation, and the billing status determines what the user can do on the platform.

## Billing setup

During billing setup, the user chooses how they will pay for NeuroStack resources. NeuroStack supports three billing arrangements:

- **Card** — the user pays personally with a payment card validated through the payment provider.
- **Invoice** — the user pays personally by invoice, with payment by bank transfer.
- **Internal billing code** — the user's company pays for NeuroStack under an existing corporate agreement.

After the chosen billing arrangement is verified, billing becomes Active and the user can create workspaces and use paid resources.

## Paying personally

Users who pay personally can choose between two payment methods:

### Card

The user adds card details during billing setup. Card details are validated through the payment provider, and verification is usually immediate.

If validation fails, the billing status changes to Failed. The user sees a general message and can correct the card details and retry, or choose a different billing arrangement. NeuroStack does not display detailed bank decline reasons.

### Invoice

The user provides company and billing details and receives an invoice. Invoice verification can take up to 5 business days, provided all required information has been submitted.

If additional information or supporting documents are required, NeuroStack contacts the applicant by email. Verification may take longer if the requested information has not yet been received. The verification process resumes when the applicant provides the required information.

When verification is complete, NeuroStack sends an email to the account email address, and the billing status changes to Active.

## Internal billing code

An internal billing code connects an employee's NeuroStack account to an existing corporate billing agreement. It is issued by NeuroStack or an authorized account manager and is not a payment method or promotional code.

Employees joining an existing corporate agreement do not need to establish an individual billing arrangement. Charges for their use of NeuroStack are handled under the organization's corporate agreement.

The code is used during the initial connection to the corporate agreement, not at every login.

## Billing statuses

The following statuses apply to billing:

| Status | When used | What is available |
|---|---|---|
| Pending | A paid-plan billing setup has been submitted but has not yet passed initial verification. | Workspace creation is unavailable until verification is complete. |
| Failed | Verification of the billing setup has finally failed. | The user must correct the details or choose a different billing arrangement. |
| Active | Verification has passed and there is no overdue debt. | The user can create workspaces and use paid resources. |
| Payment overdue | The payment due date has passed and payment has not been received. | New paid resources cannot be created. Existing resources continue to run during the grace period. |
| Suspended | The grace period has ended without payment. | Paid resources are unavailable; running resources are stopped. |

## Billing cycle

The billing cycle for an individual paid plan begins when the billing status becomes Active and repeats every 30 days.

Charges are collected according to the selected billing arrangement:

- **Card** — charges are billed automatically to the card.
- **Invoice** — invoices are issued once every 30 days and paid by bank transfer.
- **Internal billing code** — charges are billed to the organization under the corporate agreement, using the same 30-day invoice cycle.

Invoices are due within 30 days of issuance. Account activation does not depend on whether any charges have been paid.

For Enterprise, the billing cycle is established at the corporate agreement level. Adding an employee to an existing corporate agreement does not start or reset the organization's billing cycle.

Selecting a plan does not start a billing cycle. The Free plan has no paid billing cycle and does not incur usage charges.

## Payment overdue and grace period

If a payment due date passes without payment, the billing status transitions to Payment overdue, and a seven-day grace period begins.

During the grace period:

- The user cannot create new paid resources.
- Existing resources continue to run.
- The user is notified that payment is overdue and shown the date when resources will be stopped if payment is not received.

If payment is received during the grace period, the billing status returns to Active. Existing resources continue to run without interruption.

If payment is not received by the end of the grace period, the billing status transitions to Suspended, and running resources are stopped.

If payment is received after billing has transitioned to Suspended, the billing status returns to Active. Stopped resources are not restarted automatically; the user must start the required resources manually.

A failed recurring charge is an event within the Payment overdue state, not a status change to Failed.

## Related docs

- [Create account](../getting_started/create_account.md)
