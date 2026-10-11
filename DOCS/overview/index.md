# NeuroStack overview

NeuroStack is a cloud platform for developing, training, deploying, and monitoring machine learning (ML) models.

The platform provides managed development environments, compute resources, object storage, training jobs, and model endpoints. It allows data scientists and ML engineers to work with ML projects without provisioning or managing servers, clusters, or networking directly.

## What you can do with NeuroStack

- Develop ML models in managed Jupyter environments with CPU or GPU resources.
- Store data and artifacts in object storage.
- Train models by running training jobs on managed compute resources.
- Register model artifacts for use in deployment workflows.
- Deploy models as API endpoints with auto-scaling.
- Run inference by sending requests to deployed model endpoints.
- Monitor deployed models for endpoint health, performance, and resource usage.
- Automate workflows through the REST API and CLI.

## Get started

Follow the [Getting Started](../getting-started/index.md) guide to set up billing, create your first workspace, and run your first inference request.

## How the platform works

A typical ML workflow starts with a workspace, where you prepare data and develop training code in a Jupyter environment. You then run a training job, register the resulting model artifact, and deploy the model to an endpoint. Once the endpoint is available, you can send inference requests and monitor its operation.

Before creating a workspace, you must create a billing account, connect a payment method, and ensure that the billing account is active.

## Explore the documentation

- [Platform architecture](./platform-architecture.md) — understand the main platform components and how they relate to one another.
- [Resource hierarchy](./resource-hierarchy.md) — learn how NeuroStack organizes billing accounts, workspaces, and resources.
- [Getting Started](../getting-started/index.md) — follow the onboarding workflow from billing setup to your first inference request.
- [Concepts](../concepts/index.md) — learn about the platform's resources and terminology.

## Access the platform

NeuroStack supports three access methods:

- **Web Console** — interact with the platform through its web interface.
- **REST API** — integrate platform operations into applications and automated workflows.
- **CLI** — manage platform resources from the command line.
