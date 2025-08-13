```
# ==== YOUR VALUES ====
$TenantID       = ""
$SubscriptionID = ""
$ResourceGroup  = ""
$WorkspaceName  = ""
$TableName      = "m2131_perf_CL"   # must end with _CL
$RetentionDays  = 730               # adjust as needed
# =====================

Import-Module Az.Accounts -ErrorAction Stop
Connect-AzAccount -Tenant $TenantID -Subscription $SubscriptionID | Out-Null

$MgmtBase = "https://management.azure.com"
$WsId = "/subscriptions/$SubscriptionID/resourceGroups/$ResourceGroup/providers/Microsoft.OperationalInsights/workspaces/$WorkspaceName"
$TableResPath = "$WsId/tables/$TableName"
$ApiVersion = "2023-01-01-preview"   # REQUIRED for Auxiliary plan

# IMPORTANT: Auxiliary tables cannot have 'dynamic' columns.
$Body = @{
  properties = @{
    schema = @{
      name    = $TableName
      columns = @(
        @{ name = "TimeGenerated";     type = "datetime" }
        @{ name = "Computer";          type = "string"   }
        @{ name = "ObjectName";        type = "string"   }
        @{ name = "CounterName";       type = "string"   }
        @{ name = "CounterPath";       type = "string"   }
        @{ name = "InstanceName";      type = "string"   }
        @{ name = "CounterValue";      type = "real"     }
        @{ name = "SampleCount";       type = "int"      }
        @{ name = "Min";               type = "real"     }
        @{ name = "Max";               type = "real"     }
        @{ name = "Average";           type = "real"     }
        @{ name = "StandardDeviation"; type = "real"     }
        @{ name = "BucketStartTime";   type = "datetime" }
        @{ name = "BucketEndTime";     type = "datetime" }
        @{ name = "SourceSystem";      type = "string"   }
      )
    }
    totalRetentionInDays = $RetentionDays
    plan = "Auxiliary"   # <-- REQUIRED
  }
} | ConvertTo-Json -Depth 6

$uri = "$MgmtBase$TableResPath`?api-version=$ApiVersion"
Invoke-AzRestMethod -Method PUT -Uri $uri -Payload $Body | Out-Null
Write-Host "Created/ensured Auxiliary table $TableName" -ForegroundColor Green

# Verify
$tables = Invoke-AzRestMethod -Method GET -Uri "$MgmtBase$($WsId)/tables?api-version=$ApiVersion"
($tables.Content | ConvertFrom-Json).value | Select-Object -ExpandProperty name | Sort-Object | Out-Host
```
