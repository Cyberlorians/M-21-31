{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "dataCollectionRuleName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Data Collection Rule"
      }
    },
    "location": {
      "type": "string",
      "defaultValue": "eastus",
      "metadata": {
        "description": "Location for the Data Collection Rule"
      }
    },
    "workspaceName": {
      "type": "string",
      "defaultValue": "M2131-ICAM-EntraConnectAdminActions",
      "metadata": {
        "description": "Name of the Log Analytics Workspace"
      }
    },
    "workspaceResourceGroup": {
      "type": "string",
      "metadata": {
        "description": "Resource group of the Log Analytics Workspace"
      }
    },
    "workspaceSubscriptionId": {
      "type": "string",
      "metadata": {
        "description": "Subscription ID of the Log Analytics Workspace"
      }
    }
  },
  "variables": {
    "workspaceResourceId": "[format('/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.OperationalInsights/workspaces/{2}', parameters('workspaceSubscriptionId'), parameters('workspaceResourceGroup'), parameters('workspaceName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Insights/dataCollectionRules",
      "apiVersion": "2023-03-11",
      "name": "[parameters('dataCollectionRuleName')]",
      "location": "[parameters('location')]",
      "kind": "Windows",
      "properties": {
        "dataSources": {
          "windowsEventLogs": [
            {
              "streams": [
                "Microsoft-Event"
              ],
              "xPathQueries": [
                "Application!*[System[EventID=2503 or EventID=2504 or EventID=2505 or EventID=2506 or EventID=2507 or EventID=2508 or EventID=2509 or EventID=2510 or EventID=2511 or EventID=2512 or EventID=2513 or EventID=2514 or EventID=2515 or EventID=2516 or EventID=2517 or EventID=2518 or EventID=2519 or EventID=2520 or EventID=2521]]"
              ],
              "name": "eventLogsDataSource"
            }
          ]
        },
        "destinations": {
          "logAnalytics": [
            {
              "workspaceResourceId": "[variables('workspaceResourceId')]",
              "name": "la-destination"
            }
          ]
        },
        "dataFlows": [
          {
            "streams": [
              "Microsoft-Event"
            ],
            "destinations": [
              "la-destination"
            ],
            "transformKql": "source",
            "outputStream": "Microsoft-Event"
          }
        ]
      }
    }
  ]
}
