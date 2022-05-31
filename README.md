# ARM template for Azure

ARM template and parameter files for deploying mxdeployer resources

## Prerequisites
* [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

## Parameter files

### parameters.json

This is the parameter file for the production deployment.

## Creating a resource group using the template

First, create a resource group using the Azure CLI:

    $> az group create --name rg-mxdeployer-prod-westus2 --location "West US 2"

Next, create the resources within the group:

    $> az deployment group create --name rg-mxdeployer-prod-westus2 --resource-group rg-mxdeployer-prod-westus2 --template-file template.json --parameters parameters.json

It will take some time for this to run, but shouldn't take more than 30 minutes.

## Deleting a resource group

If you make a mistake, you can delete a resource group using the Azure CLI like this:

    $> az group delete --resource-group rg-mxdeployer-prod-westus2

Please note that it will take quite some time to run, but no more than 10 minutes.

## Retrieving connection strings for configuration files

### Configure Service Bus Namespace Primary Connection String

Use the following query to retrieve the primary connection string for the service bus namespace. 

    $> az servicebus namespace authorization-rule keys list --resource-group rg-mxdeployer-prod-westus2 --namespace-name sb-mxdeployer-test --name Private --query primaryConnectionString

    $> az servicebus namespace authorization-rule keys list --resource-group rg-mxdeployer-prod-westus2 --namespace-name sb-mxdeployer-test --name Public --query primaryConnectionString

### Configure Storage Connection String

    $> az storage account show-connection-string -g rg-mxdeployer-prod-westus2 -n stmxdeployertest --query connectionString
