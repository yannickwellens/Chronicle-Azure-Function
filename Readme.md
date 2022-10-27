# Chronicle Azure Function

## Run
Azure function is deployed through visual studio publish on func-dpb-chronicle-l-weu-01

You can change the logsources to be ingested by changing LogTypes in [application settings](https://portal.azure.com/#@delenbe.onmicrosoft.com/resource/subscriptions/20d94b62-dbca-4e5a-a3a4-32c674807de2/resourceGroups/rg-dpb-infosec-l-weu-01/providers/Microsoft.Web/sites/func-dpb-chronicle-l-weu-01/configuration)
This needs to be a oneliner json in the following form (do not escape "):

```[ { "ChronicleTag": "WINDOWS_DEFENDER_ATP", "LogSourceCategories":["AdvancedHunting-DeviceFileEvents","AdvancedHunting-DeviceProcessEvents","AdvancedHunting-DeviceLEvents"] } ]```

## Build and Run Locally

1. Start visual studio 2022 under your admin username (you will need to do this to be able to publish the app)
2. Create a user secrets.json file if it doesn't exist yet by **right clicking on connected services**, **manage connected services** and choosing the plus icon and then **Secrets.json (local)**
4. Add the following **key-value** pairs in **Secrets.json**

```
"eventhub03":"<EVENTHUB CONNECTION STRING>" 
"serviceAccount":"<GOOGLE SERVICEACCOUNT JSON>" (needs to be a oneline and escaped --> e.g. "{ \"type\": \"service_account\", \"project_id\": \"malachite-dlb\",...)
```
4. Build the project

Running the azure function locally leverages azure function core cli, currently the loglevel default is set to warning in host.json, this is only for local development.

## Publish
1. Right click your solution and select publish
2. If there is no publish endpoint configured choose **+ New**. This will connect to azure and you should see **func-dpb-chronicle-l-weu-01**, add this function
3. Choose **Show all settings**, choose **File publish options** and select **Remove additional files at destination**
4. Run publish (sometimes publish fails due to HTTP error code, just rerun publish then)
