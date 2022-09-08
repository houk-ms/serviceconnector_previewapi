## Dryrun
### create dryrun resource
az rest --method put --resource https://management.azure.com/ --url https://eastus2euap.management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/houk-test2/providers/Microsoft.ServiceLinker/locations/eastus2euap/dryruns/houklc-dryrun?api-version=2022-07-01-privatepreview --body `@dryrun_sp.json

### get dryrun result from Azure-AsyncOperation
az rest --method get --resource https://management.azure.com/ --url https://eastus2euap.management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/providers/Microsoft.ServiceLinker/locations/EASTUS2EUAP/operationStatuses/ef656b0e-1d3b-412c-acbb-69552c06c407*17D7510AF355A02349988CE29D299B7620644D47A49C52D9AC561D88C79FA612?api-version=2022-05-01


## Create Connector
### create a connector with sp auth
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/houk-test2/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc?api-version=2022-07-01-privatepreview --body `@create_sp.json

### create a connector, save connection info into keyvault
az rest --method put --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/houk-test2/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc?api-version=2022-07-01-privatepreview --body `@create_sp_kvstore.json


## GenerateConfigurations
### get the original configurations of a connector
az rest --method post --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/houk-test2/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc/generateConfigurations?api-version=2022-07-01-privatepreview --body '{}'

### customize configuration key name
az rest --method post --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/houk-test2/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc/generateConfigurations?api-version=2022-07-01-privatepreview --body `@genconfigs_custkeys.json


## List Connector
az rest --method get --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/houk-test2/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors?api-version=2022-07-01-privatepreview


## Delete Connector
az rest --method delete --url https://management.azure.com/subscriptions/d82d7763-8e12-4f39-a7b6-496a983ec2f4/resourceGroups/houk-test2/providers/Microsoft.ServiceLinker/locations/eastus2euap/connectors/houklc?api-version=2022-07-01-privatepreview