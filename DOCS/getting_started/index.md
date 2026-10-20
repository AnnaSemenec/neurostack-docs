# Getting started

This section helps you start working with NeuroStack: from choosing a plan to running your first inference request.

Follow the steps in order. Each step builds on the previous one and results in a working part of your ML workflow.

## Prerequisites

Before you begin, make sure you have:

- An email address to create a NeuroStack account.
- A payment card or invoice details, if you plan to use a paid plan.
- An internal billing code from your organization, if your company pays for NeuroStack.

See [Prerequisites](./prerequisites.md) for details.

## Workflow overview

```mermaid
graph LR
    A[Choose a plan] --> B[Create account]
    B --> C[Create workspace]
    C --> D[Start Jupyter Server]
    D --> E[Upload data]
    E --> F[Prepare training code]
    F --> G[Run training job]
    G --> H[Register artifact]
    H --> I[Deploy model]
    I --> J[Run inference]
```

## Steps

1. [Choose a plan](./choose-plan.md) — select the plan that fits your needs.
2. [Create account](./create-account.md) — create your account and complete billing setup, if required by your plan.
3. [Create a workspace](./create-workspace.md) — create an isolated environment for your ML project.
4. [Start a Jupyter Server](./start-jupyter.md) — launch a managed development environment.
5. [Upload data](./upload-data.md) — add datasets to object storage.
6. [Prepare training code](./prepare-training-code.md) — write or upload the code that trains your model.
7. [Run a training job](./run-training-job.md) — train your model on managed compute resources.
8. [Register a model artifact](./register-artifact.md) — save the trained model for deployment.
9. [Deploy the model](./deploy-model.md) — expose the model through an API endpoint.
10. [Run inference](./run-inference.md) — send a request to the endpoint and get a prediction.

## After you finish

Once you complete all steps, you will have a working ML workflow: a trained model deployed as an API endpoint that returns predictions.

To learn more about individual platform resources and concepts, see [Concepts](../concepts/index.md).

If you run into problems, see [Troubleshooting](../troubleshooting/index.md).
