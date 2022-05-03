# Configure Salem to use customer defined secrets

When Salem accesses third party systems, it will likely need customer managed secrets.  This guide will walk you through enabling Salem to access a customer managed key vault to read secret values.

1. Use and existing or key vault or create a new Azure Key Vault in the same subscription as the Salem application.  For new Key Vaults, we recommend adding them to the same resource group as the Salem Managed Application.
2. Ensure the new key vault is configured to use role-based access control (RBAC) permissions.  You will find this configuration under `Access policies` for the Key Vault
3. Under `Access control (IAM)`, select `Add` to add a role assignment for the Salem API managed identity.
4. Select the `Key Vault Secrets User` role.  Under members, select `Managed identity` and then find the user-assigned managed identity who's name begins with `APIAppId`
5. Save

Salem can now access secrets in this Key Vault.  You will configure the name of the vault and the secret name as parameters in an ActionDefinition that requires Salem to use a secret to connect to a third party system.

## Added Key Vault Security (optional)
You can restrict network access to this key vault by updating the networking configurations.  Add the Salem virtual network and the api-backend subnet to the the Key Vault allowed virtual networks.