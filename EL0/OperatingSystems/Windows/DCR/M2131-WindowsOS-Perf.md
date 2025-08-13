# ======= EDIT THESE =======
$TenantID       = "231fba77-bebd-4bd8-ba2e-e01c6f72c37d"
$SubscriptionID = "4260a1bd-84f2-4114-8197-2bbf9a9350a1"
$ResourceGroup  = "sentinel"
$Location       = "eastus"
$DcrName        = "M2131-WindowsOS-Perf"
$WorkspaceId    = "/subscriptions/4260a1bd-84f2-4114-8197-2bbf9a9350a1/resourcegroups/sentinel/providers/microsoft.operationalinsights/workspaces/sentinellaw" # e.g. /subscriptions/.../resourceGroups/sentinel/providers/Microsoft.OperationalInsights/workspaces/sentinellaw
# ==========================

# Auth (Az.Accounts only)
if (-not (Get-Module -ListAvailable -Name Az.Accounts)) { Install-Module Az.Accounts -Force -AllowClobber }
Import-Module Az.Accounts
Connect-AzAccount -Tenant $TenantID -Subscription $SubscriptionID | Out-Null

# DCR REST endpoint
$MgmtBase   = "https://management.azure.com"
$ApiVersion = "2023-03-11"
$DcrResId   = "/subscriptions/$SubscriptionID/resourceGroups/$ResourceGroup/providers/Microsoft.Insights/dataCollectionRules/$DcrName"
$Uri        = "$MgmtBase$DcrResId`?api-version=$ApiVersion"

# Full perf counter spec (Microsoft-Perf)
$counterSpecifiers = @(
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
)

# Build DCR body (Microsoft-Perf -> LA dest -> Custom-m2131_perf_CL; no transform, we keep 'source')
$Body = @{
  location   = $Location
  properties = @{
    kind            = "Windows"  # optional, aligns with your example
    dataSources     = @{
      performanceCounters = @(
        @{
          name                       = "perfCounterDataSource60"
          streams                    = @("Microsoft-Perf")
          samplingFrequencyInSeconds = 60
          counterSpecifiers          = $counterSpecifiers
        }
      )
    }
    destinations    = @{
      logAnalytics = @(
        @{
          name                = "la-dest"
          workspaceResourceId = $WorkspaceId
        }
      )
    }
    dataFlows       = @(
      @{
        streams      = @("Microsoft-Perf")
        destinations = @("la-dest")
        transformKql = "source"
        # IMPORTANT: This routes to your custom Aux table (must already exist as Auxiliary)
        outputStream = "Custom-m2131_perf_CL"
      }
    )
  }
} | ConvertTo-Json -Depth 10

Invoke-AzRestMethod -Method PUT -Uri $Uri -Payload $Body | Out-Null
Write-Host "✅ DCR '$DcrName' created/updated (no associations)." -ForegroundColor Green
