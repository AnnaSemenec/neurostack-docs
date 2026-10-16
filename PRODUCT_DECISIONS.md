# Product Decisions

**Last updated:** October 2026

This document records product decisions, assumptions, and constraints made while developing the fictional NeuroStack product model.

NeuroStack is a portfolio project. Some product details are intentionally simplified or defined specifically to support the documentation exercise.

When a detail is not defined here or in the product documentation, it should not be treated as established product behavior.

---

## Product Scope

NeuroStack is a cloud platform for developing, training, deploying, and monitoring machine learning models.

The platform provides:

- managed Jupyter environments;
- CPU and GPU compute resources;
- object storage for datasets and model artifacts;
- training jobs;
- model artifacts and model management;
- API endpoints for model deployment;
- inference;
- monitoring;
- REST API and CLI access.

NeuroStack is documented as a cloud product rather than as a generic collection of ML tools.

---

## Documentation Model

The documentation follows a Docs-as-Code approach.

The documentation set is organized around:

- Overview
- Getting Started
- Concepts
- Tutorials
- How-to Guides
- Reference
- Troubleshooting
- FAQ
- Best Practices
- Release Notes
- Glossary

The documentation distinguishes between:

- **Concepts** — explain what a platform resource or concept is;
- **Tutorials** — guide users through a complete scenario;
- **How-to Guides** — explain how to complete a specific task;
- **Reference** — provide precise technical information;
- **Troubleshooting** — help users diagnose and resolve problems.

The Getting Started path follows a complete user journey from billing setup to the first model inference.

---

## Account and Billing

### Accounts and organizations

Each user has an individual NeuroStack account. Users do not share a single login for an organization.

A corporate organization has a single corporate billing account linked to a single agreement with NeuroStack. Employee accounts are linked to the corporate organization and its billing.

Workspaces are created per project, not automatically per user. One user can work in several workspaces, and several users can participate in one workspace.

### Registration and account creation

The user creates a NeuroStack account with an email address and password. After sign-up, the user verifies their email address.

Email verification codes are valid for 10 minutes, are one-time use, and allow a maximum of five incorrect attempts. Requesting a new code invalidates the previous one. Rate limits apply to code requests.

After email verification, the user is prompted to complete a billing setup.

A completed billing setup is required to create a workspace, including on the Free plan. The Free plan does not incur usage charges.

### Billing setup

A billing setup connects a user account or organization to a billing arrangement. NeuroStack supports three billing arrangements:

- **Card** — a personal or corporate card validated through the payment provider.
- **Invoice** — for organizations paying by bank transfer.
- **Internal billing code** — a corporate identifier that links a user account to an existing corporate billing agreement.

An internal billing code is not a payment method. It links the user to an existing corporate billing arrangement; charges are billed to the organization under the corporate agreement.

### Billing cycle

Usage is billed every 30 days where applicable. The Free plan does not incur usage charges.

- **Card** — charges are billed automatically to the card.
- **Invoice** — invoices are issued once every 30 days and paid by bank transfer.
- **Internal billing code** — charges are billed to the organization under the corporate agreement, using the same 30-day invoice cycle.

Account activation does not depend on whether any charges have been paid.

### Billing account statuses

The following statuses apply to a billing account:

| Status | When used | What is available |
|---|---|---|
| Pending | The billing setup has not passed initial verification yet. | Workspace creation is not available. |
| Failed | Verification of the billing setup has finally failed. | The user must correct the details or choose a different billing arrangement. |
| Active | Verification has passed and there is no overdue debt. | The user can create workspaces and use paid resources. |
| Payment overdue | The payment due date has passed and payment has not been received. | New paid resources cannot be created. Existing resources continue to run during the grace period. |
| Suspended | The grace period has ended without payment. | Paid resources are unavailable; running resources are stopped. |

If a user resubmits corrected details after a `Failed` status, the billing account returns to `Pending` until verification is complete.

`Payment overdue` is set when the payment due date has passed and payment has not been received. During the seven-day grace period, users cannot create new paid resources, but existing resources continue to run.

When the grace period ends without payment, the account transitions to `Suspended` and running resources are stopped.

After payment is received, the billing account returns to **Active**. Stopped resources are not restarted automatically; the user receives a notification and starts the required resources manually.

For card payments in `Payment overdue` status, NeuroStack retries the charge automatically. The user receives a notification about the failed charge and the date when resources may be stopped.

A failed recurring charge is an event within the `Payment overdue` state, not a status change to `Failed`.

### Corporate billing status and user access

Billing account statuses describe the billing account, not the individual user account.

If a corporate billing account is in `Payment overdue` or `Suspended`, linked employees cannot create new paid resources, even if they have no personal debt. The user interface shows the state of the corporate billing to affected users.

The personal account status of an employee is not automatically changed to `Payment overdue` when the debt belongs to the organization.

### Card verification

Card details are validated through the payment provider. Verification is usually immediate.

If validation fails, the billing account status changes to **Failed**. The user sees a general message and can correct the card details and retry, or choose a different billing arrangement. NeuroStack does not display detailed bank decline reasons.

### Invoice verification

Invoice verification can take up to 5 business days, provided all required information has been submitted.

The invoice request form collects:

- Legal business name (required);
- Country of registration (required);
- Registered business address (required);
- Bill-to address (required if different);
- Business contact name (required);
- Business contact email (required);
- Accounts payable email (required);
- Tax ID / VAT ID (required depending on the country);
- Company registration number (required depending on the country);
- Purchase order number (optional);
- Supporting documents (requested only if needed for verification).

When verification is complete, NeuroStack sends an email to the account email address, and the status changes to **Active**.

### Internal billing code

An internal billing code links a user account to an existing corporate billing agreement with NeuroStack. It is issued to an organization by NeuroStack or the organization's account manager. It is not a promotional code.

The code is a means of initial connection to the organization, not a password for each sign-in. After connecting, the user signs in normally.

The code is bound to the organization's email domain. To use the code, the user must provide a work email address on the associated domain.

Connection flow:

1. The NeuroStack account manager creates the corporate billing account and issues the code to the company.
2. The company designates an authorized billing owner for the corporate billing account.
3. The company shares the code with employees who are allowed to connect.
4. The employee signs up or signs in to their individual NeuroStack account.
5. If the corporate email address is not verified yet, the employee verifies it.
6. The employee enters the corporate code.
7. NeuroStack validates the code and checks that the email domain matches the domain associated with the code.
8. The user account is linked to the corporate organization and its billing.

If the account email address does not match the domain associated with the code, the user must provide and verify a corporate email address.

The billing owner of the corporate billing account is designated by the company when the corporate billing account is created. The first user to activate the code does not automatically become the billing owner.

For reliability, the organization should designate a second billing administrator or a recovery procedure for billing access.

### Revoking access and rotating the code

Revoking an individual employee's access and rotating the corporate code are separate operations.

**Revoking an employee's access:**

- The organization removes the employee's account from the corporate organization.
- Access to corporate resources is revoked immediately.
- Revoking access does not delete the employee's personal NeuroStack account.
- Other employees continue to work.
- The corporate code remains valid.
- The system revokes the user's membership, permissions, and, if necessary, active sessions and tokens.

**Rotating the code:**

Rotating the code is used when the code may have been compromised, shared outside the organization, or as part of planned access rotation.

When the code is rotated:

- The old code immediately stops working for new connections.
- A new code is issued to an authorized representative of the organization.
- Existing user links and active sessions are preserved.
- If the organization wants to remove specific employees, it does so separately.

Rotating the code does not automatically disconnect all existing employees.

### Billing notifications

For corporate billing, a billing contact or accounts payable contact is designated when the corporate billing account is set up. Payment notifications are sent to this contact.

If the designated contact is no longer available, the organization updates the billing contact in the corporate billing account settings.

The status of the corporate billing is shown to all linked users affected by its restrictions.

---

## Workspaces

A workspace is an isolated environment for an ML project.

A workspace combines:

- compute resources;
- object storage;
- user permissions;
- billing;
- project settings.

A workspace can be created through:

- Web Console;
- CLI;
- REST API.

Billing must be active before a workspace can be created.

---

### Workspace Names

A workspace name is a technical resource identifier.

Workspace names may contain:

- Latin letters;
- numbers;
- hyphens.

Spaces, Cyrillic characters, and special characters are not supported.

The restriction exists because the workspace name is used as a technical identifier in APIs, CLI commands, URLs, and internal resource names.

---

### Regions

A workspace is created in a specified region.

Example region identifiers include:

- ru-central1
- eu-central1

The region API parameter is a string. The backend validates whether the requested region is supported.

This allows NeuroStack to add new regions without changing the API format or requiring clients to update a hardcoded list.

Region selection affects resource location, latency, availability, and potentially cost.

---

### Workspace Limits

Workspace and Jupyter Server limits depend on the billing plan.

| Plan | Workspaces | Jupyter Servers per workspace |
|------|------------|-------------------------------|
| Free | 1 | 1 |
| Standard | 5 | 3 |
| Pro | 20 | 10 |
| Enterprise | Custom | Custom |

Other resource quotas may also depend on the plan. Exact quotas are documented separately when defined.

---

### Workspace Roles

NeuroStack uses role-based access control.

**Owner**

Has full workspace access, including:

- billing management;
- user management;
- resource management.

**Admin**

Can manage:

- workspace resources;
- users;
- project settings.

An Admin cannot transfer workspace ownership.

**Editor**

Can work with project resources but cannot manage users or billing.

**Viewer**

Has read-only access to the workspace.

### Permission model

Workspace roles apply to all resources within the workspace, including Jupyter Servers, training jobs, model artifacts, and endpoints.

NeuroStack does not support individual permission overrides for specific resources. Permissions cannot be changed for a single resource without changing the user's workspace role.

This model keeps access control consistent across the workspace and avoids the need to manage permissions separately for each resource.

---

### Workspace Errors

The following workspace-related errors are defined:

- `BILLING_NOT_LINKED`
- `INSUFFICIENT_PERMISSIONS`
- `INTERNAL_ERROR`
- `WORKSPACE_LIMIT_EXCEEDED`

`BILLING_NOT_LINKED` means that the required billing account is not connected or active.

`INSUFFICIENT_PERMISSIONS` means that the current user does not have permission to perform the requested action.

`INTERNAL_ERROR` indicates an unexpected internal system failure rather than invalid user input.

`WORKSPACE_LIMIT_EXCEEDED` indicates that the workspace quota for the current plan has been reached.

---

## Jupyter Server

A Jupyter Server provides a managed development environment inside a workspace.

Users can select a compute configuration when starting a Jupyter Server.

Currently defined example configurations include:

| Configuration | CPU | RAM | GPU |
|---------------|-----|-----|-----|
| cpu-small | 2 vCPU | 8 GB | None |
| cpu-medium | 4 vCPU | 16 GB | None |
| gpu-small | 4 vCPU | 16 GB | 1 GPU |
| gpu-t4 | 8 vCPU | 32 GB | 1 × T4 |

CPU configurations are suitable for ordinary development and smaller workloads. GPU configurations are intended for workloads that benefit from GPU acceleration, such as deep learning.

Exact pricing and the complete list of supported configurations are not currently defined.

NeuroStack officially supports Python in Jupyter environments. Exact supported Python versions are not currently fixed.

---

## ML Workflow

The primary ML workflow documented by the project is:

```mermaid
graph TD
    A[Workspace] --> B[Jupyter Server]
    B --> C[Data]
    C --> D[Training code]
    D --> E[Training job]
    E --> F[Model artifact]
    F --> G[Deployment]
    G --> H[Endpoint]
    H --> I[Inference]
    I --> J[Monitoring]
```

Each stage has a corresponding concept or workflow in the documentation.

---

## Training Jobs

A training job is a background process that trains a machine learning model.

Training uses data and training code to produce a trained model.

NeuroStack handles the compute environment required to run the training job so users do not need to manage the underlying infrastructure directly.

Detailed training configuration, scheduling, and API schemas are not yet defined.

---

## Artifacts and Models

A model artifact is a stored snapshot of a trained model that can be registered and used for deployment.

The documentation distinguishes between:

- **artifact** — a stored output produced by a workflow;
- **model** — a trained ML model represented by a registered model artifact and used for deployment or inference.

The exact artifact registry API and metadata schema are not yet defined.

---

## Deployment and Endpoints

Deployment makes a trained model available for inference.

A deployed model is exposed through an API endpoint.

NeuroStack endpoints support auto-scaling.

The exact auto-scaling configuration, scaling metrics, limits, and policies are not yet defined.

---

## Inference

Inference is a request sent to a deployed model endpoint to obtain a prediction or model response.

The exact request and response schemas are not yet defined.

---

## Monitoring

NeuroStack provides monitoring for deployed endpoints.

Monitoring covers endpoint health, performance, and resource usage.

The exact metrics, dashboards, alerts, and retention periods are not yet defined.

---

## API and CLI

NeuroStack provides both REST API and CLI access.

The API and CLI are intended to support platform operations such as:

- billing management;
- workspace management;
- Jupyter Server management;
- training;
- model deployment;
- inference.

Exact API endpoints, authentication mechanisms, CLI commands, rate limits, and request/response schemas are not yet defined.

---

## Decisions Still to be Defined

The following areas require additional product decisions before they can be documented in detail:

- exact pricing and billing rates;
- complete quota model;
- supported regions;
- complete compute configuration list;
- Python version support;
- API authentication;
- API request and response schemas;
- CLI command structure;
- training configuration;
- artifact metadata;
- deployment configuration;
- auto-scaling policies;
- inference schemas;
- monitoring metrics and alerting;
- data management workflows;
- security model beyond workspace-level RBAC (for example, organization-level roles, per-resource overrides, service accounts);
- CI/CD integration.

These items should be defined before corresponding reference or procedural documentation is treated as final.

---

## Decision-Making Principle

When product behavior is not defined, documentation should not invent implementation details.

Instead:

1. Identify the missing product decision;
2. Clarify the expected behavior;
3. Record the decision;
4. Update the relevant documentation;
5. Keep terminology and behavior consistent across the documentation set.
