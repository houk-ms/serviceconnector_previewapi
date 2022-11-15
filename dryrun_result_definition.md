# Dryrun Response
Dryrun response consists of two parts
- `prerequisiteResults`: Pre-check of the request payload and users' permissions.
- `operationPreivews`: Actions SC will take when creating the connection.

## prerequisiteResults
The result has two possible types
- `permissionMissing`: User doesn't have the permission to create connection.
- `basicError`: All other possible errors in connection creation (share same error codes and messages with PUT connection request).

Sample of `permissionMissing` type.
```
{
    "type": "permissionsMissing",
    "scope": "/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/servicelinker-test-linux-group/providers/Microsoft.KeyVault/vaults/sc-kv-reader",
    "permissions": [
        "Microsoft.KeyVault/vaults/write"
    ]
}
```

Sample of `basicError` type. Cases below are the main errors users may see in dryrun response.
```
Case1.
{
    "type": "basicError",
    "code": "ResourceNotFound",
    "message": "The Resource 'Microsoft.Storage/storageAccounts/houkaccount2' under resource group 'houk-test' was not found.",
}
```

```
Case2.
{
    "type": "basicError",
    "code": "InvalidDbSecret",
    "message": "Error in username or password.",
}
```

```
Case3.
{
    "type": "basicError",
    "code": "InvalidArgument",
    "message": "Client type Django is not supported by target resource. Supported client types are None,Dotnet,Java,Nodejs,Python,SpringBoot"
}
```

## operationPreivews
When `authType == secret`, the result has the following possible types
- `ConfigFirewallRule`: When caller IP is not in firewall white list.
- `ConfigKeyVaultSecret`: When using keyvault secret store.
- `ListAccessKeys`: **Only possible in cloud connection**, as local connection won't list access key in creation, instead, it lists access key in generateConfiguration.
- `ConfigSourceProperties`: **Only possible in cloud connection**, as local connection won't config app settings.

Sample of `ConfigFirewallRule` type.
```
{
    "name": "configFirewallRule",
    "operationType": "configNetwork",
    "description": "Config firewall rule for target service to allow source service access",
    "action": "Microsoft.KeyVault/vaults/write",
    "scope": "/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/servicelinker-test-linux-group/providers/Microsoft.KeyVault/vaults/sc-kv-reader"
}
```

Sample of `ConfigKeyVaultSecret` type.
```
{
    "name": "configKeyVaultSecret",
    "operationType": "configConnection",
    "description": "Config key vault secret for credentials",
    "action": "Microsoft.KeyVault/vaults/secrets/write",
    "scope": "/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.KeyVault/vaults/houk-vault"
}
```

Sample of `ListAccessKeys` type.
```
{
    "name": "listAccessKeys",
    "operationType": "configConnection",
    "description": "List access keys of target service to build connection information",
    "action": "Microsoft.Storage/storageAccounts/listkeys/action",
    "scope": "/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.Storage/storageAccounts/houkaccount"
}
```

Sample of `ConfigSourceProperties` type.
```
{
    "name": "configSourceProperties",
    "operationType": "configConnection",
    "description": "Config appsettings for source service",
    "action": "Microsoft.Web/sites/config/write",
    "scope": "/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.Web/sites/houk-wa"
}
```