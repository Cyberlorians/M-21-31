```
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "workspaceResourceId": {
      "type": "string",
      "metadata": { "description": "Resource ID of the target Log Analytics workspace." }
    },
    "dcrName": {
      "type": "string",
      "defaultValue": "M2131-WindowsOS-Perf",
      "metadata": { "description": "Name of the Data Collection Rule (edit here if needed)." }
    },
    "customTableName": {
      "type": "string",
      "defaultValue": "m2131_perf_CL",
      "metadata": { "description": "Custom table name for output (edit here if needed)." }
    },
    "osKind": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [ "Windows" ]
    },
    "samplingFrequencyInSeconds": {
      "type": "int",
      "defaultValue": 60,
      "minValue": 10
    },
    "tags": {
      "type": "object",
      "defaultValue": {}
    }
  },
  "variables": {
    "destName": "[concat('la-', uniqueString(parameters('workspaceResourceId')))]"
  },
  "resources": [
    {
      "type": "Microsoft.Insights/dataCollectionRules",
      "apiVersion": "2023-03-11",
      "name": "[parameters('dcrName')]",
      "location": "[resourceGroup().location]",
      "kind": "[parameters('osKind')]",
      "tags": "[parameters('tags')]",
      "properties": {
        "streamDeclarations": {},
        "dataSources": {
          "performanceCounters": [
            {
              "streams": [ "Microsoft-Perf" ],
              "samplingFrequencyInSeconds": "[parameters('samplingFrequencyInSeconds')]",
              "counterSpecifiers": [
                "\\Processor Information(_Total)\\% Processor Time",
                "\\Processor Information(_Total)\\% Privileged Time",
                "\\Processor Information(_Total)\\% User Time",
                "\\Processor Information(_Total)\\Processor Frequency",
                "\\System\\Processes",
                "\\Process(_Total)\\Thread Count",
                "\\Process(_Total)\\Handle Count",
                "\\System\\System Up Time",
                "\\System\\Context Switches/sec",
                "\\System\\Processor Queue Length",
                "\\Memory\\% Committed Bytes In Use",
                "\\Memory\\Available Bytes",
                "\\Memory\\Committed Bytes",
                "\\Memory\\Cache Bytes",
                "\\Memory\\Pool Paged Bytes",
                "\\Memory\\Pool Nonpaged Bytes",
                "\\Memory\\Pages/sec",
                "\\Memory\\Page Faults/sec",
                "\\Process(_Total)\\Working Set",
                "\\Process(_Total)\\Working Set - Private",
                "\\LogicalDisk(_Total)\\% Disk Time",
                "\\LogicalDisk(_Total)\\% Disk Read Time",
                "\\LogicalDisk(_Total)\\% Disk Write Time",
                "\\LogicalDisk(_Total)\\% Idle Time",
                "\\LogicalDisk(_Total)\\Disk Bytes/sec",
                "\\LogicalDisk(_Total)\\Disk Read Bytes/sec",
                "\\LogicalDisk(_Total)\\Disk Write Bytes/sec",
                "\\LogicalDisk(_Total)\\Disk Transfers/sec",
                "\\LogicalDisk(_Total)\\Disk Reads/sec",
                "\\LogicalDisk(_Total)\\Disk Writes/sec",
                "\\LogicalDisk(_Total)\\Avg. Disk sec/Transfer",
                "\\LogicalDisk(_Total)\\Avg. Disk sec/Read",
                "\\LogicalDisk(_Total)\\Avg. Disk sec/Write",
                "\\LogicalDisk(_Total)\\Avg. Disk Queue Length",
                "\\LogicalDisk(_Total)\\Avg. Disk Read Queue Length",
                "\\LogicalDisk(_Total)\\Avg. Disk Write Queue Length",
                "\\LogicalDisk(_Total)\\% Free Space",
                "\\LogicalDisk(_Total)\\Free Megabytes",
                "\\Network Interface(*)\\Bytes Total/sec",
                "\\Network Interface(*)\\Bytes Sent/sec",
                "\\Network Interface(*)\\Bytes Received/sec",
                "\\Network Interface(*)\\Packets/sec",
                "\\Network Interface(*)\\Packets Sent/sec",
                "\\Network Interface(*)\\Packets Received/sec",
                "\\Network Interface(*)\\Packets Outbound Errors",
                "\\Network Interface(*)\\Packets Received Errors"
              ],
              "name": "[concat(parameters('dcrName'), '-PC')]"
            }
          ]
        },
        "destinations": {
          "logAnalytics": [
            {
              "workspaceResourceId": "[parameters('workspaceResourceId')]",
              "name": "[variables('destName')]"
            }
          ]
        },
        "dataFlows": [
          {
            "streams": [ "Microsoft-Perf" ],
            "destinations": [ "[variables('destName')]" ],
            "transformKql": "source",
            "outputStream": "[concat('Custom-', parameters('customTableName'))]"
          }
        ]
      }
    }
  ]
}
```
