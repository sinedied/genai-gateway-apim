# Azure APIM Azure Open AI sample

This is a sample project that demonstrates how to use Azure API Management and Azure Open AI to create a simple chatbot.

## Quick Start

### Prerequisites

- Install [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- Install [Node.js](https://nodejs.org/en/download/)

## 1. Deploying the project

Deployment involves using Azure CLI to deploy the resources on a selected resource group.

### Setup

This setup step will ensure you have bicep installed and a resource group created..

```bash
az login
az account set --subscription <Your Subscription ID>
az group create -n <Your Resource Group Name> -l <Your Resource Group Location>
az bicep install
```

> NOTE: if you only have one subscription, you can skip the `az account set` command or if your default subscription is the one you want to use.

### Deploy

> NOTE: make sure you've run `azd auth login` to login to Azure before proceeding below.

To deploy the project run the following commands:

```bash
azd up
```

> NOTE: when you're asked for `environmentName`, it can be any string of your choosing, for example "APIM" as it serves as a prefix for naming resources in your deployment.

## Inspect environment variables (no action here)

A `.env` file has been generated for you under `src/.env` that enables you to run this project locally. Here's what it consists of:

```bash
SUBSCRIPTION_KEY="<Your Subscription Key>"
DEPLOYMENT_ID="<Your Deployment ID>"
API_VERSION="<Your API Version>"
APIM_ENDPOINT="<Your APIM Endpoint>"
API_SUFFIX="<Your API Suffix>"
```

**See below how to find the values in Azure Portal:**

    
|Value  |Instruction  |
|---------|---------|
|SUBSCRIPTION_KEY     | Navigate to portal.azure.com -> Select rg -> select APIM instance -> Go to APIs/Subscriptions -> Click show/hide keys on first row (Built-in all-access) -> copy Primary key        |
| DEPLOYMENT_ID | Navigate to portal.azure.com -> Select rg -> Select 1st OpenAI instance -> Go to Resource Management/Mode deployments -> Click on Manage Deployments to open Azure AI Studio -> Copy Deployment name |
| API_VERSION | Navigate to <https://learn.microsoft.com/azure/ai-services/openai/reference#completions>, Copy most recent Supported versions = 2024-02-01 |
| APIM_ENDPOINT | Navigate to portal.azure.com -> Select rg -> Select APIM instance -> Go to Overview -> Copy Gateway URL |
| API_SUFFIX | Navigate to portal.azure.com -> Select rg -> Select APIM instance -> Navigate to APIs/APIs -> open myAPI -> Go to settings -> Copy API URL suffix |

## 3. Run the project locally

Once you have set the environment variables, you can run the app by running the below commands:

```bash
cd src
npm i
npm start
```

This will start the app on `http://localhost:3000` and the API is available at `http:localhost:1337`.

## Deprovisioning

To remove all deployed resources, run the following command:

```bash
az down --purge
```

The preceding command removes all provisoned resources. The `--purge` hard deletes all resources.

> NOTE: some resources on Azure are only soft deleted for performance reasons and can be retrieved. BY using `--purge` resources are hard deleted and cannot be retrieved.


## What's in this repo

|What  |Description  | Link |
|---------|---------|--|
|Frontend     | a frontend consisting of a `index.html` and `app.js` | [Link](./src/web/)        |
|Backend     | A backend written in Node.js and Express framework | [Link](./src/api/)        |
|Bicep     | Bicep files containing the needed information to deploy resources and configure them as needed        | [Link](./main.bicep) |

## Demo

![App running](./apim.png)

## Documentation

The documentation for this project is available in the [DOC.md](./DOC.md) file.
