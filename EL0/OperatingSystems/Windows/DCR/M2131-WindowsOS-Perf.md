```
$TenantID       = ""
$SubscriptionID = ""
$ResourceGroup  = "sentinel"
$Location       = "eastus"
$DcrName        = "M2131-WindowsOS-Perf"
$WorkspaceId    = ""

if (-not (Get-Module -ListAvailable -Name Az.Accounts)) { Install-Module Az.Accounts -Force -AllowClobber }
Import-Module Az.Accounts
Connect-AzAccount -Tenant $TenantID -Subscription $SubscriptionID | Out-Null

$MgmtBase   = "https://management.azure.com"
$ApiVersion = "2022-06-01"
$DcrResId   = "/subscriptions/$SubscriptionID/resourceGroups/$ResourceGroup/providers/Microsoft.Insights/dataCollectionRules/$DcrName"
$Uri        = "$MgmtBase$DcrResId`?api-version=$ApiVersion"

$Body = @{
  location   = $Location
  properties = @{
    dataSources = @{
      performanceCounters = @(
        @{
          name                       = "m2131-perf"
          streams                    = @("Microsoft-InsightsMetrics")
          scheduledTransferPeriod    = "PT1M"
          samplingFrequencyInSeconds = 60
          counterSpecifiers          = @(
            "\\Processor(_Total)\\% Processor Time",
            "\\Memory\\% Committed Bytes In Use",
            "\\PhysicalDisk(_Total)\\Avg. Disk Queue Length",
            "\\PhysicalDisk(_Total)\\Disk Transfers/sec",
            "\\Network Interface(*)\\Bytes Total/sec"
          )
        }
      )
    }
    destinations = @{
      logAnalytics = @(
        @{
          name                = "law-dest"
          workspaceResourceId = $WorkspaceId
        }
      )
    }
    dataFlows = @(
      @{
        streams      = @("Microsoft-InsightsMetrics")
        destinations = @("law-dest")
        outputStream = "Custom-m2131_perf_CL"
      }
    )
  }
} | ConvertTo-Json -Depth 10

Invoke-AzRestMethod -Method PUT -Uri $Uri -Payload $Body | Out-Null
Write-Host "DCR $DcrName created/updated (no associations)." -ForegroundColor Green
```
