# Deployment of Azure Lighthouse

These templates give the possibility to onboard customer's subscriptions to Azure Lighthouse.
You need to follow the instructions below in order to prepare these templates and pass them to your customer.

## Usage

1. You need to edit the file *delegatedResourceManagement.parameters.json* and update the following parameters:

    * *mspName*: Specify the Managed Service Provider name (ie: My Company Name).
    * *mspOfferDescription*: Name of the Managed Service Provider offering.
    * *managedByTenantId*: Specify the tenant id of the Managed Service Provider (MSP).
    * *authorizations*: Here you need to list one or multiple authorizations as the examples in the file *delegatedResourceManagement.parameters.json*. It must include the following:

        * *principalId*: The *Object ID* of the Azure AD User or Group in your MSP tenant.
        * *principalIdDisplayName*: The name your want to associate with this authorization.
        * *roleDefinitionId*: The RBAC Role ID. You can find a list under the [Azure built-in roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles)

2. Forward the files *delegatedResourceManagement.parameters.json* and *delegatedResourceManagement.json* to your customer.

3. Connect to the Azure account:
    ```
    Connect-AzAccount
    ```
2. Deploy the template:

    ```
    New-AzDeployment -Name <My Deployment Name> `
    -Location 'Azure Region' `
    -TemplateFile delegatedResourceManagement.json `
    -TemplateParameterFile delegatedResourceManagement.parameters.json `
    -Verbose
    ```

    Example:
    ```
    New-AzDeployment -Name ManagedServices `
    -Location 'West Europe' `
    -TemplateFile delegatedResourceManagement.json `
    -TemplateParameterFile delegatedResourceManagement.parameters.json `
    -Verbose
    ```