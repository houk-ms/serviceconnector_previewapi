## Dryrun
### create dryrun resource (local connection)
az rest --method put --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.ServiceLinker/locations/eastus2euap/dryruns/houklc-dryrun?api-version=2022-11-01-preview --body `@dryrun_secret.json --debug

### create dryrun resource (cloud connection)
az rest --method put --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.Web/sites/houk-wa/providers/Microsoft.ServiceLinker/dryruns/houklc-dryrun?api-version=2022-11-01-preview --body `@dryrun_secret.json --debug

### get dryrun result from Azure-AsyncOperation
az rest --method get --url <Azure-AsyncOperation>

Check [dryrun result definition](dryrun_result_definition.md) or [dryrun sample response](dryrun_sample_response.json). 

## Create Connector
### create a connector
az rest --method put --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc?api-version=2022-11-01-preview --body `@create_secret.json

### create a connector, save connection info into keyvault
az rest --method put --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc?api-version=2022-11-01-preview --body `@create_secret_kvstore.json


## GenerateConfigurations
### get the original configurations of a connector
az rest --method post --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc/generateConfigurations?api-version=2022-11-01-preview --body '{}'

### customize configuration key name
az rest --method post --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc/generateConfigurations?api-version=2022-11-01-preview --body `@genconfigs_custkeys.json


## List Connector
az rest --method get --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors?api-version=2022-11-01-preview


## Delete Connector
az rest --method delete --url https://management.azure.com/subscriptions/937bc588-a144-4083-8612-5f9ffbbddb14/resourceGroups/houk-test/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc?api-version=2022-11-01-preview
