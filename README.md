# Azure Devcenter Quickstart

This guide helps accelerate onboarding to the two Azure Services that Azure Devcenter enables;

1. Azure Devbox - Give your developers access to managed Virtual Machines
1. Azure Deployment Environments - Provide curated Azure infra templates to your developers to deploy their code into

## Devcenter concepts

## Prerequisites

You'll need an Azure AD tenant which is licensed at least at P1.
It doesn't work with invited (B2B) identities, so users will need to be directly associated with the tenant.

## Deploy the common infrastructure

Both Dev box and Deployment Environments use several common Devcenter components to drive their experiences. Central to these is the concept of `Projects`. A project is what binds the developer access to developer workstations through Devbox and the relevant templates from ADE.

```bash
az deployment group create -g innerloop -f bicep/common.bicep -p devboxProjectUser=$(az ad signed-in-user show --query id -o tsv)
```

## Azure Devbox

A fully working Devbox requires a lot of connected components. The bicep IaC included in this repository will help expedite the creation of a functioning Devbox.

```bash
 az deployment group create -g innerloop -f bicep/devbox.bicep -p devcenterName=dc-dbox
```

### Deployed Resources

![azure resources](devboxResources.png)

### Access the Devbox

Your Developers will access Devbox resources through a dedicated portal; [https://aka.ms/devbox-portal](https://devbox.microsoft.com/)

![devbox portal](devboxPortal.png)

## Azure Deployment Environments

### Catalog repo

ADE requires a catalog in the form of a Git repository. The catalog contains IaC templates used to create environments.

To quickly get started with a sample catalog, use these commands to fork the [ADE](https://github.com/Azure/deployment-environments) repo.

```bash
gh repo 
```

> After creation of the repository, [create a PAT token](https://learn.microsoft.com/azure/deployment-environments/how-to-configure-catalog#create-a-personal-access-token-in-github) to allow ADE to gain access to these resources
