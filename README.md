# azure-managed-identity
Demoing Azure Managed Identity (previously known also as MSI) with RBAC model for Azure DevOps

## Demoing Managed Identity in Azure App Service

$resource = "https://graph.microsoft.com"
$endpoint = $env:IDENTITY_ENDPOINT
$header = $env:IDENTITY_HEADER
$apiVersion = "2019-08-01"

$headers = @{ 'X-Identity-Header' = $header }

$url = "$($endpoint)?api-version=$apiVersion&resource=$resource"

$response = Invoke-RestMethod -Method Get -Uri $url -Headers $headers
$response.access_token
![image](https://user-images.githubusercontent.com/6548359/133921550-e63c441a-59e1-4083-bc98-b42f8911817c.png)
